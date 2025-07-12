|         Course Name         |      Topic       | Professor |    Date     |            Tags             |
| :-------------------------: | :--------------: | :-------: | :---------: | :-------------------------: |
| **Data Wrangling with SQL** | Programmatic SQL |   Hanna   | 17 May 2024 | #SQL #FunctionalProgramming |

[Class Video Link](URL)

# Summary
*Programmatic SQL is used to fill in the gaps between core SQL operations that can be defined within the context of [[Data Management & Relational Algebra|relational algebra]] and extend the languages to include elements such as loops, variable declaration, and most importantly, functions via stored procedures that allow for automation via triggers*

# Key Takeaways
1. Programmatic SQL is useful because it <mark style="background: #FFB86CA6;">introduces functional programming concepts</mark> like loops and parameterizable functions
2. "He who owns the code owns the rights to make decisions about the code and data"
3. The types of events that can be used for triggers are CREATE, UPDATE, and DELETE
4. A stronger locality of data helps to prevent access to malicious actors since the weak points are the transfer of data across systems
5. These operations are not natively supported. Each [[Relational Database Management System|RDBMS provider]] maintains their own implementation for this (e.g., Microsoft has Transact (T)-SQL)

# Definitions
- Data Flow Process: Generally, data flows in 3 parts (UI, back-end, and database)
- Locality of Data: Allowing the data to be able to stay within one of the environments in the data flow process (in this case the database component)
- Transactions: The freezing of order of execution for affected relations that prevents mistakes by having all other actions on that relation wait until the transaction is either committed or rolled back
- Stored Procedure: Reusable pieces of code (closest to functions)
- Trigger: An event (DML, DDL, LOGON) that signifies the start of a run

# Additional Resources
- [Tutorial - Write T-SQL Statements (Microsoft)](https://learn.microsoft.com/en-us/sql/t-sql/tutorial-writing-transact-sql-statements?view=sql-server-ver16)
- [T-SQL Loops](https://www.educba.com/t-sql-loop/)
- [Triggers in SQL Server](https://www.sqlshack.com/triggers-in-sql-server/)

# Notes
## Rationale
- Programmatic SQL (Transact or T-SQL in Microsoft SQL server) introduces functional programming elements to a [[Relational Database Management System|relational database management system]]
	- Loops, Parameters, Flow-Control Statements (if-else)
- Programmatic SQL allows specifically for <mark style="background: #FFB86CA6;">transactions (data integrity), stored procedures (reusability and portability), and triggers (event-based automation)</mark>
## Transactions
- RDBMS are multi-user, concurrent, and [[Networking (TCP and UDP)|networked]]
	- We can freeze order of actions until a commit or rollback of a statement
- Basic Commands and usage (*produced by Chat GPT*)
	- **`BEGIN` TRANSACTION**: Starts a new transaction.
	- **`COMMIT` TRANSACTION**: Saves all changes made during the transaction to the database.
	- **`ROLLBACK` TRANSACTION**: Reverts all changes made during the transaction to the state before the transaction began.
- Example (*produced by Chat GPT*)
```sql
BEGIN TRANSACTION;

-- Debit account A
UPDATE Accounts SET Balance = Balance - 100 WHERE AccountID = 'A';

-- Credit account B
UPDATE Accounts SET Balance = Balance + 100 WHERE AccountID = 'B';

-- Check if operations succeeded
IF @@ERROR <> 0
BEGIN
    ROLLBACK TRANSACTION;
    PRINT 'Transaction rolled back due to error.';
END
ELSE
BEGIN
    COMMIT TRANSACTION;
    PRINT 'Transaction committed successfully.';
END
```

## Stored Procedures & Triggers
- These are functions that can be reused in other areas of the code
- Stored procedures can additionally take input parameters and provide output parameters
```sql
-- This is an example of a stored procedure. 
-- It is a simple example to get the total revenue for products given a parameter price
--DROP PROCEDURE IF EXISTS Warehouse.prod_revenues;
CREATE PROCEDURE Warehouse.prod_revenues @priceLow money, @priceHigh money
	AS
	BEGIN
		-- When the stored procedure is run, the view is overwritten wrt the new params
			SELECT
				p.StockItemID
	,			p.StockItemName
	,			p.UnitPrice
	,			Revenue	  =	  SUM(i.ExtendedPrice)
			FROM
				Warehouse.StockItems p
	,			Sales.InvoiceLines i
			WHERE 1=1
				AND p.UnitPrice >= @priceLow
				AND p.UnitPrice <= @priceHigh
				AND p.StockItemID = i.StockItemID
			GROUP BY p.StockItemID, p.StockItemName, p.UnitPrice;
	END
GO


EXECUTE Warehouse.prod_revenues 40, 80;
GO
```
- Often, these are automated via Triggers which can be set for many operations that are performed on the data (insert, update, delete, etc)
	- NOTE: These specifically are events which have actions. A SELECT cannot be a trigger

## Looping Mechanisms
- There are many different methods that allow for looping
- `WHILE` loops combined with a `CURSOR` object are a powerful way to iterate through table records
	- In this loop, we create a/many declared variable(s) that will place each row's records as the cursor iterates. We then can use these like any other declared variable
	- Very similar to the following in R `data %>% pmap(function(Column1, Column2){})`
```sql
	-- Variable that we will use in our pivot string
	DECLARE @years NVARCHAR(MAX);
	SET @years = '';
	
	-- Variable that will house the query to execute
	DECLARE @query NVARCHAR(MAX);
	
	-- Cursor object to let us to a for-each loop off of table results
	DECLARE YearCursor CURSOR FOR
		SELECT DISTINCT YEAR(InvoiceDate) FROM Sales.Invoices WHERE YEAR(InvoiceDate) BETWEEN @minYear AND @maxYear ORDER BY YEAR(InvoiceDate);
	
	-- Loop through all the years
	DECLARE @currentYear NVARCHAR(MAX); -- We'll use this to dynamically build the @years string
	OPEN YearCursor;
	FETCH NEXT FROM YearCursor INTO @currentYear;
	WHILE @@FETCH_STATUS = 0 -- Once there are no more items, the fetch will end
	BEGIN
		SET @years = @years + '"' + CAST(@currentYear AS nvarchar(MAX)) + '"' + ','
		FETCH NEXT FROM YearCursor INTO @currentYear
	END;
	CLOSE YearCursor;
	DEALLOCATE YearCursor; -- Do this so we can declare each time and reduce memory
	SET @years = SUBSTRING(@years, 1, LEN(@years) - 1); -- This removes the trailing comma
	PRINT 'Creating Pivot Data for Years ' + CAST(@minYear AS NVARCHAR(MAX)) + '-' + CAST(@maxYear AS NVARCHAR(MAX))
```
- In this example, we `DECLARE` YearCursor which is defined as the result of our query passed by `FOR`. It behaves much like a [[Python Generators||generator in python]]
- From there, we open the cursor and grab the first record and store it into our variables
	- NOTE: You need the same number of variables as there are columns
- Then, we iterate until the generator no longer returns anything valid
- Once complete, we close and deallocate our cursor

## Dynamic SQL
- Dynamic SQL allows us to use parameters to execute a query
- We build a query string using our parameters and other results and pass this to an executor
	- This executor has its own exception handling, so there is no need to worry about that
```sql
CREATE OR ALTER PROCEDURE pivot_yearly_sales @minYear int, @maxYear int
AS
BEGIN
	-- Variable that we will use in our pivot string
	DECLARE @years NVARCHAR(MAX);
	SET @years = '';
	
	-- Variable that will house the query to execute
	DECLARE @query NVARCHAR(MAX);
	
	-- Cursor object to let us to a for-each loop off of table results
	DECLARE YearCursor CURSOR FOR
		SELECT DISTINCT YEAR(InvoiceDate) FROM Sales.Invoices WHERE YEAR(InvoiceDate) BETWEEN @minYear AND @maxYear ORDER BY YEAR(InvoiceDate);
	
	-- Loop through all the years
	DECLARE @currentYear NVARCHAR(MAX); -- We'll use this to dynamically build the @years string
	OPEN YearCursor;
	FETCH NEXT FROM YearCursor INTO @currentYear;
	WHILE @@FETCH_STATUS = 0 -- Once there are no more items, the fetch will end
	BEGIN
		SET @years = @years + '"' + CAST(@currentYear AS nvarchar(MAX)) + '"' + ','
		FETCH NEXT FROM YearCursor INTO @currentYear
	END;
	CLOSE YearCursor;
	DEALLOCATE YearCursor; -- Do this so we can declare each time and reduce memory
	SET @years = SUBSTRING(@years, 1, LEN(@years) - 1); -- This removes the trailing comma
	PRINT 'Creating Pivot Data for Years ' + CAST(@minYear AS NVARCHAR(MAX)) + '-' + CAST(@maxYear AS NVARCHAR(MAX))
	
	 --Build our dynamic query
	DROP TABLE IF EXISTS Sales.YearlySalesPivot --Lets us start from scratch on the pivot table each time and change columns based on # yrs provided
	SET @query = 'SELECT
		*
	FROM
		(
			SELECT
				[YEAR] = YEAR(inv.InvoiceDate)
			,	SUM(lines.Quantity * lines.UnitPrice) AS AnnualRevenue
			FROM
				Sales.InvoiceLines lines
			,	Sales.Invoices inv
			WHERE 1=1
				AND lines.InvoiceID = inv.InvoiceID
				AND YEAR(CONVERT(date, inv.InvoiceDate)) >= '+ CAST(@minYear AS NVARCHAR(MAX)) +
				' AND YEAR(CONVERT(date, inv.InvoiceDate)) <= '+ CAST(@maxYear AS NVARCHAR(MAX)) +' 
			GROUP BY YEAR(inv.InvoiceDate)
		) t
	PIVOT (SUM(AnnualRevenue) FOR [YEAR] IN ('+ @years +')) piv'
	SET @query = 'WITH tmp AS(' + @query + ') SELECT * INTO Sales.YearlySalesPivot FROM tmp'
	
	EXECUTE sp_executesql @query;
END;
GO

pivot_yearly_sales 2014, 2016
SELECT * FROM Sales.YearlySalesPivot
```
- This example creates a procedure that dynamically generates a pivot revenue summary by year provided a start and end year
- Note how we systematically build the elements of the query as a string and then dynamically 