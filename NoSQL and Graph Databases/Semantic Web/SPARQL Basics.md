|   Course Name    |         Topic         |   Professor   |     Date     |     Tags     |
| :--------------: | :-------------------: | :-----------: | :----------: | :----------: |
| **Semantic Web** | SPARQL Query Language | Fabien Gandon | 28 mars 2025 | #GraphTheory |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/johnny_najjar_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fjohnny%5Fnajjar%5Fdsti%5Finstitute%2FDocuments%2FRecordings%281%29%2FA24%20%2D%20Common%20Link%20%2D%20DS%2DDE%2DDA%2D20250328%5F094929%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Edeec12ee%2Da426%2D4be0%2Db5d4%2D4ac754e532b0)

# Summary
*SPARQL is query language built on top of RDF using the turtle syntax. It is a complete graph query language with the ability to generate complex queries including data aggregation, null value handling, and union operations. The main clauses in a SPARQL query are select (choose variables to return), where (identify triple patterns to match), and filter (perform logic tests on node/property values.*

# Key Takeaways
1. SPARQL is [[RDF|turtle RDF syntax]] with variables
2. A result is returned for each matching pattern in the graph
3. The `langMatches()` function lets us match all dialects of a language (US vs British English)
4. The `minus` operator ensure the nodes which match the pattern are excluded unlike `filter()` which would still allow a node so long as it can appear for another reason
5. The `not exists` operation does not required shared variables like `minus`, but it is a blocking operation such that if ANY pattern matches, the whole operation fails
6. SPARQL operators are case insensitive, but values and labels are case sensitive

# Definitions
- Access Protocol: How to connect to online resources
- SELECT: Specifies which variables/values to return
- WHERE: Identifies which [[RDF|triples]] (graph patterns) to match
	- Works as a conjunction ("AND")
- Graph Isomorphism: A vertex [[Applications and Compositions of Sets|bijection]] which is both edge-preserving and label-preserving
- FILTER: Constraints which use test functions

# Additional Resources
- [SPARQL Negation (NOT EXISTS and MINUS)](https://jena.apache.org/documentation/query/negation.html)
- [SPARQL Function Reference](https://graphdb.ontotext.com/documentation/10.8/sparql-functions-reference.html)

# Notes
## SPARQL Protocol and RDF Query Language Overview
- Recursive acronym (the "S" used to be for "Simple")
- 3 Key parts: query language, result format, and access protocol (since SPARQL is meant for online resources)
- Turtle with Variables
	- Variables can be any part of the triple (subject, property, or object)
	- Variables are denoted with the `?` or `$` symbols
	- Same shortcuts from Turtle exist in SPARQL as well (recycling of subjects and/or predicates) as well as datatype and language specification
- Since [[RDF|RDF is directed]], resources on different sides of the same relation could be returned twice
	- Example: `?person1 foaf:knows ?person2` $\ne$ `?person2 foaf:knows ?person1`
		- So, if I query all resources with a `foaf:knows` relation between them, I would find both combinations (person1 with person2 / person 2 with person 1)
	- Trick to remove duplicates of [[OWL Property Extensions|symmetric properties]] is to use the `FILTER()` operation
		- Example: `select * where{?person1 foaf:knows: ?person2. filter(?person1 < ?person2)}` would only return one of the pairs
	- This is why the syntax is disambiguous. In [[Cypher Query Language|Cypher]], links can be undirected, so the query language has to provide additional specifications to provide for that unlike SPARQL
## Query Structure
```sparql
# Start with prefix declaration
prefix : <http://example.org/schema#>

# Select statement which determines result "columns"
select variables

# Where statement which identifies triple patterns to match
where{
triples pattern(s)

# Filter conditions (if necessary) to refine triple matches
filter(boolean condition(s))

}
```
- Like turtle, prefixes are defined at the start using the `PREFIX` keyword
- Select allows us to specify the variables we are interested in returning
- Where indicates the specific patterns we want to find
	- These work as a conjunctive "AND" to perform graph isomorphism which <mark style="background: #FFB86CA6;">finds subgraphs with matching patterns</mark>
- Filter lets us further refine the result of our selected triples based on Boolean conditions using test functions
- Most Basic Query: Return all nodes, properties, and objects
	```sparql
	select *
	where{
	# Any node with any predicate/property to any object
	?x ?p ?o
	}
	```
## Result Modifiers
- `*`: Used in conjunction with `SELECT` to <mark style="background: #FFB86CA6;">return all variables referenced within the WHERE clause</mark>
	- Different from [[Basic Querying|SQL SELECT]] which would return all columns present in the table even if not referenced anywhere in the query
- `DISTINCT`: Used in conjunction with `SELECT` to return the unique combination of variables provided
- `ORDER BY`: Stated at the end of the query (before LIMIT) and allows for the ordering of results based on a variable
	- Default is ascending. `DESC` keyword makes it descending
- `LIMIT`: Stated at the end of the query (before OFFSET) to set a maximum number of results to return (provided as an integer)
- `OFFSET`: Stated at the end of the query to skip the first `n` rows (provided as an integer)
- Example: students older than 22 sorted by name. Return only results 21-40
	```sparql
	PREFIX mit: <http://www.mit.edu#>
	PREFIX foaf: <http://xmlns.com/foaf/0.1/>
	
	SELECT * 
	WHERE { 
	?student mit:registeredAt ?x .
	?x foaf:homepage . ?student
	foaf:name ?name .
	?student foaf:age ?age .
	FILTER (?age > 22) 
	}
	ORDER BY ?name
	LIMIT 20
	OFFSET 20
	```
## "OR" Conditions
- By default, all triples in the `WHERE` clause are a conjunction
- However, the `UNION` keyword allows us to combine triple conditions and form an "or"
- Syntactically, each condition is nested within curly brackets and the two conditions are joined with `UNION`
	```sparql
	# Get all customers from website data who puchase or view a given product
	select *
	where {
	?customer a :Customer .
	?product a :Product .
	{?customer schema:buys ?product} union
	{?customer schema:views ?product}
	}
	```
## Null/Unbound Values
- By default, the entire conjunction of the triple patterns must match for a given set of variables to be returned
- SPARQL provides an `OPTIONAL` keyword which allows for specifying unbound conditions
	```sparql
	# This query would only return customers who have an industry
	select ?customer_id ?customer_industry
	where {
	?customer_id a :Customer ;
		schema:hasIndustry ?customer_industry 
	}

	# This query lets us allow customer industry to be possibly unbound
	# Returns ALL customers, but cannot reuse the subject
	select ?customer_id ?customer_industry
	where {
	?customer_id a :Customer .
	optional {?customer_id schema:hasIndustry ?customer_industry} 
	}
	```
- Can also check if a variable is bound or not using the `bound` keyword which returns a Boolean
## Filter Operators
- Comparators: `<, >, =, <=, >=, !=`
- Tests on Variables: `isURI, isBlank, isLiteral, bound`
- Regular Expressions: `regex(?variable, "expression")`
- Get attribute of value: `lang, datatype, str`
- Casting: `xsd:datatype`
	- Uses the [[RDF|XML datatypes]]
- Boolean Operators: `! (not), && (and), || (or)`
- Checking lists of values
	- `IN/NOT IN` operators
		- Simply checks against a flat list of literals
		- part of the `FILTER` statement
	- `VALUES` operator
		- Allows for more complex filtering through pre-defined bindings
		- For example, we can easily check for first and last name combinations with `VALUES`
		- Standalone operator which can accept `UNDEF` for unbound values
		- Example:
			```sparql
			SELECT ?person 
			WHERE { 
			?person :familyName ?name ;
					:firstName ?fname .
			# Build the tuple-pair mapping of values to check
			VALUES (?name ?fname) {
				("Gandon" "Faron") 
				("Fabien" "Catherine") 
				} 
			}
			```
## Additional Functions
- All of these available as of SPARQL 1.1
- `isNumeric(Val) `- test it is a numeric value 
- `coalesce(val,…, val)` - first valid value 
- `IRI(Str)/URI(Str)` - to build an [[Internet and Web|IRI/URI]] from a string 
- `BNODE(ID)` - to build a [[RDF|blank node]] 
- `RAND() `- random value between 0 and 1 
- `ABS(Val)` - absolute value 
- `CEIL(Val), FLOOR(Val), ROUND(Val)` - Ceiling, floor, and rounding
- `NOW()` - today’s date 
- `DAY(Date), HOURS(Date), MINUTES(Date), MONTH(Date), SECONDS(Date), TIMEZONE(Date), TZ(Date), YEAR(Date)` - access different parts of a date 
- `MD5(Val), SHA1(Val), SHA256(Val), SHA384(Val), SHA512(Val)` - hash functions
- `STRDT(value, type)` build a typed literal ex. `STRDT(“42", xsd:integer)=“42"^^xsd:integer` 
- `STRLANG(value, lang)` build a literal with a language ex. `STRLANG("cat", "en")="cat"@en` 
- `CONCAT(lit1,…,litn)` concatenate a list of literal 
- `CONTAINS(lit1,lit2), STRSTARTS(lit1,lit2), STRENDS(lit1,lit2)` to test string inclusion
- `SUBSTR(lit, start [,length])` extract a sub string 
- `ENCODE_FOR_URI (Str)` encodes a string for URI 
- `UCASE (Str), LCASE (Str)` uppercase and lowercase 
- `STRLEN (Str)` length of the string 
- `UUID()` and `STRUUID()` to generate UUID URN or strings 
- `LANG()` returns the language 
- `langMatches(lang,rang)` tests if language matches language‐range (all dialects)
	- `langMatches()` is the preferred way to perform Boolean tests on languages
## Triple Subtraction (`MINUS` and `NOT EXISTS`)
- Normally, triples in the `WHERE` clause are additive
- The `MINUS` keyword allows us to remove any result which has an isomorphic match to the the pattern in the clause
	- It is not enough to simply use `FILTER` because nodes in a graph can (and frequently are) be multi-typed (e.g., `:Eddie a schema:Person, schema:Employee`)
- This operator <mark style="background: #FFB86CA6;">REQUIRES that there is a shared variable</mark> between the triples in the `WHERE` clause and the triples in the `MINUS`
	- If there are none, `MINUS` will have no effect
- The `NOT EXISTS` keyword 
	- Goes inside the `FILTER` operation
	- Will remove
## Aggregation
- Works very similarly to [[Basic Querying|SQL Aggregation]]
- Specified with a `GROUP BY` keyword which comes after `WHERE`
- Aggregation functions
	- `count, sum, min, max, avg, group_concat, and sample`
	- `sample` function gives a random value within the group of the specified variable
- Can filter after aggregate with `having()`
- Not required to group the data to calculate aggregated metrics
- Example: Count of distinct customers within a customer industry
	```sparql
	select ?customer (count(distinct ?other_customer) as ?count)
	where {
	?customer schema:industry ?customer_industry .
	?other_customer schema:industry ?customer_industry . 
	}
	group by ?custoemr
	```