|   Course Name   |         Topic         |  Professor  |        Date        |             Tags              |
| :-------------: | :-------------------: | :---------: | :----------------: | :---------------------------: |
| **NOSQL Neo4j** | Graph Databases NoSQL | Ana Escobar | 23-26 julliet 2024 | #GraphTheory #Data_Management |

# Summary
*Neo4j is the leading graph database management system. Unlike traditional [[Relational Database Management System|RDBMS]] systems, Neo4j's data model connects entities (nodes) together directly using relationships. As a database, it comes with a specialized query language, [[Cypher Query Language|Cypher]]. Neo4j is able to be deployed on the cloud and can be interacted with via Python as well.*

# Key Takeaways
1. Neo4j is the leading open-source graph database
2. As datasets grow in size (especially connectedness), graph databases are far more efficient for querying
3. In Neo4j, a node can have zero, one, or many labels

# Definitions
- Graph: A data store which uses vertices (nodes) and edges (relationships) to show data linkage
- Property Graph: A graph in which the individual nodes have labels and node properties 
- Labels: A mechanism to signify that a node belongs to a subset of nodes

# Additional Resources
- [Neo4j Documentation](https://neo4j.com/docs/)
- [Example Use Cases](https://neo4j.com/graphgists/)
- [Graph Data Science Python Example](https://github.com/Egjfour/vacation_bookings_prediction_neo4j)

# Notes
## Neo4j Graph Model
- Neo4j is built on a labelled property graph model
	- Nodes and relationships can have additional information attached to them
	- This is unlike [[RDF|RDF]] which does not support properties
- Neo4j allows for undirected (symmetric) relationships between nodes
- Property graph
	- In addition to nodes and edges, graphs in Neo4j also have labels and node properties
		- Edges are able to have attributes which can allow for weighting
	- If a property does not exist in a given node (even w/in the same label), it is simply <mark style="background: #FFB86CA6;">treated as a null value</mark>
	- Neo4j is also a native graph data model including storage and the processing engine
- Features
	- Index and schema are optional
		- <mark style="background: #FFB86CA6;">Index-free adjacency drives performance</mark>
	- Supports `UNIQUE` constraints
	- [[MongoDB|ACID]] compliant
	- Advanced distributed computing option via sharding
## Neo4j on the Cloud
- 3 options on AWS
	- Single-instance on [[Computation (EC2, Lambda, Containers)|EC2]]
	- Neo4j community edition on AWS marketplace
	- Causal cluster on AWS marketplace
- Similar options for deployment directly from Azure marketplace exist as well
- Neo4j is also supported via [[Deployment (CI-CD and Containers)|Docker]] and Kubernetes on any cloud
## Neo4j and Python
- Use the Neo4j Python driver (only a single instance per application)
	- `pip install neo4j`
	```python
	# Import the neo4j dependency
	from neo4j import GraphDatabase
	# Create a new Driver instance
	driver = GraphDatabase.driver("neo4j://localhost:7687",
								   auth=("neo4j", "neo"))
	```
- Once the driver is created, we create sessions to execute transactions
	- `driver.session(database = "db_name")`
	- Then `session.run({query}, **kwargs)`
		- The `kwargs` are named parameters that can be referenced with `$` in the query
	- `session.execute_read` and `session.execute_write` allow us to wrap a unit of work in a retry loop in case of database failures as opposed to `session.run` which will fail