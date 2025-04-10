|   Course Name    |         Topic         |   Professor   |     Date      | Tags |
| :--------------: | :-------------------: | :-----------: | :-----------: | :--: |
| **Semantic Web** | Handling non-RDF data | Fabien Gandon | 04 avril 2025 |      |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/johnny_najjar_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fjohnny%5Fnajjar%5Fdsti%5Finstitute%2FDocuments%2FRecordings%281%29%2FA24%20%2D%20Common%20Link%20%2D%20DS%2DDE%2DDA%2D20250404%5F094713%2DMeeting%20Recording%201%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E51af1486%2Df73d%2D45fc%2Db2a7%2D28958e26f70a)

# Summary
*While RDF is the [[Internet and Web|W3C standard]] for accessing and creating linked data on the sematic web, there are also other protocols which provide for interoperability between other data formats. These protocols transform data sources which come from databases, tabular data, and/or JSON back into RDF data for integration with the RDF data structure and schema.*

# Key Takeaways
1. JSON-LD is both an [[RDF|RDF syntax]] and interpretation method
2. JSON-LD allows for conceptualizing data from JSON APIs
3. Linked Data Platform is not [[SPARQL Basics|SPARQL]], it replaces SPARQL

# Definitions
- Context: Defining prefixes and entity mappings for dataset conversion
- Container: Collections of resources, often homogeneous ones

# Additional Resources
- [Tabular Data Vocabulary](https://www.w3.org/ns/csvw)

# Notes
## RDF to [[Relational Database Management System|RDBMS]]
- R2RML allows for transformation of data from relational databases
- Two transformation types
	- Default: A direct mapping of relational data to RDF
		- Cells of a line are triples with a shared subject
		- Names of columns are names of properties
		- Each cell value creates an object
			- Allows for links between tables
	- Customized: A schema and mapping is provided
		- We can also use the a mapping to directly specify how we would like the table data to be transformed into the graph
## RDFa (Embedded HTML)
- RDFa is RDF embedded in HTML attributes
	- Example: We see a vocabulary, a single resource, and two literal properties
	```html
	<body voacb="http://purl.org/dc/terms/">
		<div resource="http://lib.com/books/0684853949">
			<h2 property="title">The Man Who Mistook His Wife For a Hat</h2>
			<h3 property="creator">Oliver Sacks</h3>
		</div>
	</body8>	
	```
- RDFa is able to be parsed and extracted by an RDF parser
	- Inside of an XML document GRDDL is used for RDF extraction
- A vocabulary and resources are defined for everything within a block
	- However, we can redefine it part of the way through for a specific section of triples
- RDFa allows for [[Existing Vocabularies|Creative Commons Licenses]] to be added to HTML pages
- RDFa is typically how OGP (Online Graph Protocol) code is added
## JSON-LD (JSON for Linked Data)
- JSON-LD allows for the definition of a context which allows for a mapping from a JSON model to an RDF model
	- This can be embedding in a single document or in a separate file which is referenced
- Has specific reserved names
	- `@context`: define short names used in the document
	- `@id`: identify resources with IRIs or blank nodes
	- `@value`: specify the data value of a property
	- `@language`: specify the language for a string or the document
	- `@type`: set the type of a value or a resource
	- `@vocab`: prefix IRI to expand properties and values in @type
	- `@base`: used to set the base IRI
	- `@container`: used to set the default container type for a term
	- `@index`: specify a container is used to index information
	- `@list`: an ordered list of data
	- `@set`: an unordered set of data
	- `@reverse`: express reverse properties
	- `@graph`: indicate a graph
- Example: Using a context to define prefixes
	```json
	{ "@context": {
			"foaf": "http://xmlns.com/foaf/0.1/",
			"xsd": "http://www.w3.org/2001/XMLSchema#
		},
		"@graph": [
			{ "@id": "http://ns.inria.fr/fabien.gandon#me",
				"@type": "foaf:Person", "foaf:age": 40,
				"foaf:birthday": { "@type": "xsd:gMonthDay",
									"@value": "--07-31" },
				"foaf:familyName": { "@value": "Gandon" , "@language": "fr" },
				"foaf:givenName": { "@value": "Fabien" , "@language": "fr" },
				"foaf:homepage": { "@id": "http://fabien.info" },
				"foaf:knows": [ { "@type": "foaf:Person",
								  "foaf:name": "Olivier Corby" } ,
								{ "@type": "foaf:Person",
								  "foaf:name": "Catherine Faron-Zucker"}
							  ]
			  }
		  ]
	  }
	```
## Tabular Data and Metadata (CSV-LD)
- Works similarly to JSON but for CSV or TSV data
- Uses context attachment which, unlike JSON, cannot be embedded into the document
	- Either add “-metadata.json” to the end of the name of the CSV file. OR if one is not available, a "csv-metadata.json" in the same directory
	- The context is a JSON document which uses the <mark style="background: #FFB86CA6;">same reserved names and structure as JSON-LD
- </mark>
## Linked Data Platform (Standard [[Cloud Overview|REST API]] for RDF)
- Standardized HTTP and RDF practices to build clients and servers that create, read, and write Linked Data Resources
- Allows for two kinds of resources - RDF representations and other formats (HTML, images, binary files)
- Container based framework
	- Basic: simple containment vocabulary and access
	- Direct: domain-specific membership assertions
	- Indirect: control the URI of the new domain-specific member resources
- REST API uses the OPTIONS keyword for access to the LDP resources