|      Course Name       |    Topic     |  Professor  |      Date       |       Tags       |
| :--------------------: | :----------: | :---------: | :-------------: | :--------------: |
| **Big Data Ecosystem** | Apache Spark | Joe Sanchez | 05-06 juin 2025 | #Data_Management |

[Class Video Link 1](https://dstisas-my.sharepoint.com/personal/blaise_pascal_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fblaise%5Fpascal%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20250605%5F095104%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E3ad9b640%2Dd248%2D4b58%2D95b8%2De9cb593da11d)

# Summary
*Spark is another distributed data framework, but with a key difference in that data is stored in-memory on the cluster allowing for much faster computations. The lowest unit of data in Spark is the RDD which chains lambda functions together to perform executions, but now, most people work with Spark dataframes via Python, R, and SQL which provide not only additional abstraction above RDDs but allow the catalyst optimizer to create an execution plan and optimize the RDDs.*

# Key Takeaways
1. Spark, unlike [[Hadoop, MapReduce, and Hive|Hive/MapReduce]], is faster because all data for calculations (including intermediate steps) is persisted in the cluster RAM
2. The lowest level building block in Spark is the Resilient Distributed Dataset (RDD)
3. RDDs are immutable and can be persisted in memory for reuse
4. Programming language does not matter from a speed standpoint if using abstractions like Spark dataframes and Spark SQL, but at the RDD level, Scala will always be fastest
5. The transformations within a set of Spark SQL or Spark dataframe operations are sent to the <mark style="background: #FFB86CA6;">catalyst optimizer where the logical and physical plans are determined</mark> and then used to create the actual underlying RDDs

# Definitions
- Spark: Fast, in-memory, distributed, parallel, general-purpose [[Distributed Systems Overview|cluster]] computing system
- Transformation: An operation (functional lambda expression on a key-value pair) that is performed on a Spark dataframe/RDD
	- `orderBy()`, `groupBy()`, `filter()`, `select()`, `join()`
- Action: Getting the results of one or many transformations for writing, display
	- `show()`, `take(10)`, `count()`, `collect()`, `save()`
- [[Data Storage (S3 and Caching)|Lazy Evaluation]]: Transformations which are only executed when an action is called
	- Polars lazy frames
- Narrow Transformation: A transformation which can be performed on a single record
	- `map()`, `flatMap()`, `mapPartition()`, `filter()`, `sample()`, `union()`
- Wide Transformation: A transformation which requires computation across several records
	- `intersection()`, `distinct()`, `reduceByKey()`, `groupByKey()`, `join()`, `cartesian()`, `repartition()`, `coalesce()`
- Spark Dataframe: In-memory, distributed table with named and typed columns which are a collection of rows

# Additional Resources
- [Narrow vs Wide Transformations](https://www.geeksforgeeks.org/data-engineering/wide-and-narrow-dependencies-in-apache-spark/)
- [Understanding the Execution Process of Apache Spark](https://medium.com/@Sanjay007/understanding-the-execution-process-of-apache-spark-4209374febb8)

# Notes
## Spark Infrastructure
- Spark is an open source project managed by Apache which is strongly tied to the [[Hadoop, MapReduce, and Hive|Hadoop ecosystem]]
- Spark is fast because it operates in-memory and is distributed
- Spark is used for ETL on large datasets, streaming, and graphs on structured, semi-structured and unstructured data
- Spark connects to cluster managers (YARN, Kubernetes) to distribute resources (RAM and CPU) to applications running on a cluster
- When we write and submit code, Spark
	- Asks for resources to create the driver and executors
	- Transforms code into tasks
	- Driver sends the tasks to executors
	- Executors send status to the driver
	![[Pasted image 20250615173748.png]]
## Data Structures
- Resilient Distributed Data (RDD)
	- The base building block of all data moving through the distributed system
	- A collection of elements (strings, arrays, dictionaries, etc.) which is fault-tolerant and partitioned across the nodes of a cluster
	- RDDs are **partitioned**:
	    - **1 partition** = **1 block** = 128 MB in HDFS
	    - **1 task** runs on **1 partition**
	    - Default = 1 partition per CPU core
	- Example: Chain transformations and use the result with an action
	```python
	rdd = sc.wholeTextFiles('hdfs://text/file/path') \
    .map(lambda x: x.split(',')) \      #transformation
    .flatMap(...) \                     #transformation
    .groupByKey(...)                    #transformation
	rdd.take(10)      # action
	```
- Abstractions exist on top of RDDs to make them more user-friendly and optimized
	- RDD operations are good because the developer has complete control, but Spark can optimize spark SQL and spark dataframe queries
	- RDDs also make are difficult to write and understand
	- Spark dataframes solve this by providing a pandas-like API which is far more performant than writing RDDs directly
		- Performance gains are achieved through using lazy evaluation on the transformations and then using the <mark style="background: #FFB86CA6;">catalyst optimizer to determine the best execution method and construct the appropriate RDDs</mark>
		- Performance gains level the playing field across languages (SQL, Python, R, and Scala spark dataframes are equally efficient to use)
 ![[Pasted image 20250619113431.png]]
## Job Execution
- Spark builds a [[Hadoop, MapReduce, and Hive|DAG]] of various stages where a stage is comprised of tasks
	- Stages are run in parallel when possible (for narrow transformations)
- Tasks are sent to executors and the end of each stage is a shuffle
 ![[Pasted image 20250619122049.png]]