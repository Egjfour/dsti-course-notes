|      Course Name       |    Topic     |  Professor  |      Date       |       Tags       |
| :--------------------: | :----------: | :---------: | :-------------: | :--------------: |
| **Big Data Ecosystem** | Apache Spark | Joe Sanchez | 05-06 juin 2025 | #Data_Management |

[Class Video Link](URL)

# Summary
*A 3-4 sentence description of what was learned in italics*

# Key Takeaways
1. Spark, unlike [[Hadoop, MapReduce, and Hive|Hive/MapReduce]], is faster because all data for calculations (including intermediate steps) is persisted in the cluster RAM
2. The lowest level building block in Spark is the Resilient Distributed Dataset (RDD)
3. RDDs are immutable and can be persisted in memory for reuse
4. Programming language does not matter from a speed standpoint if using abstractions like Spark dataframes and Spark SQL, but at the RDD level, Scala will always be fastest
5. The transformations within a set of Spark SQL or Spark dataframe operations are sent to the <mark style="background: #FFB86CA6;">catalyst optimizer where the logical and physical plans are determined</mark> and then used to create the actual underlying RDDs

# Definitions
- Spark: Fast, in-memory, distributed, parallel, general-purpose [[Distributed Systems Overview|cluster]] computing system
- Transformation: An operation (functional expression on a key-value pair) that is performed on a Spark dataframe/RDD
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
- Name the hyperlink in brackets then outside the brackets put the URL in parens

# Notes
## Spark Infrastructure
- Spark is an open source project managed by Apache which is strongly tied to the [[Hadoop, MapReduce, and Hive|Hadoop ecossytem]]
- Spark is fast because it operates in-memory and is distributed
- Spark is used for ETL on large datasets, streaming, and graphs on structured, semi-structured and unstructured data
- Spark connects to cluster managers (YARN, Kubernetes) to distribute resources (RAM and CPU) to applications running on a cluster
- When we write and submit code, Spark
	- Asks for resources to create the driver and executors
	- Transforms code into tasks
	- Driver sends the tasks to executors
	- Executors send status to the driver
	![[Pasted image 20250615173748.png]]
## Data Structures and Operations
