|  Course Name   |      Topic      | Professor |       Date        |                 Tags                  |
| :------------: | :-------------: | :-------: | :---------------: | :-----------------------------------: |
| **Amazon AWS** | Data Processing |   Ayoub   | 11 September 2024 | #CloudComputing #AWS #Data_Management |

# Summary
*A data engineering pipeline contains many decisions about how to best organize, create access patterns, and analyze data. Key considerations include data volume and access frequency. When processing data, it is important to know if real-time analysis of data is required or not. AWS offers many tools for all data engineering needs.*

# Key Takeaways
1. A data engineering pipeline is made up of elements ingest, process, and analyze
2. A good modern data architecture should use both [[Data Storage (S3 and Caching)|purpose-built data stores]] and data lakes

# Definitions
- Homogenous Ingestion: Move data from source to data store while keeping the same format or storage engine type
	- Extract and load directly (not transformation)
- Heterogenous Ingestion: Transformation of the data either as [[Data Warehousing (NiFi)|ETL]] or [[Data Warehousing (NiFi)|ELT]]
	- ELT is better for unstructured data going to a data lake
- Streaming Data: Streaming data is emitted at high volume in a continuous, incremental manner with the goal of low-latency processing.
- Data Lake: Data storage, a data catalog, and security access in a centralized repository for all structured and unstructured data

# Additional Resources
- [AWS Glue (AWS)](https://aws.amazon.com/glue/?nc1=h_ls)
- [Athena Overview (AWS)](https://aws.amazon.com/athena/?nc1=h_ls)

# Notes
## Data Pipelines
- Ingest: Get raw data into the cloud and pipeline
	- Homogenous and heterogenous patterns
- Process: Transform data so it is viable for analysis
	- Batch: Compute results & perform deep analysis on complete or large datasets
	- Streaming: Continuous incremental sequence of small data packets used in real-time analytics
	 ![[Pasted image 20240927122535.png]]
- Analyze: Discover details about data and build visualizations
## Batch Data Process with AWS Glue
- Glue components
	- ETL Jobs for data transformation including a no-code visual interface (Glue Studio)
	- Glue Data Catalog for data discovery and organization
	- Glue DataBrew as a no-code service for data cleaning and preparation
		- 250 pre-built transformations
	- Glue Data Quality uses statistics to recommend quality rules
		- Can monitor and send alerts when the data has deteriorated
- Can tranform data types such as csv to parquet
	- Parquet is a data format that is optimized for storage and parallel processing by storing data in a columnar fashion
## Streaming Data Process
![[Pasted image 20240927124815.png]]
- Amazon Kinesis Data Streams collects and ingests large streams of data records in real time.
- <mark style="background: #FFB86CA6;">Amazon Kinesis Data Firehose delivers near real-time streaming data to supported destinations.</mark>
- Amazon Managed Service for Apache Flink is a serverless service to query and analyze streaming data in real time.
- Amazon Kinesis Video Streams securely streams video from connected devices to AWS for analytics and other processing.
- Amazon Managed Streaming for Apache Kafka (Amazon MSK) is a fully managed Apache Kafka service that can be deployed in a VPC.
## Data Warehouse and Data Lake
![[Pasted image 20240927130525.png]]
- A data lake is implemented with a combination of AWS services like S3, Glue, Athena, and Lake Formation for management
## Parallel Processing
- Workflow
	- Split dataset into smaller parts
	- Process the parts in parallel
	- Aggregate the results
- EMR is used for cluster infrastructure management and includes Apace Hadoop applications like MapReduce and Spark
 ![[Pasted image 20240927132813.png]]
## Analysis and Visualization
- Build dashboards with QuickSight
	- Real-time application dashboards
	- Requires a separate ingestion service
- OpenSearch Service performs both ingestion and visualization capabilities
- Perform one-time SQL queries with Athena SQL