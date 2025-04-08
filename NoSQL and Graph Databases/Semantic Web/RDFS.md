|   Course Name    |                  Topic                  |   Professor   |     Date      |     Tags     |
| :--------------: | :-------------------------------------: | :-----------: | :-----------: | :----------: |
| **Semantic Web** | Constructing [[Ontologies\|Ontologies]] | Fabien Gandon | 02 avril 2025 | #GraphTheory |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/johnny_najjar_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fjohnny%5Fnajjar%5Fdsti%5Finstitute%2FDocuments%2FRecordings%281%29%2FA24%20%2D%20Common%20Link%20%2D%20DS%2DDE%2DDA%2D20250402%5F094818%2DMeeting%20Recording%201%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E56f8e7d4%2Db4c3%2D429f%2Dafcd%2D53c5f308390a)

# Summary
*RDFS is the lightweight schema for introducing inferential capabilities to data. These capabilities apply to both classes and their instances as well as properties. RDFS allows for multi-typing and multiple inheritance. The key difference between how RDFS establishes these object-oriented concepts is that it is property-focused; the signature of a property describes the relation (and the classes on either side of it) not the properties of a given class.*

# Key Takeaways
1. RDFS provides lightweight [[Ontologies|primitives]] to work with lightweight ontologies
2. The `rdfs:` [[RDF|prefix]] lets us state that we will have schematic information in the document
3. Everything in RDFS which is not a property (the classes) is an `rdfs:Resource`
4. RDFS supports both multi-typing and [[Inheritance|multiple inheritance]]
5. Signature inheritance for properties applies to the [[Object-Oriented Design|instances of classes]]
6. Multiple classes in a domain/range of a property are all applied to instances using that. There is no OR for a domain/range in RDFS (see [[OWL Property Extensions|OWL]] for "or")
7. The `rdfs:seeAlso`and `rdfs:isDefinedBy` classes allow for linking
8. Everything - triples, validation, ontologies, and inferences - are all in the graph
9. When the schema and data are both loaded, all additional properties and classes granted through inheritance and signatures are materialized in the graph (for most engines)
10. [[Data Validation (SHACL and OWL)|SHACL validation]] applies to both classes and subclasses

# Definitions
- Signature Inheritance: Definition
	- A `:hasFather` relation having a range of `:Male` would mean that any instances which are the object of a `:hasFather` relation becomes `rdf:type :Male` even if it wasn't explicitly defined
- Type Propagation: An instance of a subclass is also an instance of the parent class
- Transitivity of Subsumption: A subclass "chain" (subclass of a subclass) retains the subclass property for all comparisons of all levels of the chain  
	- IF `c2 rdfs:subClassOf c1` AND `c3 rdfs:subClassOf c2` THEN `c3 rdfs:subClassOf c1`
 
# Additional Resources
- [RDFS Documentation (W3C)](https://www.w3.org/TR/rdf-schema/)

# Notes
## RDFS Language
- [[RDF|Turtle-based]] language with primitives for lightweight ontologies
	- Since RDFS is written in RDF, RDFS schemata can be queried with [[SPARQL Basics|SPARQL]]
- Can define relations between resources, their signatures, and <mark style="background: #FFB86CA6;">organize a hierarchy</mark>
- RDFS is what allows us to move beyond simple graph matching and actually apply inference
- Adding `@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#>` indicates that the document contains schematic information
	- We can also reference other vocabularies as prefixes and combine them
- RDFS is a <mark style="background: #FFB86CA6;">schema to describe schemas</mark>
## RDFS Classes
- All classes inherit from `rdfs:Resource`
- RDFS also makes use of the available classes in base RDF
	- Example:  `rdf:Property` vs `rdfs:Class`
 ![[Pasted image 20250407100404.png]]
- RDFS supports multi-typing and multiple inheritance
	- This is defined using set semantics
	- In the example below, a `voc:SecretReport` is both a `voc:InternalDoc` and a `voc:Report` which are all subclasses of `voc:Document`
	![[Pasted image 20250407100850.png]]
- Class Semantics
	- Type propagation exists
	- Subclasses are reflexive (a class is a subclass of itself)
	- The `rdfs:subClassOf` is transitive
## RDFS Properties
- All RDFS properties inherit from `rdf:Property` which inherits from `rdfs:Resource`
 ![[Pasted image 20250407100541.png]]
- Similar to classes, RDFS properties are organized using set semantics and support multi-typing and multiple inheritance
- RDFS properties are also support (like classes)
	- Type propagation
	- Reflexivity
	- Transitivity of the `rdfs:subPropertyOf` relation
- Property Signature
	- Contrary to [[Object-Oriented Design|OOP]], <mark style="background: #FFB86CA6;">RDFS defines a property in terms of classes of resources to which it applies</mark> versus defining a class in terms of properties possessed by its instances
	- The signature is comprised of a domain (departure space) and range (arrival space)
		- Set using the `rdfs:domain` and `rdfs:range` properties
	- Multiple domains and ranges are supported
		- <mark style="background: #FFB86CA6;">The effective domain/range is the intersection of declared domain/range and domains/ranges of super properties</mark>
			- Signature inheritance exists for sub-properties
	- Any object used on either side of a property will become an instance of all relevant classes for the domain/range of that property
		- IF `p rdfs:domain d` AND `x p y` THEN `x rdf:type d`
		- IF `p rdfs:domain d` AND `x p y` THEN `x rdf:type d`
		- Example:
		 ![[Pasted image 20250407102412.png]]
## RDFS Labels and Comments
- Labels (`rdfs:label`)
	- Resources (classes and properties) can have one or more labels in one or more languages (designated with [[RDF|language codes]])
	- These are simply text attached to a resource to help us identify its use and meaning
	- Tend to be relatively short to allow for querying
- Comments (`rdfs:comment`)
	- Resources (classes and properties) can also have comments in one or more languages
	- Comments provide definitions/explanations in natural language and tend to be longer
## RDFS Links Between Resources
- `rdfs:seeAlso` indicates a resource which might provide additional information
	- Example: `:Man a rdfs:Class ; rdfs:seeAlso :Woman .`
- `rdfs:isDefinedBy` indicates a resource defining the subject
	- Example: `:Man a rdfs:Class ; rdfs:isDefinedBy <http://my.onto> .`