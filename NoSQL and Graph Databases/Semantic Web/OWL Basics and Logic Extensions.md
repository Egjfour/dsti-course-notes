|   Course Name    |                Topic                |   Professor   |     Date      |     Tags     |
| :--------------: | :---------------------------------: | :-----------: | :-----------: | :----------: |
| **Semantic Web** | Building [[Ontologies\|Ontologies]] | Fabien Gandon | 03 avril 2025 | #GraphTheory |

[Class Video Link](URL)

# Summary
*A 3-4 sentence description of what was learned in italics*

# Key Takeaways
1. OWL is an extension of RDFS for heavyweight ontologies
2. In OWL, individuals/resources, classes, and properties are disjoint sets (i.e., a URI can only be one of these)

# Definitions
- Term: Definition
	- Practical examples can be added below

# Additional Resources
- Name the hyperlink in brackets then outside the brackets put the URL in parens

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
## Equivalence and Difference of Primitives and Resources