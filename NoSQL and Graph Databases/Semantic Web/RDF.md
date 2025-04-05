|   Course Name    |           Topic            |   Professor   |      Date       |     Tags     |
| :--------------: | :------------------------: | :-----------: | :-------------: | :----------: |
| **Semantic Web** | Web Data Language Standard | Fabien Gandon | 26-27 mars 2025 | #GraphTheory |

[Class Video Link 1](https://dstisas-my.sharepoint.com/personal/johnny_najjar_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fjohnny%5Fnajjar%5Fdsti%5Finstitute%2FDocuments%2FRecordings%281%29%2FA24%20%2D%20Common%20Link%20%2D%20DS%2DDE%2DDA%2D20250326%5F095027%2DMeeting%20Recording%201%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Ea87de534%2D3ad4%2D4417%2Dbdc7%2Da8664e1937cd)
[Class Video Link 2](https://learn.dsti.institute/mod/url/view.php?id=23681)

# Summary
*The resource description framework (RDF) is the [[Internet and Web|standard]] which allows for communication and referencing of resources across domains on the web. There are many syntaxes for RDF, though Turtle is the most concise and easiest for a human to read. RDF is based on triples which define the individual components of the directed, labeled, multigraph which lies beneath.*

# Key Takeaways
1. RDF is a triple-based model: subject, property, and object
2. Triples are the atoms of the RDF model. Nothing is smaller
3. IRIs are used where they exist for interoperability (else are strings)
4. Values of properties can be either URIs or literals
5. The Turtle RDF language allows for the re-use of a subject `(;)` or a subject-property `(,)` combination
6. RDF graphs are serialized as [[Internet and Web|XML]] which is a tree-based structure
7. Blank/Anonymous nodes can exist if a URI is unknown or for decomposition of complex values
8. RDF is a monotonous logic - what is true and inferred now remains that way as new statements are added to the graph

# Definitions
- Resource Description Framework (RDF): Standard graph model linking descriptions of [[Internet and Web|resources]]
- Multi-Graph: Several arcs/edges between vertices/nodes
- Namespace: Set of names used to identify and refer to objects of various kinds
	- Declared by prefixes in RDF to specify the constant part of a URI for a group of resources
- Prefix: A local shortcut to declare a namespace in an RDF file
- Qualified Names: Prefix + ":" + Local Name
- Bag: Unordered group of elements
- Reification: Allow for the naming of triples using a URI
	- Replaced by name graph in RDF 1.1

# Additional Resources
- [RDF Validator](https://www.w3.org/RDF/Validator/)
- [Linked Data Extension (VS Code)](https://marketplace.visualstudio.com/items?itemName=Elsevier.linked-data)
- [XML Datatypes](https://www.ibm.com/docs/en/bpm/8.5.6?topic=support-supported-xml-schema-data-types)
- [ISO Language Codes](https://www.andiamo.co.uk/resources/iso-language-codes/)

# Notes
## Resource Description Framework (RDF) Overview
- Elements
	- Resource: has a URI
	- Description: Comprised of attributes, features, and relations
	- <mark style="background: #FFB86CA6;">Framework</mark>: Made up of a model, languages, and descriptors
- This is a triple model built on a directed, labeled, multi-graph
	- Similar to a [[Internet and Web|knowledge graph]]
- There are many different syntaxes for RDF
	- ex: XML, Turtle, TriG, N-Triples, N-Quads, JSON, RDFa
		- N-Triples is a simple and minimalistic syntax but very verbose
			- Lines of subject property object with a `.` to separate
			- URIs go in-between angle brakcets `<...>`
			- Literal values between double quotes
	- Translation tools can go from one to another since it is a precise and disambiguous language (Linked Data Extension in VS Code can translate)
	- Less verbose syntaxes (like Turtle) allow for namespaces, prefixes, and bases
		- In turtle, declared with `@prefix <URI>`
		- Bases can either be declared using `@base` or simply `:`
			- ex: `: <http://inria.fr/data>` would declare that as the base
- RDF is a subset of first-order logic
	- Only includes binary predicates/properties
	- Allows for existential quantifications and conjunctions
	- Has no disjunction ("or" statements), negation, or universal quantification
- RDF is an <mark style="background: #FFB86CA6;">extensible vocabulary</mark> based on URIs
	- It can be used by anyone to discuss anything
## Turtle Syntax for RDF
- Considered the most human-friendly and readable
- Starts with declaring namespaces and prefixes at the top of the file so we can use qualified names in our actual data/schema definitions
- Comments use the `#` character and MUST live outside a URI
- Style conventions
	- ClassName as upper camel case
	- propertyName as lower camel case
	- individual_name as snake case
- Supports XML data type declaration and ISO language codes
	- XML Datatype declaration done using...
		- `@prefix xsd:<http://www.w3.org/2001/XMLSchema#> .`
		- The character `^^`
	- ISO language codes are defined for strings using the `@` character after 
		- Literals with and without language codes are disjoint ("Eddie" $\ne$ "Eddie"@en)
- Turtle offers syntactic sugar for `rdf:type` using simply `a`
	- Example: `:INSIGHT2PROFIT a :Company` == `:INSIGHT2PROFIT rdf:type :Company`
- With turtle we can <mark style="background: #FFB86CA6;">create many triples using the same subject or same subject-predicate</mark>
	- Same subject but different predicates is separated with a semi-colon
		- Example `:Eddie a schema:Person; schema:name "Eddie"@en .`
			- Creates two triples with `:Eddie` as the subject. One with property `rdf:type` and another with `schema:name`
	- Same subject and predicate/property is separated with a comma
		- Example: `:Eddie a schema:Person, schema:Man .`
			- Creates two triples both with subject `:Eddie` and property `rdf:type` but with different values (`schema:Person` and `schema:Man`)
## RDF XML Syntax (Historical)
- Typically, RDF is no longer written/maintained for humans in XML. Turtle is preferred
	- Some older sources will only provide the XML
- RDF graphs are serialized as XML which follows a tree-based structure
	```xml
	<a>
		<b>
			<c>
			</c>
		</b>
	</a>
	```
	- The above XML represents the following graph
		 ![[Pasted image 20250405154423.png]]
- Namespaces exist in RDF XML as well as well as bases
	- Uses `xml:base="{uri}"` as the mechanism
- Like Turtle, we can reuse subjects. In XML, this simply means having multiple tags inside a given graph
	- This graph should begin with `<rdf:Description rdf:about="{URI}">` then put any other tags and relations
	 ![[Pasted image 20250405154931.png]]
- Main keywords are `rdf:Description, rdf:about, and rdf:resource`
	- `rdf:id` also exists, but automatically places a `#` and should, therefore, not be used
- XML entities may also be used for variable declaration
## Blank Nodes
- Blank/Anonymous nodes let us specify existential quantification
	- $\exists$ resource such that ... condition(s)
	- These nodes do not provide a URI or name
		- We can mention them using `_:tempId`
			- Lets us assign more attributes by serializing
	- Example: defining complex values like a weight with a unit of measure
		 ![[Pasted image 20250405160305.png]]
- Turtle syntax
	- Uses <mark style="background: #FFB86CA6;">square brackets to signify</mark>
	```turtle
	<http://example.com/people#Eddie> :hasWeight [ 
	:weightValue 180; 
	:uom "pounds" ] . 
	```
- RDF XML syntax
	- Simply an `rdf:Description` which does not specify an `about`
## Handling Resources with Many Elements
- Bags: unordered groups of elements
	- Defined using a blank node and specifying a resource of `rdf:type rdf:Bag`
- Sequences: ordered group of resources or literals
	- Defined as a `contains` property, the object of which is a blank node
- Alternatives: lists which require that we choose at most one value for the property
	- Defined as an `rdf:type` within a blank node as the object of whichever property is being targeted
		```turtle
		<#book> schema:title [
		a rdf:Alt ; rdf:_1 "Le Petit Prince"@fr ; rdf:_2 "The Little Prince"@en
		] .
		```
- Collections: <mark style="background: #FFB86CA6;">exhaustive and ordered list</mark>
	- Cannot add or remove elements to the list
	- Declared using the `rdf:dividedIn` property
		- Provides the ordered list of URIs as the object
	  ```turtle
		<#week> dividedIn (<#MMonday> <#Tuesday> <#Wednesday> <#Thursday>
		<#Friday> <#Saturday>)
		```
	- The first element of the list is identified using `rdf:first` and the rest are accessed using `rdf:rest`
		- Looping through collection elements is generally a recursive process
## Naming Triples
- Previously (now deprecated) reification allowed us to attach an `rdf:nodeID` to a triple to identify it
	- Useful for traceability of triples
- Now, name graph replaces this functionality as of RDF 1.1
- Name Graph allows for modularization into subgraphs and lets us place attributes on those subgraphs
	- Extends N-triples to N-quads and Turtle to TriG
		- N-quads asks for a 4th parameter: the graph URI
		- TriG introduces a `GRAPH` keyword