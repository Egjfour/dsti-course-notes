|   Course Name   |                    Topic                    |   Professor   |     Date      |     Tags     |
| :-------------: | :-----------------------------------------: | :-----------: | :-----------: | :----------: |
| **Sematic Web** | Extensive [[Ontologies\|Ontology]] Building | Fabien Gandon | 03 avril 2025 | #GraphTheory |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/johnny_najjar_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fjohnny%5Fnajjar%5Fdsti%5Finstitute%2FDocuments%2FRecordings%281%29%2FA24%20%2D%20Common%20Link%20%2D%20DS%2DDE%2DDA%2D20250403%5F094949%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E398d60a4%2D9862%2D4d86%2Dba30%2D300e621c6eb1)

# Summary
*As the classes which are in the domain and range of a property are how [[RDFS|RDFS defines objects]], OWL provides for extensive ontology building with properties. Many of the functionality for defining classes exists, but OWL also allows for more propagation in the dataset with things like symmetric and inverse properties as well as functional properties and property chains.*

# Key Takeaways
1. Annotation properties have no impact on inference
2. Inverse properties, typically, should have inverse [[RDFS|signatures]]
3. A property chain can be as big as we want but the entire chain must be found to be considered a match
4. For functional (and inverse functional) properties, the system will state that two resource are identical ($\textrm{x R y \& x R z} \Rightarrow y = x$)

# Definitions
- Property Chain: The chaining of a specific order of properties to define a relationship (if x has y has z, then x has z)
	- A relation `:hasUncle` defined as resource `?x a :Person` with a `:hasParent` relation to `?y a :Parent` where `?y :hasBrother ?z`. The relation `?x :hasUncle ?z` is formed 

# Additional Resources
- [Inverse Functional Properties Discussion (W3C)](https://www.w3.org/wiki/InverseFunctionalProperty)

# Notes
## Basic Property Type Extensions
- Object Property (`owl:ObjectProperty`)
	- Dictates that a relation is only between resources for both the subject and object
	- Example: `hasParent(#thomas, #stephan)`
- Datatype Property
	- The object of a relation is a literal value which may or may not be [[RDF|typed]]
		- Note that the <mark style="background: #FFB86CA6;">subject</mark>/[[RDFS|domain]] <mark style="background: #FFB86CA6;">of a property must always be a resource</mark>
	- Example: `hasAge(#thomas, 16^^xsd:integer)`
- Annotation Property (`owl:AnnotationProperty`)
	- Used for documentation and extensions
	- Ignored in inferences
- Symmetry (`owl:SymmetricProperty`) and Asymmetry (`owl:AsymmetricProperty`)
	- Symmetry will augment the graph to make sure the relation exists in both directions
		- Example: `?x :hasFriend ?y` would generate `?y :hasFriend ?x`
	- Asymmetry is more of a validation check. The system will throw an error an asymmetric property is found in both directions between two nodes
		- Example: `:hasChild a owl:AsymmetricProperty .`
- Inverse Property `owl:inverseOf`
	- Symmetric properties are just syntactic sugar for inverse properties on themselves
	- Inverse properties are the more general case where we have relations that exist simultaneously and inversely
	- Example: `:hasChild owl:inverseOf :hasParent .`
	- This will construct the inverse relations in the underlying graph during inference
- Transitive Properties (`owl:TransitiveProperty`)
	- Transitive properties are propagated from peer-to-peer in an endless chain
	- Example: `:hasAncestor a owl:TransitiveProperty .`
	- <mark style="background: #FFB86CA6;">Constructs the relationship between all nodes at all levels in the peer propagation</mark>
- Disjunction (`owl:propertyDisjointWith`)
	- Works exactly like the `owl:disjointWith` [[OWL Logic and Class Extensions|method for classes]]
	- More of a validation check - does not propagate new properties
	- Example: `:hasChild owl:propertyDisjointWith :hasParent .`
- Reflexivity (`owl:ReflexiveProperty`) and Irreflexivity (`owl:IrreflexiveProperty`)
	- A property which links individuals to themselves is reflexive
	- Example: `:sameFamilyAs a owl:RelexiveProperty .`
	- Like with asymmetry, irreflexivity does not propagate new properties through inference
		- Example: `:hasParent a owl:IrreflexiveProperty .`
## Advanced Property Type Extensions
- Property Chain (`owl:propertyChainAxiom`)
	- Used to define a property as a [[SPARQL Advanced|sequence]] of other properties
	- Can use as many properties as desired in the chain, but the entire chain must match
	- Property chains are useful because any matching pattern in the graph will add the new property defined by the chain
	- Example: `:hasUncle owl:propertyChainAxiom (:hasParent :hasBrother)`
- Functional Properties (`owl:FunctionalProperty`)
	- A relation for which a resource can only have one resource value
	- If `?x :property ?y and ?x :property ?z`, then `?y = ?z` since the <mark style="background: #FFB86CA6;">input to the function is the same</mark>
	- Example: `:biologicalMother a owl:FunctionalProperty .`
	- Caution: This will cause resources to become treated with the [[OWL Logic and Class Extensions|owl:sameAs]] property
- Inverse Functional Properties (`owl:InverseFunctionalProperty`)
	- Similar implication as the functional property but in the reverse order
	-  If `?x :property ?y and ?z :property ?y`, then `?x = ?z` since the same input maps to the same output - `?y`