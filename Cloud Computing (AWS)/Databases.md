|  Course Name   |   Topic   | Professor |       Date        |                 Tags                  |
| :------------: | :-------: | :-------: | :---------------: | :-----------------------------------: |
| **Amazon AWS** | Databases |   Ayoub   | 05 September 2024 | #CloudComputing #AWS #Data_Management |

# Summary
*AWS has options for many popular relational and purpose-built databases. Within the relational space, Amazon RDS can handle most known types and offers a cost-effective and query-optimized service for MySQL and PostgreSQL called Aurora. Other critical services allow for proxying to minimize open connections, non-relational databases like DynamoDB, and data warehousing capabilities in Redshift. AWS also offers a [[AWS Managed Services|service to assist with database migration, AWS DMS]]*.

# Key Takeaways
1. The relational database service is managing DB volumes and log storage on the Elastic Block Store of a compute resource
2. The amount of responsibility that a DB admin has decreases moving from on-prem to hosted on EC2 to being part of a managed database service like RDS or Aurora
3. RDS allows for cross-region backups using S3 buckets that are controlled by RDS
4. By default, DynamoDB replicates data across multiple AZs in a single region

# Definitions
- Automated Backups: Restore a database to a specific point in time
	- CoCalc/Google Docs saving every x seconds
- Snapshots: Manually save a database in a known state for backup until the user deletes it
	- A commit on Github
- Throughput: Amount of data being passed back and forth through input/output (I/O) operations
- Vertical Scaling: Expand the resources that the existing server uses to increase capacity
	- Complex and time-consuming since it involves upgrading memory, storage, or processing power
- Horizontal Scaling: Increasing the number of servers that the database tuns on
	- Capacity added while database is running (no downtime to scale)
- Data Warehouse: An online analytical processing (OLAP) relational database that is optimized for read-heavy querying of entire datasets for reporting and analytics

# Additional Resources
- [Difference between RDS and Aurora](https://medium.com/awesome-cloud/aws-difference-between-amazon-aurora-and-amazon-rds-comparison-aws-aurora-vs-aws-rds-databases-60a69dbec41f)

# Notes
## Database Options

| Name                              | Relational (Y/N) | Use Case                                                                                                                                                       | Other Details                                                                                                                                                 |
| --------------------------------- | :--------------: | -------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Relational Database Service (RDS) |        Y         | - Transactional applications like ERPs, CRMs, and ecommerce apps - Online Transaction Processing (OLTP)<br>- Meant for structured data                         | - Many options and compatibilities (MySQL, PostgreSQL, MariaDB, Oracle, and SQL Server)<br>- Aurora engine support for MySQL and PostgreSQL                   |
| Dynamo DB                         |        N         | - Key-value databases<br>- Develop applications, media metadata, scale gaming platforms                                                                        | - Fully managed and serverless with millisecond performance                                                                                                   |
| Neptune                           |        N         | - Graph Databases<br>- Connections or paths within data<br>                                                                                                    | - Fully managed service<br>- Scale-up in-memory-optimized architecture to allow for fast query evaluation on large graphs<br>- Support up to 15 read replicas |
| Elasticache                       |        N         | - In-memory database                                                                                                                                           |                                                                                                                                                               |
| Timestram                         |        N         | - IoT and operational applications<br>- Patterns and trends over time                                                                                          |                                                                                                                                                               |
| Keyspaces (for Apache Cassandra)  |        N         | - Cassandra workloads<br>- Fast querying of high data volumes                                                                                                  | - Wide column data model<br>- Data can evolve over time                                                                                                       |
| MemoryDB for Redis                |        N         | - In-memory workloads<br>- Latency-sensitive, high request rate, high throughput, and no data loss<br>- Caching, game leaderboards, and bank user transactions | - Eliminate need to access disks<br>- Leverages a distributed transactional log                                                                               |
| Quantum Ledger Database           |        N         | - Ledger database<br>- A transparent, immutable, and cryptographically verifiable transaction log                                                              | - Tracks every app data change and has a complete and verifiable history over time                                                                            |
| DocumentDB                        |        N         | - Document database<br>- Flexible schema<br>- Different attributes and data values                                                                             | - Compatibility with [[MongoDB\|MongoDB]]                                                                                                                     |
## Managed Relational Databases (RDS and Aurora)
- RDS
	- Managed Relational Database Service for deploying and scaling relational databases
	- Allows for built in automated failover with the Multi-AZ deployment
	- Database and log storage are maintained on the [[Computation (EC2, Lambda, Containers)|EC2 Elastic Block Storage]]
	- Instances are isolated database environments that can contain multiple user-created databases
	- EC2 Instance Type Choice
		- General Purpose (CPU-intensive): t4g, t3, m6g, m5)
		- Memory-optimized (query-intensive workloads): t6g, r5, x2g, x1e
- Aurora
	- RDBMS managed by RDS built specifically for the cloud with high performance and availability at a much lower cost
	- Features a distributed, fault-tolerant, self-healing storage system that autoscales up to 64 TB per instance
	- High performance and availability thanks to point-in-time recovery, continuous backup to S3, replication across 3 AZs, and up to 15 low-latency read replicas
- Database clusters (Aurora)
	- One or more database instances and a cluster volume (storage) that manages data for all instances and spans multiple AZs
	- Two types of database in a cluster: primary DB instance which supports read and write operations and performs all data modifications to the cluster volume
	- Database replicas connect to the same storage volume and are only able to perform read operations (Replicas are also used for automatic failover)
- Serverless Option (Aurora)
	- On-demand autoscaling configuration to provide hands-off capacity management
	- Good for variable workloads, new apps, dev/test, and capacity planning
## RDS Proxy
- Applications can <mark style="background: #FFB86CA6;">pool and share connections established with the database</mark>
	- Many apps have many open connections and a lot of opening and closing of connections which is bad for storage and compute resources
- Reduces failover times by up to 66%
	- Transactions are queues by the proxy during failovers
	- Proxy can accept new connections that come in during the failover
- Streamlines authentication by using the IAM credentials for the application instance and letting the proxy handle the mapped identity from secrets manager
## Dynamo DB
- Supports [[MongoDB|key-value and document data]]
- Millisecond performance and automatic scaling of tables to adjust for capacity
- Secondary indexes (global and local) allow for data querying using an alternate key
- Terminology
	- Table: A collection of data. Unique to an account ID and region
	- Item: Group of attributes that is uniquely identifiable among all other items
		- Consists of a key-value pair
	- Attributes: A fundamental data element that does not get broken down further
	- Partition Key (hash key): A simple primary key
	- Sort Key (optional): How items that share same partition key are sored w/in the timestamp
		- Used to make groupings of data (e.g., timestamps)
	- Composite primary keys are the combination of the partition key and the sort key
## Data Warehousing
- Separating read-heavy operations across a full dataset from an application's transactional database which focuses on fast reads and writes in a smaller set of records
- Data warehouses are relational databases that are online analytical processing databases
- [[AWS Managed Services|Redshift]] is the AWS data warehouse solution
	- Open source that is optimized for high performance and analysis of massive datasets
## Database Autoscaling
![[Pasted image 20240923120827.png]]
