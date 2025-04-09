|   Course Name    |               Topic               |   Professor   |       Date       | Tags |
| :--------------: | :-------------------------------: | :-----------: | :--------------: | :--: |
| **Semantic Web** | Famous [[Ontologies\|Ontologies]] | Fabien Gandon | 03-04 avril 2025 |      |

[Class Video Link 1](https://dstisas-my.sharepoint.com/personal/johnny_najjar_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fjohnny%5Fnajjar%5Fdsti%5Finstitute%2FDocuments%2FRecordings%281%29%2FA24%20%2D%20Common%20Link%20%2D%20DS%2DDE%2DDA%2D20250403%5F094949%2DMeeting%20Recording%201%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E06310354%2Da587%2D405c%2D8441%2D42befa6c3b28)
[Class Video Link 2](https://dstisas-my.sharepoint.com/personal/johnny_najjar_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fjohnny%5Fnajjar%5Fdsti%5Finstitute%2FDocuments%2FRecordings%281%29%2FA24%20%2D%20Common%20Link%20%2D%20DS%2DDE%2DDA%2D20250404%5F094713%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E09086b03%2D952c%2D4b3f%2D996f%2D756103333867)

# Summary
*As the [[Internet and Web|web]] links many resources which are similar in nature together, flexible high-level ontologies have been developed for a variety of domains such as social networking, describing of documents and datasets, and data traceability. It is generally advised, where possible, to use these existing ontologies to allow for greater interoperability with other datasets.*

# Key Takeaways
1. There can only be one preferred label per language for a concept in SKOS
2. Creative Commons Licenses can be generated using their tool
3. Existing ontologies, where possible and reasonable, should be used as much as possible

# Additional Resources
- [Schema.org](https://schema.org/)
- [SKOS](https://www.w3.org/2009/08/skos-reference/skos.html)
- [Dublin Core](http://purl.org/dc/elements/1.1/)
- [Creative Commons](http://creativecommons.org/ns#)
- [Friend of a Friend](http://xmlns.com/foaf/0.1/)
- [Relationship](http://purl.org/vocab/relationship/)
- [Media Resources](http://www.w3.org/TR/mediaont-10/)
- [LOV Schemata Search Engine](https://lov.linkeddata.es/)

# Notes
## Schema.org
- `<https://schema.org/>`
- Founded by Bing, Google, Yahoo, and Yandex
- create, maintain, and promote schemas for structured data on the Internet, on web pages, in email messages
- Used by 10 millions sites and includes many domains
## SKOS (`skos:`)
- `<http://www.w3.org/2004/02/skos/core#>`
- Knowledge in thesauri, classifications, subject, etc to describe and document concepts
	- Library data
- Topics are organized w/o the need for classes
	- Everything is just a `skos:Concept` which inherits from `owl:Class`
- Labels are the primary driving force with three main types
	- Preferred Labels (`skos:prefLabel`): At most one per language
	- Alternative Labels (`skos:altLabel`)
	- Hidden Labels (`skos:hiddenLabel`): Used for sorting and handling non-ASCII languages
- Additional notes can be added to documents
	- `skos:note, skos:definition, and skos:examples`
	- Notes also can include `skos:scopeNote` and `skos:historyNote`
- Relations between concepts also exist with `skos:narrower` and `skos:broader`
	- These relations are [[OWL Property Extensions|inverse but not transitive]]
	- Inherit from the transitive properties `skos:narrowerTransitive` and `skos:broaderTransitive`
- Related concepts can be linked with `skos:related` which are neither narrower nor broader
	- `skos:related` is [[OWL Logic and Class Extensions|symmetric but not transitive]]
- Linking to other schemata is done with the `skos:exactMatch and skos:closeMatch` operators
	- `skos:exactMatch` is transitive but `skos:closeMatch` is not
	- Also provides for `skos:narrowMatch` and `skos:broadMatch` for cases when the narrow/broad concepts are defined elsewhere
## Dublin Core (`dc:` and `dcterms:`)
- `<http://purl.org/dc/elements/1.1/>`
- Popular schema for describing documents
	- `dc:title, dc:date, dc:subject, dc:coverage, dc:description, dc:format, dc:language, dc:type, dc:source, dc:identifier, dc:rights, dc:creator, dc:relation, dc:contributor, dc:publisher`
- Also provides the DCTerms namespace: `<http://purl.org/dc/terms/>`
	- This allows for defining the type among other things
	- Example: `dc:type dcterms:Text`
- Mixes well with SKOS to say "I have a document with a concept"
## Creative Commons (`cc:`)
- `<http://creativecommons.org/ns#>`
- Describes the rights associated to a resource
	- Rights, conditions, and prohibitions for use
- Fully aligned with and extends the Dublin Core
- Properties
	- `cc:license, cc:permits, cc:morePermissions, cc:requires, cc:attributionName, cc:prohibits, cc:attributionURL, cc:jurisdiction, cc:useGuidelines, cc:legalcode, cc:deprecatedOn`
- Classes
	- `cc:License, cc:Reproduction, cc:Notice, cc:Distribution, cc:Attribution, cc:DerivativeWorks, cc:ShareAlike, cc:Sharing, cc:SourceCode, cc:CommercialUse, cc:Copyleft, cc:HighIncomeNationUse, cc:LesserCopyleft`
- Predefined/common licenses from the creative commons can be used as a direct URI
- Example of manually building a license:
	```turtle
	# Combines SKOS, Dublin Core, and a CC License to describe a topic
	@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
	@prefix dc: <http://purl.org/dc/elements/1.1/> .
	@prefix skos: <http://www.w3.org/2004/02/skos/core#> .
	@prefix cc: <http://creativecommons.org/ns#> .
	
	<InriaTopics> a skos:ConceptScheme ;
		dc:title "Inria Research Topics" ;
		cc:license [
			a cc:License ;
			cc:permits cc:DerivativeWorks, cc:Distribution ;
			cc:requires cc:Attribution, cc:Notice, cc:ShareAlike ] ;
		skos:hasTopConcept <#ComputerScience> .
	```
## Friend of a Friend (`foaf:`)
- `<http://xmlns.com/foaf/0.1/>`
- Popular schema for describing persons and social networks
- FOAF = Core + Social Web + Linked Data Utilities
- Describing user profiles and social networks
	- Classes
		- `:Agent, :Person, :Project, :Organization, :Group, :Document, :Image`
	- Properties
		- `:name, :title, :img, :depiction, :familyName, :givenName, :knows, :based_near, :age, :made (:maker), :member, :primaryTopic`
- Describing social activities (accounts/actions)
	- Classes
		- `:OnlineAccount
	- Properties
		- `:mbox, :homepage, :weblog, :workplaceHomepage, :schoolHomepage, :account, :accountName, :nick, :publication, :currentProject, :pastProject, :interest, :topic_interest, :topic``
## Relationship (`rel:`)
- `<http://purl.org/vocab/relationship/>`
- Extends the `foaf` schema with more complex relationships between people
	- `foaf` only really provides for a `foaf:knows` property
- One class: `rel:RelationShip`
- Many properties
	- `rel:friendOf, rel:acquaintanceOf, rel:closeFriendOf, rel:parentOf, rel:siblingOf, rel:childOf, rel:grandchildOf, rel:grandparentOf, rel:spouseOf, rel:ancestorOf, rel:descendantOf, rel:enemyOf, rel:antagonistOf, rel:ambivalentOf, rel:lostContactWith, rel:knowsOf, rel:knowsInPassing, rel:knowsByReputation, rel:hasMet, rel:worksWith, rel:colleagueOf, rel:collaboratesWith, rel:employerOf, rel:employedBy, rel:mentorOf, rel:apprenticeTo, rel:livesWith, rel:neighborOf, rel:lifePartnerOf, rel:engagedTo, rel:influencedBy`
## VoID (`void:`)
- Describes other RDF/linked datasets
- Extends both Dublin Core and FOAF
 ![[Pasted image 20250409103117.png]]
 - Example: Declare the DBPedia dataset
	```turtle
	:DBpedia a void:Dataset;
		void:sparqlEndpoint ;
		void:feature :RDFXML ;
		void:subset :DBpedia2Geonames ;
		void:uriLookupEndpoint ;
		dcterms:modified "2008-11-17"^^xsd:date;
		dcterms:title "DBPedia";
		dcterms:description "RDF data extracted from Wikipedia";
		dcterms:publisher :DBpedia_community;
		dcterms:license ;
		dcterms:source .
	```
- VoID allows for mapping of schemata together with a `void:Linkset
	- Example: DBPedia predicates that match between Geonames and DBPedia are the same
		```turtle
		:DBpedia2Geonames a void:Linkset ;
			void:linkPredicate owl:sameAs ;
				void:target :DBpedia ;
				void:target :Geonames .
		```
## DCAT and Data Cube (`dcat:` and `qb:`)
- DCAT allows for describing of non-RDF datasets (CSV, SQL, etc)
	 ![[Pasted image 20250409103724.png]]
- Data Cube is used to publish statistics on the data to understand processing
	![[Pasted image 20250409103811.png]]
## Provenance: PROV-O
- Used for traceability to describe entities and activities involved in providing a resource
 ![[Pasted image 20250409104211.png]]
- Example: A chart produced from two data sources
	```turtle
	ex:compose prov:used ex:dataSet1 ;
		prov:used ex:regionList .
	ex:composition prov:wasGeneratedBy ex:compose .
	ex:illustrate prov:used ex:composition .
	ex:chart1 prov:wasGeneratedBy ex:illustrate .
	```
	 ![[Pasted image 20250409104131.png]]
## Media Resources (`ma:`)
- `<http://www.w3.org/TR/mediaont-10/>`
- Allows for defining fragments of multimedia (video, audio, etc) resources
- Four dimensions
	- Temporal
	- Spatial
	- Track
	- Named
## Finding Existing Schemata
- The vocabulary search engine, LOV, lets us search for schemata based on keywords
- Displays in order of references to the relevant vocabularies
- Also displays how many classes/properties there are and how many vocabularies reference the one you're seeing and how many it references as well