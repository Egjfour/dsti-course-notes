|        Course Name        |      Topic      |  Professor  |           Date           |     Tags     |
| :-----------------------: | :-------------: | :---------: | :----------------------: | :----------: |
| **Graph Databases NoSQL** | Querying Graphs | Ana Escobar | 23, 24 & 26 juillet 2024 | #GraphTheory |

# Summary
*A 3-4 sentence description of what was learned in italics*

# Key Takeaways
1. Cypher matches patterns in the data and then returns results (nodes that matched)
2. [[Neo4j|Labels]], property keys, and variables are case-sensitive, but the cypher keywords are not
3. The `MERGE` keyword ensures added nodes are not duplicative. This is not the case with `CREATE`
4. If the direction of the relationship is not specified when created, it is assumed to be left to right

# Definitions
- Cypher: A query language designed for graphs wherein [[Neo4j|nodes]] are represented by parentheses connected together by arrows

# Additional Resources
- [Cypher Cheat Sheet](https://neo4j.com/docs/cypher-cheat-sheet/25/all/)

# Notes
## Cypher Query Syntax Basics
- The `MATCH` keyword lets us find specific patterns using nodes
	- Most basic MATCH (finds all nodes)
		- `MATCH ()`
	- We can also specify node types and relationships between them in the match
		- Example: Match all nodes that are of type student and have a relationship of type taking with a node course
		- `MATCH (s:Student) -[t:Taking]-> (c:Course)`
			- `s`, `t`, and `c` act as aliases for the node and relationship types
	- <mark style="background: #FFB86CA6;">The direction of the arrow matters when defining and querying relationships</mark>
	- We can have multiple clauses in a `MATCH` as well and there are many syntax options for this including commas, using `MATCH` twice or utilizing the same node for multiple comparisons
		- `MATCH (a:Person)-[:ACTED_IN]->(m:Movie)<-[:DIRECTED]-(d:Person)`
	- We can also use `OPTIONAL MATCH` clauses to get information that may exist
- The `RETURN` keyword is necessary to actually retrieve the data
	- Behaves similarly to `SELECT` in [[SPARQL Basics|SPARQL]]
	- We can return entire nodes, relationships, or only properties of nodes/relationships
	- `RETURN` clauses also support the `DISTINCT` operation
- Filtering on properties can either be done in the `MATCH` statement or using a `WHERE` clause
	- In the `MATCH` statement, we apply the property in the node definition
		- `MATCH(s:Student {name: 'Eddie Jenkins'})`
	- With a `WHERE` clause, we leverage SQL-like syntax between the `MATCH` and `RETURN` statements
		```cypher
		 MATCH (s:Student)
		 WHERE s.name = 'Eddie Jenkins'
		 RETURN s.status
		```
		- `WHERE` clauses are often preferable when complex logic is needed since they support `AND` and `OR` operations
	- Additional filtering operations
		- Range of values: `WHERE 2000 <= m.yearReleased <= 2003`
		- Property existence: `s.advisor IS NOT NULL`
		- Partial string match: `WHERE toLower(s.name) STARTS WITH 'eddie'`
		- List inclusion: `WHERE s.major IN ['Economics', 'Data Science']`
		- <mark style="background: #FFB86CA6;">Graph patterns</mark>: `WHERE NOT EXISTS (s) -[:EMPLOYED_BY]-> (u:University)`
- Style best practices
	- labels named with CamelCase
	- property keys and variables also with camelCase
	- UPPERCASE for Cypher keywords
- To see the query plan we can use the `EXPLAIN` keyword
- To check how many rows would be returned from a query, we use `PROFILE`
- `ORDER BY` lets us change the result return order
	- Ascending by default, but supports the `DESC` keyword
	- Can order by as many properties as we'd like
- `LIMIT` stops the number of results to a chosen count and we can combine this with `SKIP` to ignore the first k results
## Creating, Updating, and Deleting Data
- The `MERGE` operator allows us to add new nodes (if they don't already exist)
	- Example: `MERGE (p:Professor {name: 'Ana Escobar'})`
	- This operator can also be repeated several times in a row for different nodes
	- `MERGE` can also be used to form new relationships between existing nodes. Example:
		```cypher
		  MATCH (p:Person {name: 'Michael Caine' })
		  MATCH (m:Movie {title: 'The Dark Knight' })
		  MERGE (p)-[:ACTED_IN]->(m)
		```
- The `SET` keyword also lets us modify properties and labels of nodes and relationships
	- Be sure to make sure that the match and filtering is specific enough since it will apply to all found nodes
	- We can also say `WITH DISTINCT n SET n.property` to ensure each node is only set once
- The `REMOVE` keyword lets us delete properties
	- Do not remove properties that are used as the [[Data Management & Relational Algebra|primary key]] for a node
- `MERGE` behavior can be customized with the following commands
	- `ON CREATE SET ...` "Only set the property is the node is being created during the query"
	- `ON MATCH SET ...` "Only set the property if the node was already created previously"
- Nodes and relationships can be deleted using the `DELETE` keyword
	- Neo4j will automatically remove relationships for deleted nodes to get rid of orphaned relationships
		- But to ensure that the node and all its relationships are removed, use `DETACH DELTE`
	- This is performed after `MATCH` and `WHERE` clauses, so be cautious to correctly sub-select
- The `REMOVE` keyword lets us take away a label from matched nodes
- Data can also be loaded from source files such as CSV, relational databases, APIs, BI tools, etc
	- This is done using a specified Cypher command. For example,
		- `LOAD CSV [WITH HEADERS' FROM url [AS alias] [FIELDTERMINATOR char]`
		- All data is loaded as strings and must be cast to different data types
			- `toInteger`, `toBoolean`, `toFloat`, `date()`, `datetime()`, `toString()`
	- For large files, we can split the query into multiple [[Programmatic SQL|transactions]] using
		- `CALL{query} IN TRANSACTIONS [OF x ROWS]`
- Unique IDs and constraints
	- Generally uses the syntax
		```cypher
		 CREATE CONSTRAINT [constraint name] [IF NOT EXISTS]
		 FOR (l:NodeLabel)
		 REQUIRE l.propertyName IS UNIQUE
		```
	- We can drop entire constraints across all affected nodes using `DROP CONSTRAINT [constraint_name]`
- We can also modify only the result collected as opposed to the underlying data with updates in the `RETURN` statement
	- `AS` lets us rename fields
	- Calculations of new data can be performed
	- Conditional logic can be applied using `CASE WHEN`
## Data Aggregation
- Aggregation functions like `count()` are placed in the `RETURN` statement