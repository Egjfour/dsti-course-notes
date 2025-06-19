|      Course Name       |   Topic   |         Professor          |       Date        |       Tags       |
| :--------------------: | :-------: | :------------------------: | :---------------: | :--------------: |
| **Big Data Ecosystem** | Streaming | Joe Sanchez and Mori Huang | 06 & 11 juin 2025 | #Data_Management |

[Class Video Link 1](https://dstisas-my.sharepoint.com/personal/blaise_pascal_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fblaise%5Fpascal%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20250606%5F095412%2DMeeting%20Recording%201%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E1bd5aa87%2D6e3c%2D4651%2D8ada%2D1a88391ad5b1)
[Class Video Link 2](https://dstisas-my.sharepoint.com/personal/blaise_pascal_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fblaise%5Fpascal%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20250611%5F094942%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E32ed8e79%2Dbe0a%2D45cb%2D80a9%2D75a9fb33183d)

# Summary
*Streaming in a distributed system involves the handling of unbounded, continuous data like system logs. Both Spark and Apache Kafka are solutions which allow us to interact with and process such data. When processing streaming data important considerations are related to the processing window and the watermark. When producing streaming data, the producer guarantee is the main concern, and when consuming data, the consumer delivery guarantee (at most once, at least once, or exactly once) is the primary consideration.*

# Key Takeaways
1. Apache [[Spark|Spark]] offers a fault-tolerant, exactly-once processing streaming framework
2. Between event and processing time, we are more concerned with event time
3. Apache Kafka is a distributed streaming platform that lets us [[Monitoring and Events|publish and subscribe]] to streams of records which are based off events
4. Kafka splits topics into partitions (1-N partitions) and replicates topics (1-M times)
5. Producers are responsible for choosing the topic and partition to write to in Kafka
6. When a consumer accesses data, the data persists unlike in a traditional [[Monitoring and Events|queueing system]]
7. Data is always inserted to the leader partition and waits inside the broker to be consumed
8. Kafka now uses Kraft for leader selection as opposed to [[Hadoop, MapReduce, and Hive|Zookeeper]]

# Definitions
- [[Data Ingestion and Engineering|Streaming Data]]: Data which is continuously generated, small in size, and potentially coming from many sources
	- IoT, stock market, GPS positioning
- [[Cloud Overview|Streaming Architecture]]: The tools and infrastructure used to process and store continuous data
- Micro-Batch Model: Delay processing of continuous data and process collected groups at once
- Event Time: When data is actually generated
- Processing Time: When the streaming system received the data
- Watermarking: Establishing a cutoff point after which late data will no longer be processed
	- Given an event time E to a processing time P, we state that at time P, all data generated prior to E have been observed
- Key-Based Routing: Calculating a hash of the key and taking the modulus of the number of partitions to determine which partition to route to
	- Every message with the same key goes to the same partition
- Producer Guarantee: The mechanism to communicate that a message from the producer has been received and stored on the Kafka cluster
- Consumer Guarantee: Mechanism to state how 

# Additional Resources
- [Kafka Website](https://kafka.apache.org/)
- [Spark Streaming Programming Guide](https://spark.apache.org/docs/latest/streaming-programming-guide.html)

# Notes
## Streaming Overview
- Streaming is the collection, storage, and processing of unbounded data which is generated continuously and is typically small in size
	- System logs, video/audio streaming, etc
- Streaming takes information from a source, processes it with a [[Distributed Systems Overview|distributed system]] and sends it to a sink
- Unlike standard/batch data processing, streaming handles individual records or micro batches of a few records
- Stream processing frameworks
	- The <mark style="background: #FFB86CA6;">traditional method</mark> for processing stream data has sources sending records to a specific node which processes records for that node
		- This structure is high latency but introduces many single points of failure
		 ![[Pasted image 20250619180605.png]]
	- The micro batch model has less latency but all nodes execute all tasks which provides redundancy
		 ![[Pasted image 20250619181148.png]]
## Spark Streaming
- Spark provides a fault-tolerant exactly-once streaming process
- Streaming dataframes follow a very similar syntax to traditional [[Spark|Spark dataframes]]
	- Many operations are NOT supported however such as `distinct`, `take`, `limit`, chained aggregation, and certain joins
## Kafka Overview
- Kafka is based off [[Monitoring and Events|events]] happening in the physical or digital world
	- When Kafka is subscribed to an event, a message is sent to the Kafka architecture
- Message
	- Composed of <mark style="background: #FFB86CA6;">timestamp</mark>, key, value, and an optional header
	- Keys allow for ordering and timestamps are crucial
- Topic
	- All messages are sent to a topic inside a broker
	- Different topics are stored differently
	- Topics are partitioned
		- <mark style="background: #FFB86CA6;">Partitions are replicated across different brokers</mark> for fault tolerance
- Log Messaging System
	- Kafka messages are stored as a logfile which simply appends the new records
	- Data is persisted on the system even after it is accessed
- Kafka cluster architecture
	- Producers write messages to specific partitions for a topic
		- Kafka does not have any routing, so the <mark style="background: #FFB86CA6;">producer must specify the partition</mark>
		- There are many strategies for choosing partitions such as round robin or key-based
	 ![[Pasted image 20250619140623.png]]
 - Consumers and Consumer Groups
	 - All consumers within the same consumer group share the workload of the consuming task
	 - Each record is delivered to one consumer of <mark style="background: #FFB86CA6;">each consumer group</mark>
		 - 1 partition to 1 consumer
		 - If # consumers > # partitions, some consumers will sit idle
 - Data Architecture
	 - Each partition of a topic has <mark style="background: #FFB86CA6;">one server acting as the "leader"</mark>
		 - Responsible for reads and writes for the partition
		 - Handles client requests
	 - Each partition of a topic has <mark style="background: #FFB86CA6;">zero or more servers acting as "followers"</mark>
		 - Replicate the leader's data and stay in sync in case the current leader fails
	 - Controllers work at the server/broker level and are elected by the cluster
		 - Manages states of partitions and replicas
		 - Decides when a new leader for a partition is needed
		 - Handles tasks like reassigning partitions
 - Performance
	 - Not impacted by volume stored
	 - Scale of processing achieved by increasing consumer instances
## Stream Processing Dataflow Model
- Producer Guarantee
	- Acknowledge 0: Producer sends the message and moves on
		- Lowest latency but also no security the cluster has the message
	- Acknowledge 1: Producer waits for leader to acknowledge the message before moving on
		- Balanced latency/security
	- Acknowledge 2: Wait for both the leader and follower to state that they have received the message well
		- Highest latency but also most secure
- Consumer Delivery Guarantee
	- At most once
		- Messages can fail to consume
	- At least once
		- Message will deliver but there could be duplicates
	- Exactly once
		- Message only exists and is delivered one time
- Windows
	- Windows are necessary particularly when handling aggregations
	- Windows can either be <mark style="background: #FFB86CA6;">overlapping or tumbling</mark> and can be fixed, sliding, or session-based
	- An event can belong to one of more windows (in a sliding window framework for > 1)
	- When data arrives late (provided it is within the watermark) it is counted for the window of the event
		 ![[Pasted image 20250619162411.png]]
	- Watermarking allows us to establish a threshold for "too late" arrival of records