|   Course Name    |         Topic         |   Professor   |     Date      |     Tags     |
| :--------------: | :-------------------: | :-----------: | :-----------: | :----------: |
| **Semantic Web** | SPARQL Query Language | Fabien Gandon | 28 avril 2025 | #GraphTheory |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/johnny_najjar_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fjohnny%5Fnajjar%5Fdsti%5Finstitute%2FDocuments%2FRecordings%281%29%2FA24%20%2D%20Common%20Link%20%2D%20DS%2DDE%2DDA%2D20250328%5F094929%2DMeeting%20Recording%201%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E1178880e%2D61ef%2D4d25%2D8296%2D83a653e9b03f)

# Summary
*The SPARQL Query Language, on top of being a full graph query language, includes functionality to make it particularly useful in an RDF context. Property paths allow for more dynamic relationships between nodes to be found, conditional statements and subqueries allow for complex querying, CRUD operations provide data update and manipulation mechanisms, and most importantly, SPARQL provides a means to not only connect to and access external data natively, but also to execute the query on external compute resources and seamlessly integrate the queried data into the local graph.*

# Key Takeaways
1. Property paths allow for simulating [[Object-Oriented Design|object-oriented]] properties
2. The `CONSTRUCT` keyword does not actually modify the base. The graph is created for viewing but is not loaded
3. When using the `FROM` keyword for named graphs, the graphs used must be specified in the RDF. Graphs cannot be created on-the-fly like SQL views

# Definitions
- `CONSTRUCT`: Generate a graph of a given query to display to the user
- `DESCRIBE`: View the resources and properties attached to a URI
- `SERVICE`: Utilize a remote SPARQL engine for part (or all) of a query

# Additional Resources
- [SPARQL Endpoints List](https://www.wikidata.org/wiki/Wikidata:Lists/SPARQL_endpoints)
- [Understanding SPARQL Endpoint](https://medium.com/virtuoso-blog/what-is-a-sparql-endpoint-and-why-is-it-important-b3c9e6a20a8b)
- [FROM vs FROM NAMED in SPARQL](https://labs.stardog.ai/from-vs-from-named-sparql)
# Notes
## Object-Oriented Design with Property Paths
- These let us define, in the [[SPARQL Basics|WHERE clause]] of a SPARQL query, passes in the graph
	- Properties can become optional or we can specify to look for skips as well
- Sequences (`/`)
	- Let us specify a chain of properties in an explicit order
	- We must define each property and where it falls
	- Example: Friend of a friend - `?x foaf:knows/foaf/knows ?y`
- Alternatives (`|`)
	- Specify a set of properties to search for between two nodes
	- Example: Mother or Father -  `?x (:hasMother | ?hasFather) ?y`
- One or Several (`+`)
	- Checks for all possible lengths of a sequence
	- Example: Friend of a friend of a friend (until there are no friend relations left)
	- CAUTION: This <mark style="background: #FFB86CA6;">can result in combinatorial explosion</mark>
- Zero or Several (`*`)
	- Similar to `+` but does not require a match to be found
- Optional (`?`)
	- The property relation between the nodes need not exist
	- Similar to the [[SPARQL Basics|optional keyword]] but combines with other property paths
	- Example: Specify sequence but don't require second property to be found - `?x foaf:knows/foaf:knows? ?y`
- Reverse (`^`)
	- Look for nodes which are connected by a given property but in the reverse direction
	- Example: Data only provides :hasParent properties but we want to find people who have children - `?x ^:hasParent ?y`
- Connected Otherwise (`!`)
	- Exclude certain relationship types
	- Similar to the [[SPARQL Basics|minus keyword]] but can be chained with other property paths
## Conditional Statements
- The `BIND` keyword assigns values to variables
	- Can be used in either the `SELECT` or `WHERE` statements
	- Commonly used with [[SPARQL Basics|aggregations]] in the `SELECT` statement
	- Paired with `AS` to actually create the variable
	- Example: `select (max(?count) as ?maxCount) ...`
- Conditional statements in SPARQL occur in either the `SELECT` or `WHERE` clause
	- Use the keyword `IF` and follow Excel syntax: `IF(condition, value if true, value if false)`
	- Variables used in the conditional statement must also be defined in the `WHERE` clause
	- In the `WHERE` clause
		- Uses `BIND` to create a new variable based on the conditional statement
		- Can pass the bound variables directly to `FILTER`
	- In the `SELECT` statement
		- Simply wraps parentheses around the `IF` statement
## Subqueries
- The inner query goes within the `WHERE` clause of the outer query
- Subqueries are typically used to get information related to aggregated metrics
	- Example: Name of the oldest person in the database
- To use a result of the subquery in the outer query, the variable name must be in the `SELECT` of the inner query and match the variable name in the outer query
	- A subquery must have its own `SELECT` and `WHERE` statements and the whole subquery should be wrapped in curly brackets
## SPARQL Endpoints
- Many large RDF datasets provide a mechanism through which we can retrieve data and execute relevant portions of a query using their SPARQL engine and compute resources
- To remotely access these endpoints, we use the `SERVICE` keyword inside the `WHERE` clause to indicate which part of the query should be executed on a different server and where
	- We can call `SERVICE` multiple times for different resources in the same query AND blend with local RDF data as well
- This functionality is also useful if there are multiple SPARQL instances/databases being run internally (e.g., different regions/departments)
	- Or useful for <mark style="background: #FFB86CA6;">different rules engine implementations</mark> (materialization vs query rewriting) for different needs
- Results are either returned as a binding (list of all selected values as XML), RDF sub-graphs for each answer, JSON, or CSV/TSV
- Example:
	```sparql
	prefix r: <http://fr.dbpedia.org/resource/>
	prefix p: <http://fr.dbpedia.org/property/> 
	prefix o: <http://dbpedia.org/ontology/> 
	select * 
	where {
	# Execute on the DBPedia SPARQL endpoint with access to the RDF data there
	service <http://fr.dbpedia.org/sparql> {
		r:Auguste p:succ ?s ; o:wife ?w 
		}
	}
	```
## Moving Beyond the `SELECT` Operator / CRUD Operations
- `ASK` keyword can be used to see if a triple pattern (or set of patterns) exists in a dataset
	- Does not return results, simply a true/false value but is more performant
- `DESCRIBE` keyword is used to inspect a URI to see all the properties and related nodes
	- Good for getting a first understanding of how data is setup
	- When accessed with code, response is RDF
- `CONSTRUCT` keyword is a pattern of RDF that we want to create
	- This RDF is NOT materialized in the source dataset but rather is available for viewing or downloading
	- Lets us reformat result of another entity's RDF to match our own
	- Example: Transform MIT students from their schema to future executives in ours
		```sparql
		PREFIX mit: <http://www.mit.edu#>
		PREFIX corp: <http://mycorp.com/schema#>

		# Construct statement - more than just variables. It is a full triple(s)
		CONSTRUCT { ?student rdf:type corp:FuturExecutive . }
		WHERE { ?student rdf:type mit:Student . }
		```
- CRUD Operations
	- `LOAD` adds an entire RDF dataset
	- Single triple entry/deletion
		- `INSERT DATA` and `DELETE DATA` allow for adding or removing a single triple to the dataset
	- Multiple triple entry/deletion
		- `INSERT` and `DELETE` keywords with a `WHERE` clause
			- Must be provided full triples to add
		- Work similarly to construct, but do <mark style="background: #FFB86CA6;">have a material impact on the underlying source database</mark>
		- The `WITH/USING` keyword allows for named graph specification when performing mass updates with `INSERT/DELETE` respectively
	- Additional operations include `CLEAR, DROP, and CREATE`
## RDF Datasets and Named Graphs
- Ability to choose from which named graph (specified by a URI) we want our query to use
- The `FROM` prefix allows us to specify these URIs
	- We can also use prefixes
	-  Patterns outside of `GRAPH` blocks are evaluated against the merge of all graphs listed in `FROM`. <mark style="background: #FFB86CA6;">The active graph is the merge of all such graphs</mark>, it does not change during execution.
- Specify specific part of the `WHERE` clause with named graphs
	- Using the `FROM NAMED` keyword, we can further refine which graph we use in our queries
- Examples:
	```sparql
	PREFIX mit: 
	
	# Will use data from either of the mit data sources - combines the graphs
	SELECT ?student 
	FROM mit:data1
	FROM mit:data2
	WHERE { ?student mit:registeredAt ?x . }
	
	# Also uses data from either data sources, but returns which graph it's from
	# Loops over each graph separately and indepdently
	SELECT ?student ?g
	FROM NAMED mit:data1
	FROM NAMED mit:data2 
	WHERE { GRAPH ?g { ?student mit:registeredAt ?x . } }
	
	# Will ONLY use data from mit:data1 since we specified the graph
	SELECT ?student
	WHERE { GRAPH mit:data1 { ?student mit:registeredAt ?x . } }
	```