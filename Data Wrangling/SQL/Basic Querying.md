|         Course Name         |     Topic      | Professor |    Date     | Tags |
| :-------------------------: | :------------: | :-------: | :---------: | :--: |
| **Data Wrangling with SQL** | Basic Querying |   Hanna   | 15 May 2024 | #SQL |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/ted_codd_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fted%5Fcodd%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FS24%2D%20DS%20%26%20Common%20LINK%20DS%5FDA%5FDE%2D20240515%5F095054%2DMeeting%20Recording%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E3a53272d%2D0226%2D4101%2D80d0%2D49aa642320ee)
[Class Video Link 2]()

# Summary
*Basic queries will allow us to view, filter, and aggregate data from an [[Relational Database Management System|RDBMS]]. We are also able to join datasets together that have [[Data Management & Relational Algebra|functional dependencies]]*

# Key Takeaways
1. Database tables contain tables that are linked via relationships
2. Drivers help with connection to databases but are not always needed

# Definitions
- Aggregation: Calculation of summarized metrics across a dataset or within other attributes
	- Total revenue for each customer

# Additional Resources
- [W3Schools Basic SQL Queries](https://www.w3schools.com/sql/sql_syntax.asp)

# Notes
## Basic Information Queries
- We should always start with a ```SELECT COUNT(*)``` on a table to get a sense of size
	- This will make sure we don't inadvertently crash the database
- To view columns we can do the following:
```sql
-- Column Count
SELECT
	COUNT(*) 
FROM INFORMATION_SCHEMA.Columns 
WHERE 1=1
	AND TABLE_NAME = 'Customers'
	AND TABLE_SCHEMA = 'Sales'
```

## Joins to Gather More Information
```sql
-- Q2: Give me the full postal address of all the customers
SELECT
	 cust.CustomerID
	, cust.CustomerName
	, cust.PostalAddressLine1
	, cust.PostalAddressLine2
	, cty.CityName
	, prov.StateProvinceName
	, cust.PostalPostalCode
FROM
	Sales.Customers AS cust
	, Application.Cities AS cty
	, Application.StateProvinces AS prov
WHERE 1=1
-- Join conditions
AND (cust.PostalCityID = cty.CityID
	OR cty.CityID IS NULL)
AND (cty.StateProvinceID = prov.StateProvinceID
	OR prov.StateProvinceID IS NULL)
```
- In the above query, we first create the cross join between all the tables in the FROM clause
- We then reduce this based on the join conditions


```sql
-- Q3: See the billing information for all customers
SELECT
	  ShipToID					=		ship.CustomerID
	, ShipToName				=		ship.CustomerName
	, BillToName				=		bill.CustomerName
	, BillToAddressLine1		=		bill.PostalAddressLine1
	, BillToAddressLine2		=		bill.PostalAddressLine2
	, BillToCityName			=		cty.CityName
	, BillToState				=		prov.StateProvinceName
	, BillToPostalCode			=		bill.PostalPostalCode
FROM 
	Sales.Customers AS ship
	, Sales.Customers AS bill
	, [Application].Cities AS cty
	, [Application].StateProvinces AS prov
WHERE 1=1
	-- Join Conditions
	AND ship.BillToCustomerID = bill.CustomerID
	AND bill.PostalCityID = cty.CityID
	AND cty.StateProvinceID = prov.StateProvinceID
ORDER BY ShipToID, ShipToName DESC
```
- In this next query, we add to the one from before to order the data by ship to information for clarity

## Aggregation
- The GROUP BY clause allows us to calculate summary metrics within groups
```sql
-- Group Customers by City and show total customer count and total volume for all cities
SELECT City, [PersonCount] = COUNT(*) INTO #CityCounts FROM Customers GROUP BY City
```

- We can also filter based on the results of an aggregation using the HAVING clause
```sql
-- Question: How many customers purchased ALL available products
-- Version 1: Inner query with HAVING Clause
SELECT CustomerID, ProdCount = COUNT(DISTINCT ProductID)
FROM 
	Purchased purch
GROUP BY CustomerID
HAVING COUNT(DISTINCT ProductID) = (SELECT COUNT(*) FROM Products)
```
