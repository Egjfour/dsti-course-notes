|         Course Name          |       Topic        | Professor |     Date      |       Tags       |
| :--------------------------: | :----------------: | :-------: | :-----------: | :--------------: |
| **Warm Up: Data Management** | Relational Algebra | Sebastien | 18 April 2023 | #Data_Management |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/ted_codd_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fted%5Fcodd%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FS24%2DWarmUp%20%2D%20One%2DTime%2DLink%2D20240418%5F105356%2DMeeting%20Recording%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0%3D&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0=&ga=1)

# Summary
*Early data modeling schemes relied heavily on arrays and linked lists to store and query information. In the 70s, Ted Codd looked at this topic through the lens of set theory and developed the relational model. This model is all about finding functional dependencies among sets of attributes*

# Key Takeaways
1. Prior to relational models, data was primarily organized into hierarchical or navigational database systems
2. In relational databases, the only goal is to find functional dependencies in the data dictionary
3. A data dictionary has no data structure and is not interested in design or technical details
4. The result of **any** query is a table in memory even if there is only one row and one column in the result set
5. Any SQL query is converted into a query plan and then passed to an optimizer to identify which plan (among many) is the best

# Definitions
- Data Dictionary: A list of attributes
- Functional Dependency: For all elements in one attribute, there exists one and only one of another attribute
	- Attributes of a customer master are functionally dependent on the Customer ID
- Navigational: A storage and querying method based on mathematical graphs that heavily employs linked lists
- Hierarchical: A storage and querying method where data is arranged as objects (like a tree)
- Primary Key (underlined): A <mark style="background: #FFB86CA6;">uniquely-valued</mark> attribute which is the functional dependency of the other attributes on a table and does not contain the [[Logic and Set Theory|empty set]]
- Foreign Keys (#): A property that is functionally dependent on another property while serving as a primary key itself

# Additional Resources
- [Relational Algebra Basics (Medium)](https://medium.com/@GeneHFang/relational-algebra-union-difference-and-join-cd9cfea8eec0#id_token=eyJhbGciOiJSUzI1NiIsImtpZCI6IjZjZTExYWVjZjllYjE0MDI0YTQ0YmJmZDFiY2Y4YjMyYTEyMjg3ZmEiLCJ0eXAiOiJKV1QifQ.eyJpc3MiOiJodHRwczovL2FjY291bnRzLmdvb2dsZS5jb20iLCJhenAiOiIyMTYyOTYwMzU4MzQtazFrNnFlMDYwczJ0cDJhMmphbTRsamRjbXMwMHN0dGcuYXBwcy5nb29nbGV1c2VyY29udGVudC5jb20iLCJhdWQiOiIyMTYyOTYwMzU4MzQtazFrNnFlMDYwczJ0cDJhMmphbTRsamRjbXMwMHN0dGcuYXBwcy5nb29nbGV1c2VyY29udGVudC5jb20iLCJzdWIiOiIxMTU4OTg5OTM2NTAwMTg0NDA3OTkiLCJoZCI6ImpjdS5lZHUiLCJlbWFpbCI6ImVqZW5raW5zMjBAamN1LmVkdSIsImVtYWlsX3ZlcmlmaWVkIjp0cnVlLCJuYmYiOjE3MTM1MTk3NDAsIm5hbWUiOiJFZHdhcmQgSmVua2lucyIsInBpY3R1cmUiOiJodHRwczovL2xoMy5nb29nbGV1c2VyY29udGVudC5jb20vYS9BQ2c4b2NJakFwU3hITFJ6SkVfYV9SdThFOEx5c1Z6TG4wNEJkM3BzVGZsUVB6cGMtXzg1TXc9czk2LWMiLCJnaXZlbl9uYW1lIjoiRWR3YXJkIiwiZmFtaWx5X25hbWUiOiJKZW5raW5zIiwiaWF0IjoxNzEzNTIwMDQwLCJleHAiOjE3MTM1MjM2NDAsImp0aSI6ImFhZjZkYjM0MmY5N2RiNzVlNzkwYzQ4ODk4M2VmMGEzNzIxNjAxNDIifQ.YHOBF6vCVtOt5RlfcGaFu8nGbQhKHm_E0yvLLg-rbBqxCxh_4bvMP8MSMrcGDm81mrbrflAGLOfvjccmtaAcp6i5Qaak4mGpfBHkdt0c8efdOJMnxDTI12mvBjczwSFJHAB1ZUVbFltasFAPoFl7xsuiPAUQ3qT_5r17qznP6GNZqlsk7g-oMpBAz_NJDxZ4xs4yHJLhenRImyyZAdK1Ji7cFMbxPclUnVqO3xZZAzIPUe7Bi9YFoMviXLQmTGfCw2zV-ATFTQRXP_2eONFYMuJMtrUbl9df9SzZc1R34xTTYNUOlVNRLLp1Cg4lcJdQV8efm9LK8Ff0A7H6MHiklg)
- [Detailed Relational Algebra (Wiki)](https://en.wikipedia.org/wiki/Relational_algebra#%CE%B8-join_and_equijoin)
- ["A Relation Model of Data for Large Shared Data Banks"](https://www.seas.upenn.edu/~zives/03f/cis550/codd.pdf)

# Notes
## Early Data Modeling
- Started in the early 60s as binary files using the language Data Structures in Cobal
	- Each release meant having to recode everything. No cross-system portability
	- Had to find the "right" structures
- Database systems were then created as a dedicated storage and querying space
	- Navigational (graph based) and hierarchical (object/tree based) were the most common
	- Still lacked portability and had no known guidelines to producing the data model
- Relational algebra emerged in the 70s as a mathematical method of expressing data
	- Developed alongside the redefinition of math concepts into set theory
	- Relies on the notion of <mark style="background: #FFB86CA6;">functional dependencies</mark> which are defined as:
$$
\forall u \in \Omega(CustID)\:\: \exists!\: v \in \Omega (CustName)
$$
*For all elements belonging to the universe of CustID, there exists one and only one CustName*
## Building a Relational Data Model
- Relational data models are simply about finding and leveraging functional dependencies
	- This works because these are generally rare and their contraposition is even more rare
	- Begin by identifying all elementary functional dependencies
		- Containing only one attribute
	- If there are any attributes with no elementary relationships, then move into non-elementary relationships where the FD is comprised of multiple attributes
- These relationships ultimately create 2 important values
	- Primary Keys: these are the uniquely-values attributes that provide a functional dependency for all other attributes in the table
		- A primary key MUST be unique and not null
	- Foreign Keys: These are an attribute on one table that is a foreign key on another
		- They do NOT have to meet the primary key constraints
## Querying (A Model and Method)
- Ultimately, the relation model is expressed as an algebra over sets
	- Uses all standard operators of set theory
- <mark style="background: #FFB86CA6;">Introduces 3 new operations as well</mark>
	- Projection ($\pi$): Cuts table vertically (grabs entire columns)
		- "SELECT" statement in SQL
	- Selection ($\sigma$): Cuts table horizontally (grabs sets of rows from table)
		- "WHERE" clause(s) in SQL
	- Join ($\Join$): Specifically a "Natural Join" when the symbol is by itself in which all columns with matching names are checked for equality. Can specify other join types as well
- Query Plans
	- In SQL code, the query provided by the user is converted to relational algebra operands
	- The query planner software also has an optimizer to choose the best query
	- The <mark style="background: #FFB86CA6;">optimizer chooses the best plan based on the minimization of these values </mark>in order
		- Input/Output with Storage
		- RAM Usage
		- Compute Resources
	- The optimizer identifies the best plan using metadata about the tables' structure, content, size, etc 
		- This is stored in the information schema
		- These statistics have to be recollected at a set interval