|   Course Name    |                Topic                |   Professor   |     Date      |     Tags     |
| :--------------: | :---------------------------------: | :-----------: | :-----------: | :----------: |
| **Semantic Web** | Building [[Ontologies\|Ontologies]] | Fabien Gandon | 03 avril 2025 | #GraphTheory |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/johnny_najjar_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fjohnny%5Fnajjar%5Fdsti%5Finstitute%2FDocuments%2FRecordings%281%29%2FA24%20%2D%20Common%20Link%20%2D%20DS%2DDE%2DDA%2D20250403%5F094949%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E398d60a4%2D9862%2D4d86%2Dba30%2D300e621c6eb1)

# Summary
*OWL is a language written in RDF to extend RDFS and allow for more complex writing of schemata/ontologies. OWL is divided into a disjoint set of resources, classes, and properties which all have enhanced definition availability. With OWL, for the first time in RDF-based languages, we are able to fully express union conditions among many other things.*

# Key Takeaways
1. OWL is an extension of RDFS for heavyweight ontologies
2. In OWL, individuals/resources, classes, and properties are disjoint sets (i.e., a URI can only be one of these)

# Definitions
- Web Ontology Language (OWL): Semantic Web language designed to represent rich and complex knowledge about things, groups of things, and relations between things

# Additional Resources
- [OWL Overview (W3C)](https://www.w3.org/OWL/)

# Notes
## OWL Overview
- OWL is a full logic language (it is a type of description logic)
- OWL is a [[Internet and Web|W3C recommendation]]
	- Set at the URI `<http://www.w3.org/2002/07/owl#>` and [[RDF|prefixed]] with `owl:`
	- OWL is written in the [[RDF|turtle RDF syntax]]
- Provides additional primitives to build more complex ontologies with richer definitions of classes/properties
- Can perform even more inferences and draw more conclusions than possible with [[RDFS|RDFS]]
- OWL Capabilities Overview
	 ![[Pasted image 20250407162018.png]]
## OWL Set Operations for Primitive Definitions
- Enumeration (`owl:oneOf`)
	- Declares that a [[RDFS|primitive]] must be one of a list of elements provided
	- Example: `:EyeColor owl:oneOf (:Blue :Green :Brown :Hazel) .`
- Union (`owl:unionOf`)
	- Defines that primitives are the combination of ANY of the elements
	- Instances of a union will also have the `rdf:type` of all constituent classes
		- Only works in the direction of the primitive being defined as both of the classes in the union. No effect on resources defined as a class in the union only
	- Example: `:LegalAgent owl:unionOf (:Person :Group) .`
- Intersection (`owl:intersectionOf`)
	- Specifies that a primitive is the combination of two other classes
	- Adds <mark style="background: #FFB86CA6;">class typing to resources in BOTH directions</mark>
		- A resource which meets the condition of being both intersected classes will <mark style="background: #FFB86CA6;">automatically obtain the type even if it's not explicitly declared</mark>
	- Example: `:Man owl:intersectionOf (:Person :Male) .`
- Complement (`owl:complementOf`)
	- Lets us define the complement of a set
	- CAUTION: Ensure that the primitive and its complement comprise the entire set
	- Example: `:Physical owl:complementOf :Abstract .`
	- <mark style="background: #FFB86CA6;">Complement can be used to define opposites which aren't the complete set) by combining with the intersection operation</mark> and using a [[RDF|blank node]]
		- Example: `:GoodActor owl:intersectionOf ([ owl:complementOf :BadActor ] :Actor) .`
			- This restricts our definition of good actors to people who not only aren't bad actors (which includes non-actors) but also who are actors
- Disjunction (`owl:disjointWith` and `owl:AllDisjointClasses`)
	- Acts more as [[Data Validation (SHACL and OWL)|validation]] for the URIs. System will fail to load if this is violated
		- More powerful as it also ensure <mark style="background: #FFB86CA6;">primitives gained through inference also respect disjunction rules</mark>
	- Simple binary disjunction
		- Specifies that a resource of one class/property cannot be also typed as another
		- Example: `:Sqaure owl:disjointWith :Circle .`
	- Multiple disjoint conditions
		- `AllDisjointClasses` acts as syntactic sugar for applying many `disjointWith` conditions
		- Uses the `owl:members` keyword to specify a collection of disjoint classes
		- Classes are first defined separately, then a blank node is used to create the disjunction
		- Example: Given classes (`:Square, :Circle, and :Triangle`)
			- `[] a owl:AllDisjointClasses ; owl:members (`:Square, :Circle, and :Triangle`) .`
## Equivalence and Difference of Classes and Resources
- Equivalent Classes (`owl:equivalentClass`)
	- Used to define two classes with exactly the same resources
	- Allows us to map other ontologies into our own
	- Example `mySchema:Human owl:equivalentClass foaf:Person .`
- Identical Resources (`owl:sameAs`)
	- Two resources (URIs) which identify <mark style="background: #FFB86CA6;">exactly the same thing</mark>
	- Example: `:EddieJenkins owl:sameAs :EdwardJenkins`
- Different Resources (`owl:differentFrom`)
	- Two resources (URIs) which are known to represent different things
	- Example: `:Good owl:differentFrom :Evil`
## Identification with Keys (`owl:hasKey`)
- Two resources with the same key values are considered the same (`owl:sameAs`)
- A class <mark style="background: #FFB86CA6;">can be defined with multiple different keys</mark>
	- If ANY of the keys are a match, then the URIs are considered the same
- Example: A unique DNA sequence, social security number, or combination of first name, last name, birthdate, and birth place will define a unique person 
	```turtle
	:Person owl:hasKey 
	( :name :firstname :birthdate :birthplace ) , 
	( :socialSecurityNumber ),
	( :hashDNA ) .
	```