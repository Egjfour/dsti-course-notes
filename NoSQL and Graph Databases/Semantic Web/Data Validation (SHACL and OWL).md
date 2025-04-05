|   Course Name    |      Topic       |   Professor   |          Date           |     Tags     |
| :--------------: | :--------------: | :-----------: | :---------------------: | :----------: |
| **Semantic Web** | Graph Validation | Fabien Gandon | 27 mars & 03 avril 2025 | #GraphTheory |

[Class Video Link 1](https://dstisas-my.sharepoint.com/personal/johnny_najjar_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fjohnny%5Fnajjar%5Fdsti%5Finstitute%2FDocuments%2FRecordings%281%29%2FA24%20%2D%20Common%20Link%20%2D%20DS%2DDE%2DDA%2D20250327%5F094909%2DMeeting%20Recording%201%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E3f415f7b%2D8725%2D4903%2D8a55%2D43b019bfe66c)
[Class Video Link 2](https://dstisas-my.sharepoint.com/personal/johnny_najjar_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fjohnny%5Fnajjar%5Fdsti%5Finstitute%2FDocuments%2FRecordings%281%29%2FA24%20%2D%20Common%20Link%20%2D%20DS%2DDE%2DDA%2D20250403%5F094949%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Eaff8e317%2D0ab7%2D48be%2Db0cc%2D996870a9a787)

# Summary
*A 3-4 sentence description of what was learned in italics*

# Key Takeaways
1. SHACL is written using RDF Turtle
2. Validation with SHACL produces an error report for all rules which are not respected
3. SHACL only validates the data we receive, OWL restrictions and statements validate the [[RDFS|inferences]] made on the data as well

# Definitions
- Node Shape: Constraints about a focus node which must be identified with an IRI
- Property Shape: Constraints about a property and its values for a node (identified with a literal)

# Additional Resources
- [SHACL Documentation](https://www.w3.org/TR/shacl/)

# Notes
## Validation with SHACL (Shapes Constraint Language)
- SHACL is used to check that the <mark style="background: #FFB86CA6;">data we get</mark> respects certain rules
	- A separate file which is loaded with the data
- Defined with a prefix in the RDF Turtle syntax
	- `@prefix sh: <http://www.w3.org/ns/shacl#>`
- SHACL is focused on shapes which is the combination of targets (nodes/properties) and constraints (rules)
	- The constraints are typically built using [[RDF|blank nodes]]
- Targets
	- `sh:targetNode` to directly point to a node
	- `sh:targetClass` for all nodes of a given type
	- `sh:targetSubjectsOf` for all subjects of a property
	- `sh:targetObjectsOf` for all object of a property
- Constraints
	- `sh:datatype` to specify that values must be literals of a given type
	- `sh:nodeKind`: nodes/all property values must be
		- `sh:BlankNode, sh:IRI, sh:Literal, sh:BlankNodeOrIRI, sh:BlankNodeOrLiteral, sh:IRIOrLiteral`
	- `sh:class`: the `rdf:type` of all values/nodes
	- `sh:minCount` and `sh:maxCount` for cardinality constraints
	- `sh:hasValue` to state that at least one of the values of the given predicate must be this
	- `sh:minInclusive, sh:minExclusive, sh:maxInclusive, sh:maxExclusive` fpr tanges of values
	- `sh:equals, sh:disjoint, sh:lessThan, sh:lessThanOrEquals` for constraints between two properties
	- `sh:minLength, sh:maxLength, sh:pattern, sh:languageIn (list), and sh:uniqueLang (T/F)` as constraints on strings
- Severity Levels
	- 3 predefined levels
	- `sh:Violation` (default - most severe)
	- `sh:Warning`
	- `sh:Info`
- Example: Any resource of class `:Author` must have at least one property called `:authorOf`
	```turtle
	@prefix sh: <https://www.w3.org/TR/shacl/>
	
	:AuthorShape a sh:NodeShape ;
		sh:targetClass :Author ;
		sh:property [
		sh:path :authorOf ;
		sh:minCount 1
		] .
	```
