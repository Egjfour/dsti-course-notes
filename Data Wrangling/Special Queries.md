|         Course Name         |                 Topic                  | Professor |        Date        | Tags |
| :-------------------------: | :------------------------------------: | :-------: | :----------------: | :--: |
| **Data Wrangling with SQL** | Division, Inner, and Existence Queries |   Hanna   | 15 and 16 May 2024 | #SQL |

# Summary
*There are queries that have some specific syntax to answer key questions that are not immediately obvious. These use largely the same syntax as the [[Basic Querying|basic queries]] with the addition of the ```NOT EXISTS``` keyword.*

# Key Takeaways
1. The ```NOT EXISTS``` keyword is powerful and lets us answer important business questions

# Definitions
- Inner Query: Execute one query first and pass the result onto another query
- Existence Query: Identify items that do or do not exist within a list
	- Are there any products that have no sales
- Division Query: See how many items of one relation are associated with ALL items of another relation within the context of a linking third relation
	- Example: How many customers (relation 1) purchase (relation 3) *all* products (relation 2)

# Additional Resources
- [SQL EXISTS](https://sql.sh/cours/where/exists)
- [Division Queries](https://www.geeksforgeeks.org/sql-division/)

# Notes
## Inner Query
```sql
-- Question: What items are priced at or above any usb item
-- Version 1: Inner Query
SELECT
	wh.StockItemID,
	wh.StockItemName,
	wh.UnitPrice
FROM
	Warehouse.StockItems AS wh,
	(
		SELECT
			MinPrice = MIN(UnitPrice)
		FROM Warehouse.StockItems
		WHERE 1=1
			AND UPPER(StockItemName) LIKE '%USB%'
	) mp
WHERE 1=1
	AND wh.UnitPrice >= mp.MinPrice
	AND UPPER(wh.StockItemName) NOT LIKE '%USB%'
```
- In this example, we create a table that has only a single row and column for the MinPrice of USB items aliased as "mp" to be used for further operations
- This result is passed to the outer query and joined to Warehouse.StockItems
## Existence Query
```sql
-- Question: Are there any customers who have not purchased
SELECT * FROM Customers c
WHERE NOT EXISTS(
 SELECT 1 FROM Purchased p WHERE c.CustomerID = p.CustomerID
)
```
- In an existence query, <mark style="background: #FFB86CA6;">the alias of the outer relation (Customers c) is passed to the inner query</mark> in the WHERE clause
- The match condition is then performed within the inner query
- An existence query will ALWAYS be the optimal way to answer the question "Are there any X that are not found in Y"

## Additional Example (Standard, Inner Query, Existence Query)
- Find all orders that have not yet invoices
```sql
-- Question: Find all orders that have not yet invoiced
-- Version 1: With a Left Outer Join
SELECT
	ord.OrderID
,	ord.OrderDate
FROM Sales.Orders ord
LEFT OUTER JOIN Sales.Invoices inv
	ON ord.OrderID = inv.OrderID
WHERE inv.InvoiceID IS NULL

-- Version 2: Using an inner query
SELECT
	ord.OrderID
FROM
	Sales.Orders ord
WHERE
	ord.OrderID NOT IN (
							SELECT DISTINCT OrderID
							FROM Sales.Invoices
						)

-- Version 3: Existence Query (optimal way to do this)
SELECT
	ord.OrderID
FROM Sales.Orders ord
WHERE 1=1
    AND NOT EXISTS (
        SELECT
            1
        FROM
            Sales.Invoices AS inv
        WHERE
            inv.OrderID = ord.OrderID
    )
```

## Division Query
```sql
-- Question: How many customers purchased ALL available products
-- Version 2: Division Query: Simplest, most effective, and most optimized way to solve this
SELECT * FROM Customers c
WHERE NOT EXISTS (
	SELECT * FROM Products p
	WHERE NOT EXISTS (
		SELECT * FROM Purchased pu
		WHERE pu.CustomerID = c.CustomerID
		AND pu.ProductID = p.ProductID
	)
)
```
- Think of this as a double negative. The select the customers from the list where not all the products were not purchased by a given customer-product combination
- This syntax can be extended to any given number of relations so long as there is an additional table (e.g., given another table vendors, we could find All customers purchasing all products from all vendors)