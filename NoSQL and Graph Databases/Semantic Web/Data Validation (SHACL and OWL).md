|   Course Name    |      Topic       |   Professor   |          Date           |     Tags     |
| :--------------: | :--------------: | :-----------: | :---------------------: | :----------: |
| **Semantic Web** | Graph Validation | Fabien Gandon | 27 mars & 03 avril 2025 | #GraphTheory |

[Class Video Link 1](https://dstisas-my.sharepoint.com/personal/johnny_najjar_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fjohnny%5Fnajjar%5Fdsti%5Finstitute%2FDocuments%2FRecordings%281%29%2FA24%20%2D%20Common%20Link%20%2D%20DS%2DDE%2DDA%2D20250327%5F094909%2DMeeting%20Recording%201%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E3f415f7b%2D8725%2D4903%2D8a55%2D43b019bfe66c)
[Class Video Link 2](https://dstisas-my.sharepoint.com/personal/johnny_najjar_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fjohnny%5Fnajjar%5Fdsti%5Finstitute%2FDocuments%2FRecordings%281%29%2FA24%20%2D%20Common%20Link%20%2D%20DS%2DDE%2DDA%2D20250403%5F094949%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Eaff8e317%2D0ab7%2D48be%2Db0cc%2D996870a9a787)

# Summary
*Data and schema validation is done with SHACL and functionality within OWL to ensure data integrity. This is especially important as ontologies become complex with many inferences generating a lot of possible unintended consequences.*

# Key Takeaways
1. SHACL is written using RDF Turtle
2. Validation with SHACL produces an error report for all rules which are not respected
3. SHACL only validates the data we receive, OWL restrictions and statements validate the [[RDFS|inferences]] made on the data as well

# Definitions
- Node Shape: Constraints about a focus node which must be identified with an IRI
- Property Shape: Constraints about a property and its values for a node (identified with a literal)
- OWL Profile: A subset of OWL primitives which describe a level of expressivity for inference

# Additional Resources
- [SHACL Documentation](https://www.w3.org/TR/shacl/)
- [OWL Profile Explanations (W3C)](https://www.w3.org/2007/OWL/wiki/Profile_Explanations)

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
## Validation with OWL
- Many of the extensions for [[OWL Logic and Class Extensions|classes]] and [[OWL Property Extensions|properties]] act as validation and will cause the inference engine to fail to load if they are violated
	- Disjunction, asymmetry, object and datatype properties, `differentFrom`, etc
- OWL also provides for defining restrictions on which specific classes can be used for different properties
	- Specifying that all values must be part of a certain class (`owl:allValuesFrom`)
		```turtle
		# We define a restriction on the class herbivore such that every resource
		# an instance of class herbivore has an eats property with must be of
		# class plant
		:Herbivore a owl:Class ; 
			rdfs:subClassOf :Animal, 
				[ a owl:Restriction ;
					owl:onProperty :eats;
					owl:allValuesFrom :Plant ] .
		```
	- We can also use the `owl:someValuesFrom` restriction to state that only some values must be from a certain class
		- Example: Defining a class of sporty people who must have a hobby property with a resource of type sport
	- Restrictions can also be imposed to account for exact values (uses [[RDFS|subclassing from RDFS]])
		- Example: Bikes must have two wheels
		  ```turtle
			:Bike rdfs:subClassOf 
			[ a owl:Restriction ;
			 owl:onProperty :nbWheels ;
			 owl:hasValue "2" ] .
			```
	- Self restrictions impose that instances of a class have/don't have themselves as a property value
		- Example: Narcissitic people must love themselves
			```turtle
			ex:NarcisticPerson rdfs:subClassOf 
			[ a owl:Restriction ;
				 owl:onProperty ex:love ;
				 owl:hasSelf true ] .
			```
	- Cardinality restrictions specify how many times a property may be used for a given subject with different values
		- Provides for minimum, maximum, and exact cardinality constraints
		- Also uses `rdfs:subclassOf` to define
	- Cardinality can also be qualified which defines how many times a property may be used with <mark style="background: #FFB86CA6;">values of a specific type</mark> for the same subject
		- Example: Humans can only have one biological parent who is a male
			```turtle
			:Human a rdfs:subClassOf 
			[ a owl:Restriction ;
				owl:onClass :Male ;
				owl:onProperty :hasBiologicalParent ;
				owl:qualifiedCardinality "1" ] .
			```
## OWL Profiles
- Profiles are subsets of the OWL primitives
- The choice of profile is a choice in the level of expressivity
	- There is a tradeoff with expressivity and complexity of inferences
	- More complex = longer computation time
- OWL 1 Profiles
	- Lite : essentially for lightweight hierarchies. 
	- DL : more complex ontologies but complete reasoning. 
	- Full : maximum expressivity but incomplete reasoning
- OWL 2 Profiles
	- EL: large numbers of properties and/or classes and polynomial time. 
	- QL: large volumes of instance data, and conjunctive query answering using conventional relational database in LOGSPACE 
	- RL: scalable reasoning without sacrificing too much expressive power using rule‐based reasoning in polynomial time 
	- DL: the most expressive with complete reasoning
		- Not supported in Corese app
