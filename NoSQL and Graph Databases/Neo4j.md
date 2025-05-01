|   Course Name   |         Topic         |  Professor  |        Date        |             Tags              |
| :-------------: | :-------------------: | :---------: | :----------------: | :---------------------------: |
| **NOSQL Neo4j** | Graph Databases NoSQL | Ana Escobar | 23-26 julliet 2024 | #GraphTheory #Data_Management |

[Class Video Link](URL)

# Summary
*A 3-4 sentence description of what was learned in italics*

# Key Takeaways
1. Neo4j is the leading open-source graph database
2. As datasets grow in size (especially connectedness), graph databases are far more efficient for querying
3. In Neo4j, a node can have zero, one, or many labels

# Definitions
- Graph: A data store which uses vertices (nodes) and edges (relationships) to show data linkage
- Property Graph: A graph in which the individual nodes have labels and node properties 
- Labels: A mechanism to signify that a node belongs to a subset of nodes

# Additional Resources
- Name the hyperlink in brackets then outside the brackets put the URL in parens

# Notes
## Neo4j Graph Model
- Neo4j is built on a labelled property graph model
	- Nodes and relationships can have additional information attached to them
	- This is unlike [[RDF|RDF]] which does not support properties
- Neo4j allows for undirected (symmetric) relationships between nodes
- Property graph
	- In addition to nodes and edges, graphs in Neo4j also have labels and node properties
	- If a property does not exist in a given node (even w/in the same label), it is simply <mark style="background: #FFB86CA6;">treated as a null value</mark>
- 