|      Course Name       |  Topic  | Professor |     Date     |       Tags       |
| :--------------------: | :-----: | :-------: | :----------: | :--------------: |
| **Document Databases** | MongoDB |  Clément  | 22 July 2024 | #Data_Management |

[Class Video Link](https://learn.dsti.institute/mod/url/view.php?id=19385)

# Summary
*MongoDB is a NoSQL document database that uses JSON to allow users to insert, update, query, and aggregate records. MongoDB is very fast because it stores information as serialized binary JSON. Indexes can also be used to improve query performance*

# Key Takeaways
1. Pros: Flexible scalability, dynamic schema, replication, cheaper query cost
2. Cons: Less mature, requires technical skills, poor BI/Analytics capabilities, ACID interpretation
3. All numbers are treated as doubles
4. Aggregations are processed one-by-one in FIFO order
5. Indexes remove the need for MongoDB to perform collection scans

# Definitions
- NoSQL: A data model (storage and retrieval) that is modeled in a way other than [[Relational Database Management System|relational tabular data]]
	- JSON, Graph, etc.
- Document Databases: Store data in a document similar to JSON for general purpose applications
- MongoDB: A document-based NoSQL DBMS that uses binary JSON (BSON)
- Aggregation: Process data records and return computed results by grouping values from multiple documents together
- Collection Scan: Check every document in a collection for the specified condition

# Additional Resources
- [JSON and BSON](https://www.mongodb.com/resources/basics/json-and-bson)
- [BSON Datatypes](https://www.mongodb.com/docs/manual/reference/bson-types/)
- [Update Operations](https://www.mongodb.com/docs/manual/tutorial/update-documents/)
- [Query Operators](https://www.mongodb.com/docs/manual/reference/operator/query/)
- [Aggregation Reference](https://www.mongodb.com/docs/manual/reference/aggregation/)

# Notes
## SQL vs NoSQL
![[Pasted image 20241007124855.png]]
## MongoDB Elements
- Structure
	- Database -> Collection -> Document -> Field
	- Within each document, fields do not have to be consistent
	- Collections are groupings of MongoDB documents that also have no enforced structure
	- Fields are the name-value pairs
- Field Types
	- Have two identifier types (integers and strings)
	- See BSON types link above
## Querying MongoDB
- Console: javascript-like syntax
- Compass GUI: Send instructions directly to the server
- Use/Create a database
	- `use databaseName`
- Insert Record
	- `db.databaseName.insertOne({"key":"value", "key2":"value2"})`
- Delete Record
	- Many Records:`db.<collectionName>.deleteMany({<filters>})`
		- Removes all records in collection with no filters
	- One Record: `db.<collectionName>.deleteOne({<filters>})`
		- First match
- Update Record
	- Supports one (first match) and Many
	- `db.${nameOFYourCollection}.update({<query>},{<update>},{<options>})`
	- Example: `db.<collectionName>.updateOne({<filter>}, {$set:{"key":"value"}})`
- Find Record
	- Similar to `SELECT` in SQL
	- findOne returns the first match
- Count Records
	- `db.<collectionName>.count(<query>)`
- Query Operators
	- `$lt` and `$lte`: less than, less than or equal (numbers and dates)
	- `$gt` and `$gte`: greater than, greater than or equal (numbers and dates)
	- `$in` and `$nin`: In and not in (query a range)
	- `$eq` and `$ne`: Exact match or not exact match (equal and not equal)
- Logical Operators
	- `$and`: Match all clauses in the AND
	- `$not`: Inverse effect of the query
	- `$or`: Query clause joined with logical OR
	- `$nor`: Query clause fail to match ALL inside
- Element Operators
	- `$exists`: Documents that have the specified field
	- `$type`: Select documents if a field is of the specified type
	- `$regex`: Select documents where values match a regular expression
	- `$elemMatch`: Select documents if element in an array field  match all conditions specified
	- `$all`: Match if an array contains at least elements inside the clause (order not important)
## Aggregations
- Aggregation stages
	- Passed as a list to the aggregate method
		- `db.<collectionName>.aggregate([<stages>])`
	- `$match`: Filter documents and pass to next stage unmodified
	- `$project`: Reshape each document
	- `$group`: <mark style="background: #FFB86CA6;">Group input by a specified identifier expression and applies the accumulator expression</mark>
	- `$lookup`: Left join with another collection
	- `$unwind`: <mark style="background: #FFB86CA6;">Deconstruct an array in fields</mark>
- Accumulators (Group and Project)
	- `$max`: Return highest expression value for each group
	- `$min`: Return lowest expression value for each group
	- `$sum`: Returns sum of numeric values
		- Ignores non-numeric values
	- `$avg`: Returns average of numerical values
		- Ignores non-numeric values
	- `$first` and `$last`: Returns value from the first/last document for each group
		- Order is only defined if documents are in order already
## Indexes
- Default
	- `_id` is the default index generated by Mongo when a document is first inserted
	- Client cannot duplicate or drop this index
- Single Field
	- Same as `_id` but can be specified for any fields of a document or embedded document
	- Can be dropped
- Compound Index
	- Index by multiple fields
- Mongo supports text, geospatial, and hashed indexes