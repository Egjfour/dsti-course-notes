|   Course Name    |       Topic       |   Professor   |     Date     |     Tags     |
| :--------------: | :---------------: | :-----------: | :----------: | :----------: |
| **Semantic Web** | Graph of Web Data | Fabien Gandon | 26 mars 2025 | #GraphTheory |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/johnny_najjar_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fjohnny%5Fnajjar%5Fdsti%5Finstitute%2FDocuments%2FRecordings%281%29%2FA24%20%2D%20Common%20Link%20%2D%20DS%2DDE%2DDA%2D20250326%5F095027%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E22716709%2Da047%2D40d2%2D99f3%2D47f23b568e58)

# Summary
*The modern web, primarily attributed to Tim Berners-Lee, is a combination of networking (the internet) and hypertext/hypermedia which lets us link concepts together. The web is built on three key pillars: identification and addressing, representation, and a communication protocol. The underlying data on the web can be accessed in RDF format which is a standardized way of handling linked data. Many websites have this content available which can be accessed through content negotiation in the HTTP headers of a request to a URI.*

# Key Takeaways
1. The internet is NOT the same as the web
2. The web will be truly useful when it can understand the semantic representation of the world
3. The full potential of the web is to connect all kinds of intelligence
4. [[RDF|RDFS]] lets us connect concepts semantically to each other (e.g., Book -> Author)
5. Knowledge graphs are directed, labelled multigraphs
6. User agents inform the servers of the preferred media (MIME) type
7. "He who controls the metadata, controls the web"

# Definitions
- Internet: Infrastructure which allows for networking
- Web: Application of distributing hypertext over the internet
- Knowledge Graph: The combination of named and linked entities with named relations
- Directed Graph: A graph where links between nodes go in one and only one specified direction
- Semantic Web: The collection of knowledge graphs as a standard representation, built on distributed linked data/graphs, using distributed schemas/semantics 
- Resource: Anything which can be connected on the web and identified with a URI
- XML: Structured data using tags
- Content Negotiation: The process of using HTTP headers to specify the acceptable representations of a resource you would like to receive from a given URI

# Additional Resources
- [As We May Think](https://www.theatlantic.com/magazine/archive/1945/07/as-we-may-think/303881/)
- [Content Negotiation via HTTP Headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/Content_negotiation)

# Notes
## History of the Web
- 1945: Article "As We May Think" from Vannevar Bush
	- Considers that humans cannot keep up with amount of content generated
- 1965: Ted Nelson coined the Hypertext term as a data model for Bush's idea
	- Also extended this to images (Hypertext -> Hypermedia)
- 1989: Tim Berners-Lee Merged Hypertext and [[Networking (TCP and UDP)|networking]] to create the web
	- The web is built on top of the internet but is not, itself, the internet
- 1994: Ward Cunningham's Wiki re-opened write access to the web
	- Led to the explosion of social networking and user-created content
	- Facebook's Open Graph Protocol (OGP) allowed other websites to use semantic injection in the tags of the website itself to communicate back and forth with Facebook
- When the web was first born, it was in <mark style="background: #FFB86CA6;">read and write</mark> mode like a giant Wiki
	- Changes happened in the server for everyone
	- Future browsers disallowed this for security
- Web Applications (Dynamic Webpages) came next
	- Web services directories allow different services to (e.g., spellcheck and translate) to communicate allowing for application-to-application connection
	- We can provide various schemata/[[Ontologies|ontologies]] for various services
- Web ML is a recent advancement which allows for the user's browser to be used as a [[Virtual Machines|virtual machine]] to execute ML models
	- The computational costs of ML inference can be on the end user 
## Key Elements of the Web
- Identification and Addressing (Typical: URL)
	- Started with URL (Universal Resource Locator): Identify and local <mark style="background: #FFB86CA6;">resources which are on the web</mark>
	- Moved to URI (Universal Resource Identifier): Identify, on the web, <mark style="background: #FFB86CA6;">everything that exists</mark>
		- Extended by IRI (International Resource Identifier) to represent, in any language, everything that exists (non-ASCII characters)
		- Key difference is that URIs identify all things -both on and not on the web - such as physical objects which are not actually on the web
			- Resources which are not on the web must have representations on the web
			- ![[Pasted image 20250405112508.png]]
- Representation Language (Typical: HTML)
	- Additional representations allowed us to separate the presentation and data layers
	- XML was introduced in 1998 to build a <mark style="background: #FFB86CA6;">network of general structured documents</mark>
		- XML can be used to represent ANYTHING and provide standardized processing
	- [[RDF|RDF]] was created as the <mark style="background: #FFB86CA6;">first semantic web language</mark>
		- It is a distributed graph description built using little triples 
			- e.g., <doc.html> {has for author} {Eddie}
		- We can [[Basic Querying|query]] any RDF data with [[SPARQL Basics|SPARQL]]
		- Concepts can also be linked in RDF using RDFS
- Communication/Protocol (Typical: HTTP)
## Standardization
- Mainly handled by the World Wide Web Consortium (W3C)
	- All ~400 members have one equal vote
	- Designers of the web architecture
- W3C standardization process
	- Main phases are (least to most stable)...
		- Working Draft, Candidate Recommendation, Proposed Recommendation, and Recommendation
	 ![[Pasted image 20250405092926.png]]
- Standards for Protecting People
	- PICS rating system developed in 1997 to protect children
		- Ratings are given for amount of swear words, sexually explicit content, etc and are maintained by the website themselves
		- Websites are incentivized with SEO to provide the ratings
	- Protecting Web Surfers in 2002 gave user preference for privacy sharing but was made obsolete because there was no adoption by the websites due to no incentive
- Security was standardized through XML
## Knowledge Graphs, Semantic Web, and Linked Data
- Knowledge graphs are comprised of
	- Named entities (formal and universal naming)
	- Linked entities
	- Named relations
- Knowledge graphs are directed, labelled, multi-graphs
	- Used for data contextualization (RAG for LLMs), recommendation, and explainability
	- Flexible extensions and loose schemas for complex querying and validation as well as <mark style="background: #FFB86CA6;">inferential schemata</mark>
- Knowledge graphs support associative (many links) data and [[Object-Oriented Design|object-oriented]] structures
	- These, however, are not [[Neo4j|property graphs]]. Nodes and relationships cannot have attributes
- Semantic web uses knowledge graphs as a standard representation of resources
	- Uses <mark style="background: #FFB86CA6;">distributed</mark> graphs and schemata
	- Relative to the web...
		- HTML -> Representations
		- URL -> URI -> IRI
- Linked Data
	- Uses [[RDF|RDF]] as a format and HTTP URIs as names for resources
	- Useful information should be provided using content negotiation when looking up a URI and links to other URIs should exist so related things can be discovered
	- Several web mechanisms which make this work: [[Internet Protocol (IP) and LAN|DNS]], Content Negotiation, and HTTP Redirect
## XML Concepts
- XML Formatting Rules
	- All tags must be closed, but tags with no content can be self-closing
		- Typical: `<root>...</root>`
		- Self-Closing: `<x/>`
	- XML is case-sensitive and the nesting order must be respected
		- Example (Incorrect): `<a><b></a></b>`
		- `<x>` $\ne$ `<X>`
	- Tags cannot include spaces or start with "xml" or any number
		- Examples (Incorrect): `<1an> <xmla> <bla bla>`
	- Attributes can be included within the tag
		- Example: `<tel type="mobile">724-591-3664</tel>`
- All XML files have a root which is the start and end of the file
## Content Negotiation
- Process which happens automatically between users and web servers whenever a webpage is accessed to serve <mark style="background: #FFB86CA6;">different representations of a resource at the same URI</mark>
- Browsers typically negotiate HTML from web servers so that they can display content in a human-friendly way
	- We can negotiate other things as well... the underlying data
- HTTP headers indicate preferences media type preferences (MIME type, format, language)
	- These can also be weighted using the `q` parameter in an HTTP request
	- Example (Languages): `Accept-Language: fr; q=1.0, en; q=0.5`
		- Accepts French with a preference of 1 and English with a preference of 0.5
- MIME Types (media type) indicate the file formats and format content
	- Examples: `application/javascript, application/json, application/msword, application/pdf, application/sql, application/vnd.ms-excel, application/vnd.ms-powerpoint, application/xml, application/zip, audio/mpeg, image/jpeg, text/plain, text/css, text/csv, text/html, text/xml`
	- RDF Mime Types
		- JSONLD (`.jsonld`): `application/ld+json`
		- N-Triples (`.nt`): `application/n-triples`
		- Turtle (`.ttl`): `text/turtle`
		- RDF XML (`.rdf`/`.xml`): `application/rdf+xml`
		- N3 (`.n3`): `application/n3` OR `text/n3`
		- Trig (`.trig`): `application/trig`
- We can specify desired content in `curl`/`wget` commands
	- Example: `curl -o Paris-rdf.xml -L -H "Accept: application/rdf+xml" http://dbpedia.org/resource/Paris`
		- Goes to the resource at dbpedia for Paris and tries to get RDF XML
		- `-o` saves it to a file at that location with that name
		- `-L` allows HTTP redirects
		- `-H` lets us provide HTTP headers as the next argument as a string