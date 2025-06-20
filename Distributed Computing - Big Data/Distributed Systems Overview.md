|      Course Name       |              Topic               |  Professor  |     Date     |       Tags       |
| :--------------------: | :------------------------------: | :---------: | :----------: | :--------------: |
| **Big Data Ecosystem** | Big Data and Distributed Systems | Joe Sanchez | 02 juin 2025 | #Data_Management |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/blaise_pascal_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fblaise%5Fpascal%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20250602%5F095456%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E2413f3bf%2Dd3e9%2D4438%2Db1ac%2Dd366bfcd3654)
[Final Day Review Video Link](https://dstisas-my.sharepoint.com/personal/blaise_pascal_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fblaise%5Fpascal%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20250613%5F095106%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Ed47833d2%2D04fa%2D41b3%2D9769%2D3c6aaa08b037)

# Summary
*Distributed systems are needed in a modern data environment because the required volume, velocity, and variety of data that needs processed is too large, too quick, and too vast to handle on single machines. These distributed systems allow for horizontal scaling that is partition tolerant for many different workloads including batch processing and streaming.*

# Key Takeaways
1. Distributed systems must have partition tolerance with respect to the [[Data Storage (S3 and Caching)|CAP theorem]]
2. Big data clusters are organized into a master-slave (worker) model

# Definitions
- Big Data: The need to process data across multiple devices due to the <mark style="background: #FFB86CA6;">volume, velocity, or variety</mark> of incoming data
- Cluster: A group of connected computers which can be viewed as a single system

# Additional Resources
- [Distributed Systems Overview](https://www.geeksforgeeks.org/computer-networks/what-is-a-distributed-system/)

# Notes
## Why Big Data
- Big data systems are necessary because in the modern world, we have massive amounts of data which needs to be processed
- Such data may not be able to be processed efficiently by a single machine or would require [[Databases|vertical scaling]] to a scale which is cost prohibitive
	- Distributed systems provide for [[Databases|horizontal scaling]] to build a cluster
- Data size isn't the only concern of a big data system - V's are what these systems are used for
	- Volume: Data which is too great in size to fit in RAM or an [[Relational Database Management System|RDBMS]]
	- Velocity: Speed at which we must process data or deliver results
		- Credit card processing
	- Variety: Handling and processing of unstructured data which takes more compute to process
- Big data is useful not just for large enterprises specializing in data but for normal businesses to extract the value from their data
	- These systems let us build a [[Data Ingestion and Engineering|data lake]] to gather data from all around the company
## General Architecture
- Distributed systems are organized into clusters
- Inside a cluster, nodes determine the function of specific architecture
	- Clusters follow a master-worker architecture
 ![[Pasted image 20250614161754.png]]