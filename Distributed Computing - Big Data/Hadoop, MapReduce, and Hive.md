|      Course Name       | Topic  | Professor  |      Date       |       Tags       |
| :--------------------: | :----: | :--------: | :-------------: | :--------------: |
| **Big Data Ecosystem** | Hadoop | Mori Huang | 03-04 juin 2025 | #Data_Management |

[Class Video Link 1](https://dstisas-my.sharepoint.com/personal/blaise_pascal_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fblaise%5Fpascal%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20250602%5F095456%2DMeeting%20Recording%201%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E3511936c%2D0e3f%2D40de%2D9e78%2D37a60ac4d0b5)
[Class Video Link 2](https://dstisas-my.sharepoint.com/personal/blaise_pascal_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fblaise%5Fpascal%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FA24%20%2D%20Common%20Link%20DS%5FDE%5FDA%2D20250604%5F095321%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E80d45261%2D22df%2D488a%2Dbf37%2D891da5df11a9)

# Summary
*Hadoop is the main distributed computing architecture which includes a full suite of open-source software solutions for resource management, file management and storage, and computation. As it is very low-level to work with, abstractions have been built on top of this architecture to provide more user-friendly tooling like Hive Query Language and HBase.*

# Key Takeaways
1. HDFS provides resiliency by replicating blocks of data (3x by default) on different nodes/racks
2. HDFS data is write once, read many (WORM), so modifications of existing data are not directly possible
3. MapReduce jobs write all intermediate steps to disk
4. The number of output files created by a MapReduce job equals the number of reducers

# Definitions
- Hadoop Ecosystem: Stack of open source software needed to build a [[Data Ingestion and Engineering|data lake]] and exploit the data stored within
- Hadoop Distributed Filesystem (HDFS): The underlying filesystem that Hadoop uses which splits data across hundreds/thousands of [[Distributed Systems Overview|nodes]] and replicates data
- Yet Another Resource Manager (YARN): Management of cluster resources
	- Handles RAM and CPU of the worker nodes and allocates resource for applications
- Small-File Problem: Since the name node stores file metadata in RAM, having many small files on HDFS can overwhelm the name node's memory
- Application: A single job or a directed acyclic graph of jobs
- Directed Acyclic Graph (DAG): A graph which has directional relations between nodes such that it is impossible to reach a node again once it has already been visited (no loops)
- Online Analytical Processing (OLAP): The processing of large amounts of data simultaneously as a batch
	- Reporting pipelines
- Online Transaction Processing (OLTP): Read/insert/update a few values as fast as possible. Generally handles only single records at a time
	- Financial transactions
- Wide-Column Databases: A type of non-relational database that store data in columns rather than rows, allowing for efficient storage and retrieval of sparse data sets

# Additional Resources
- [HDFS Architecture Docs](https://hadoop.apache.org/docs/r3.1.0/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html)
- [Mastering Hive Partitioning](https://www.sparkcodehub.com/hive/partitioning-in-hive#:~:text=Understanding%20Hive%20Partitioning,instead%20of%20the%20whole%20dataset.)

# Notes
## HDFS
- HDFS is built according to the [[Distributed Systems Overview|master/slave architecture]]
	- The Name Node is the master which handles filesystem metadata
		- Knows exact path of every file and which blocks compose that file
		- Knows the position of every block in the cluster
		- Filesystem metadata is stored in RAM by the name node
	- The Data Nodes are the workers which actually store the files on discs and handle all the read/write optimizations
	- The Journal Node stores edit logs of the Name Node to ensure fault tolerance
		- Also handles synchronized updates between active and standby name nodes
- Storage mechanism
	- A file is divided into blocks which are 128 MB max
		- A file that is less than 128 MB does not "waste space"
	- Blocks are replicated (3x by default but this is a tunable parameter)
		- Replication is done on OTHER nodes to assist with resiliency
		- HDFS is rack-aware to help provide even more resiliency
- Availability can be achieved using more than one Name Node
	- One active and one standby
	- Helps to avoid single points of failure
	- Zookeeper is used to determine which name node is in-charge to <mark style="background: #FFB86CA6;">avoid the split-brain scenario</mark>
## YARN
- YARN handles resource allocation on the cluster
- Also responsible for job monitoring
- Architecture is similar to HDFS with a Resource Manager (Master) and a Node Manager (Worker)
	- The resource manager schedules applications and gathers info about running applications
- YARN scheduling of applications can be configured to follow many different algorithms
	- First-in-first-out (FIFO), Capacity Scheduling, Fair Scheduling
## MapReduce
- Designed to help write applications that process vast amounts of data on large clusters in a reliable, fault-tolerant manner
- Application steps
	- Input is a key-value pair
	- Map input to intermediate key-value pairs
	- Shuffle and sort to dispatch key-value pairs w/ same key to the same reduce
	- Reduce the set of values with the same key to a smaller set (Aggregate)
- Example: Word count count by word in a set of document
	 ![[Pasted image 20250615104727.png]]
- Outputs for MapReduce are <mark style="background: #FFB86CA6;">written to disk between each step</mark>
	- Makes this slow but requires very little RAM to run large jobs
	- Number of mappers depends on number of blocks
	- Number of reducers depends on number of [[Distributed Systems Overview|worker nodes]]
	- Number of output parts = number of reducers
## Hive
- Provides an [[Basic Querying|SQL]]-like language to query <mark style="background: #FFB86CA6;">data already on HDFS</mark> called HiveQL
	- HiveQL builds a directed acyclic graph (DAG) of jobs on YARN and executes them using one of many frameworks (MapReduce, Tez, or Spark) -- Tez uses RAM and can chain reduces
	- Supports querying of many file formats including CSV, JSON or optimized formats like Apache ORC, Parquet, and Avro
		- <mark style="background: #FFB86CA6;">ORC and Parquet are columnar storage while Avro is row-based</mark>
- Provides for Online Analytical Processing (OLAP) only
	- HiveQL is really <mark style="background: #FFB86CA6;">only appropriate for batch processing jobs</mark>
- Architecture of Hive
	- The Hive Server converts HiveQL to Tez/MapReduce
	- The Hive Metastore stores metadata in RDBMS
		- Database metadata and table statistics
	- The Hive Client connects one or many applications to the Hive Server
- Hive data can (and should) be partitioned to allow for faster and easier access
	- The most common partition is by date, but we can partition files by anything
	- Should not make partitions too small though or else we run into the small files problem
	- 1 partition = 1 subfolder in HDFS
## HBase
- HBase is the NoSQL querying language for Hadoop which also (like Hive) relies on HDFS for storage
- HBase is a wide-column database
	- A table is a collection of rows that have columns and column families
	```json
	{
	"key_1": {
		"column_family_1": { "col_1": "a", "col_2": "b"},
		"column_family_2": { "col_3": "c", "col_4": "d"}
		}
	}
	```
- Provides for <mark style="background: #FFB86CA6;">both OLAP and OLTP</mark>
- The architecture is an HBase Master and a Region Server
	- A region is a set of rows with a certain range of keys
	- The master handles create and delete queries and assigns regions to region servers