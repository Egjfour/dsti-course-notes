|   Course Name    |  Topic   |   Professor   |     Date      |     Tags     |
| :--------------: | :------: | :-----------: | :-----------: | :----------: |
| **Semantic Web** | Schemata | Fabien Gandon | 02 avril 2025 | #GraphTheory |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/johnny_najjar_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fjohnny%5Fnajjar%5Fdsti%5Finstitute%2FDocuments%2FRecordings%281%29%2FA24%20%2D%20Common%20Link%20%2D%20DS%2DDE%2DDA%2D20250402%5F094818%2DMeeting%20Recording%2Emp4&ga=1)

# Summary
*Ontologies are a formal method for describing the basic facts of the universe for which our application is concerned. Ontologies create interoperability through reuse among systems and allow for encoding of specific knowledge through rules, constraints, and explanations into an inference engine.*

# Key Takeaways
1. A shared ontology between AI systems provides inference and interoperability
2. Ontologies are made up of general background knowledge which is true in ANY context
3. There is a trade-off between coverage and specificity/granularity in an ontology
4. Building an ontology requires a modeling domain, a domain expert, and scenarios
5. In a hierarchy, a rigid class can never be below an anti-rigid class

# Definitions
- Ontology: Creating interoperability for AI systems by giving an explicit partial account of a conceptualization
	- Example: Novels are a type of Book and should be treated similarly
- Sign: An entity that <mark style="background: #FFB86CA6;">represents</mark> another entity for an agent
- Notion: A thought formed in the mind which structures knowledge/perceptions of the world
- Concept: A notion, expressed by a term/sign, which represents a group of objects/beings which share characteristics
- Relation: Notion of an association/link between concepts expressed by a sign
- Signature of a Relation: The set of concepts which can be linked by a given relation
	- This constraint is a characteristic of the relation which participates in its intension
- Extension: ALL of the individual instances of a concept/relation
- Intension: The characteristics/attributes of a concept/relation
- Primitive: A basic, irreducible concept or relation that forms the foundation upon which more complex ontological structures and reasoning processes are built
	- Human, Animal, Building, etc.
- Coverage: Extent to which primitives in an application are covered by an ontology
- Specificity: Extent to which primitives are uniquely identified
- Granularity: Extent to which primitives are precisely and formally defined
- Formality: Extent to which primitives are described in a formal language
- Rigid Class: $\phi$ is a necessary property for all its instances 

# Additional Resources
- [Ontology Overview (W3C)](https://www.jfsowa.com/ontology/ontoshar.htm)
- [An Overview of OntoClean](https://www.researchgate.net/publication/226934944_An_Overview_of_OntoClean)

# Notes
## Encoding Knowledge
- Ontology derived from Latin
	- Ontos: to be/being
	- Logos: discourses/schemata
- Humans interpret information all the time and use that interpretation to inform the next acquisition
	- Machines are only capable of simulation, not true interpretation
- Understanding requires shared ontologies
	- We need a <mark style="background: #FFB86CA6;">base set of universal logic/understanding</mark> through which we can operate to be able to interpret
	- Must have an intentional semantic structure to encode implicit rules
		- ex: a car has four wheels and at least one front window
- Pierce's Semiotics are the mediums through which signs are interpreted
	- Icon: Shows the shape of an entity (fire itself)
	- Index: Points towards the entity (smoke of a fire)
	- Symbol: A representation using a convention (e.g., the English Language)
	- Machines prefer symbols
- DIKW Pyramid shows that knowledge is where interpretation is afforded to our data
	 ![[Pasted image 20250406214836.png]]
## Ontology Formalization
- Formal ontologies are a logical theory
	- Concepts are linked together in a structure
	 ![[Pasted image 20250406213735.png]]
- Ontologies are comprised of properties (relations) and classes (objects)
	- Have an extension (enumeration) and intension (definition) for all primitives defined
- Properties in an ontology have a signature which specifies which objects may be on either side of the relation
	- Domain (input classes) and range (output classes/literals)
- Ontologies are largely driven by the domain of application and the culture of the developers
	- Specific domains will take different concepts to be ground truth that may not apply in others
	- Hierarchies may be conceptually different across languages (consider the lack of a general "Vehicle" concept in Chinese but the presence of the "Che")
	- The specific scenario of the application will also define the necessary coverage, specificity, and granularity to correctly balance the trade-off
- Ontologies are NOT the same as Taxonomies
	- Taxonomy is a subclass of ontology
	- Example: links between chemical compounds in chemistry are ontological knowledge but not taxonomical knowledge
## Knowledge Based System and Ontological Commitment
- The knowledge base is comprised of both the ontology and the predefined facts
	- Example: students have scores and scores are floats between 0 and 100
- The inference engine is what applies everything together to make use of the knowledge
	- It contains...
		- The knowledge base 
		- Rules
			- If a student has a score less than 50%, then they fail
		- Checking/[[Data Validation (SHACL and OWL)|Data Validation]]
			- Number of scores for a course must be equal to number of students taking the course
		- Explain
			- Languages to formalize the ontologies
	 ![[Pasted image 20250406215738.png]]
- The domain of the application is not necessarily that of the ontology
	- When designing/extending/reusing an ontology, it is <mark style="background: #FFB86CA6;">a commitment to that conceptualization of the world</mark> which may not make sense for the application
	- Example: Medical ontologies which say you cannot be your own parent would not work in Hollywood for describing The Terminator
	- Performing a formal concept analysis helps with ontology construction
		 ![[Pasted image 20250406220145.png]]