|      Course Name       | Topic | Professor  |     Date     |       Tags       |
| :--------------------: | :---: | :--------: | :----------: | :--------------: |
| **Big Data Ecosystem** | NiFi  | Mori Huang | 12 juin 2025 | #Data_Management |

[Class Video Link 1](https://dstisas-my.sharepoint.com/personal/blaise_pascal_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fblaise%5Fpascal%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20250612%5F095133%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Ee116215e%2D3236%2D4cc1%2Dbb6e%2D107cc476663e)
[Class Video Link 2](https://dstisas-my.sharepoint.com/personal/blaise_pascal_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fblaise%5Fpascal%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20250612%5F095133%2DMeeting%20Recording%201%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Ef4b54ac1%2D67c9%2D4369%2Dac29%2D48b93dbf7879)

# Summary
*NiFi is a data warehousing solution developed by the NSA and managed under the Apache project to provide distributed ETL and ELT capabilities in a more secure way and user-friendly (low-code) way. NiFi maintains data in the Java Virtual Machine as a FlowFile which makes its way through various processors where it undergoes different transformations. While there are over 400 processors in the base NiFi library, we can extend the capabilities with .jar files as well. However, NiFi is primarily for moving data between systems with light transformations. Expensive [[Spark|wide transformations]] should be handled elsewhere.*

# Key Takeaways
1. NiFi handles the flow of data between systems
2. Handles both batch and [[Streaming Data (Spark & Kafka)|streaming]] workloads including Kafka
3. The NiFi registry handles git-style [[Version Control (Code, Data, and Model)|version control]] for pipelines
4. NiFi can be used to do <mark style="background: #FFB86CA6;">light data transformations and data enrichment</mark>, but heavier transformations such as complex joins are better left to more specialized tools

# Definitions
- Extract, Transform, Load (ETL): Data is fetched/retrieved from source and undergoes transformations (validation, cleaning, joining, etc.) BEFORE being loaded to the FINAL target 
	- INSIGHT ProfitBuilder
- Extract, Load, Transform (ELT): Data is fetched/retrieved from source and is dumped into a target system where jobs are then run to further transform the data
	- Clients extract from their ERP and dump files to the SFTP for INSIGHT transformations
- Zero-Leader Clustering: Each node performs the same tasks on the data but each operates on a different set of the data
- FlowFile: A data object moving through the system that contains attributes (metadata), a payload (content), and provenance information
- Processor Relationship: Output state for a processor. Not the same for each processor but some are commonly available such as terminate, retry, success, and failure

# Additional Resources
- [Announcement of NiFi Publication by the NSA](https://www.forbes.com/sites/adrianbridgwater/2015/07/21/nsa-nifi-big-data-automation-project-out-in-the-open/)
- [NiFi Architecture Overview](https://nifi.apache.org/docs/nifi-docs/html/overview.html#nifi-architecture)
- [Crontab Guru - Establish CRON cadence](https://crontab.guru/)
- [NiFi Expression Language](https://nifi.apache.org/docs/nifi-docs/html/expression-language-guide.html)

# Notes
## NiFi Solution Overview
- Data warehousing solution 
- Provides security at many levels with fine-grained control
	- System to system, user to system, multi-tenant
- Easy to use - low/no-code interface with guaranteed delivery live indicators
	- Makes data provenance very easy to track
- NiFi is written in Java, so we can build customized processors
- NiFi nodes are [[Databases|horizontally scalable]] on a cluster and are managed by [[Hadoop, MapReduce, and Hive|Zookeeper]]
	- Single node as the Cluster Coordinator, and failover is handled automatically
	- Unlike [[Streaming Data (Spark & Kafka)|Kafka]], NiFi uses zero-leader clustering
- Data storage and integrity are managed in the storage layer
	- FlowFile Repository stores the <mark style="background: #FFB86CA6;">attributes/metadata</mark> of the file
	- Content Repository stores the <mark style="background: #FFB86CA6;">payload</mark> (file content)
	- Provenance Repository stores the <mark style="background: #FFB86CA6;">data provenance</mark> for the flow file
 ![[Pasted image 20250620085509.png]]
## Components of a NiFi Flow
- FlowFile
	- Data object moving through the system and is made up of three parts
		- Attributes: metadata about the file
		- Payload: content of file
		- Provenance: information about the movement of the data through the system
- FlowFile Processors
	- Single unit of work in the system
	- Performs an <mark style="background: #FFB86CA6;">action with the data</mark> such as fetching, validation, routing, etc.
- Connection
	- Links between processors which act as [[Monitoring and Events|queues]]
- Funnel
	- Combine data from several connections into a single one
	- Also can act as an endpoint for development/debugging
- Process Group
	- Organize components/flows into logic groups
	- Facilitate creation of security policies
- Remote Process Group
	- Treats external NiFi clusters as just another process group locally
- Input/Output Ports
	- Pipe FlowFiles into/out of process groups
- Labels
	- Allow for quick flow documentation
	- Look like a big sticky note on the user interface
## Configuration Options - Processors and Connections
- Processor Settings
	- Penalty Duration: An amount of <mark style="background: #FFB86CA6;">time added to the FlowFile</mark> that indicates how long to pause the processing of that FlowFile after a problem has been encountered
	- Yield Duration: The amount of <mark style="background: #FFB86CA6;">time a processor will pause</mark> execution if problem is encountered
	- Bulletin Level: Verbosity of bulletins shown in the user interface (default is WARN - warnings and errors are shown)
- Processor Scheduling
	- Scheduling can either be a timer or a CRON job
	- Concurrent Tasks states how many FlowFiles can be processed at the same time
	- Run Duration: How long a processor runs before passing FlowFiles to next destination
		- Dial to control latency vs. throughput
- Processor Properties (specific to EACH processor)
	- Controller Services: Reading/Writing different filetypes or database connectors
		- Processor Group level mechanisms to handle various files
	- NiFi Expression Language
		- Process and manipulate FlowFile attributes
		- ONLY works with a RouteOnAttribute processor
- Connection Configuration
	- FlowFile Expiration: Data can be aged out of the flow
		- default value of 0 means the file never expires
	- Available Prioritizers: Defaults to *OldestFlowFileFirst* (oldest in dataflow).
	- Back Pressure: Provides both object and total size thresholds.
	- Load Balance: Distribute the load across the cluster.