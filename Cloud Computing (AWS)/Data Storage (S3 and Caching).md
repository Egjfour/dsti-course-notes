|  Course Name   |   Topic    | Professor |          Date          |         Tags         |
| :------------: | :--------: | :-------: | :--------------------: | :------------------: |
| **Amazon AWS** | S3 Buckets |   Ayoub   | 04 & 10 September 2024 | #CloudComputing #AWS |

# Summary
*Amazon AWS offers an object storage solution with the Simple Storage Solution (S3). S3 organizes data into region-specific buckets where each object is uniquely named. There are many options for data upload/download as well as how the data is stored on the physical AWS infrastructure. These choices are largely informed by needed access patterns and data retention requirements. Caching data can also be used to increase performance and cost of retrieving regularly accessed data by using a content delivery network.*

# Key Takeaways
1. S3 Buckets are lacking in terms of [[AWS Well-Architected Framework|partition tolerance]] as it relates to the CAP Theorem
2. S3 is an <mark style="background: #FFB86CA6;">object storage service</mark> that allows for virtually unlimited amounts of unstructured data
3. Objects in S3 are encrypted by default using [[AWS Physical Architecture|server-side encryption]]
4. Versioning is enabled at the bucket-level and disabled by default
5. Transfer acceleration improves speeds for cross-country transfer of large datasets by using [[AWS Physical Architecture|edge locations in CloudFront]]
6. AWS ensures read-after-write consistency for all GET, PUT, LIST, and DELETE
	![[Pasted image 20240908144149.png]]
7. Caches are optimized for reading since they are key-value 
 
# Definitions
- Block Storage: Fixed-sized blocks of data on disk that can be retrieved with a unique id and amended independently of the rest of the data
	- Ultra-low latency applications (like INSIGHT lookup service)
- File Storage: Data in a hierarchical structure
	- Windows File Explorer
- Object Storage: Highly unstructured data that is identified with a unique ID and metadata
	- Photos, Videos, logs
	- Object storage for photos contains metadata regarding the photographer, resolution, format, and creation time
- Lifecycle: A rules-based procedure that automatically moves data into different storage classes
	- Ex: Move any noncurrent version of a file to glacier deep archive after 30 days
- Caching: Temporary high-speed storage layer that allows for faster access by storing data closer to the user
- Elasticache Node: A fixed-size chunk of network-attached RAM
- Lazy Loading: Data is only loaded to cache when actually requested
- Write-Through: Update the cache immediately after the database

# Additional Resources
- [Block Storage Explanation (AWS)](https://aws.amazon.com/what-is/block-storage/)
	- Includes definitions and links to other storage types as well

# Notes
## Amazon Simple Storage Solution (S3) Overview
- Amazon S3 is an object-based storage solution that allows for storing massive amounts of unstructured data
	- Single-object limit is 5TB
	- Objects have a key, version ID, metadata, and sub-resources
- An S3 bucket has a <mark style="background: #FFB86CA6;">unique name with a region-specific endpoint</mark>
	 ![[Pasted image 20240908111911.png]]
- Prefixes can be used in an S3 bucket to imply a folder structure
- S3 provides durability
	- 11 9s concept: Every year, there is a 0.000000001 percent chance of losing an object
	- AWS stores data redundantly across many devices in the same region
	- Data integrity is preserved with checksums
- S3 provides availability
	- 99.99% access to data when it is requested (4 nines)
	- AWS is scalable as well since there is virtually unlimited storage capacity
- S3 provides high performance
	- Can perform thousands of transactions per second
## Data Upload Options
- AWS management console
	- Max upload is limited to 160 GB
	- Wizard-based approach with ability to drag and drop
- AWS CLI
	- Terminal command prompt or from a script
	- No upload limits (except 5TB object size)
- AWS SDK
	- Wrapper libraries for CLI commands in different programming languages
- S3 REST API
	- A [[Cloud Overview|REST API]] is provided which allows for PUT requests against an S3 bucket
	- Write permissions on the bucket requested are necessary
- Multi-part data upload
	- AWS cloud automatically segments the data into independent parts
		- Each part is a contiguous portion of the data
	- This is <mark style="background: #FFB86CA6;">automatically handled by AWS.</mark> However, the API offers fine-grained control like chunk size options 
	- Benefits:
		- Parts are uploaded in parallel to improve throughput.
		- Smaller part size minimizes the impact of restarting a failed upload due to a network error
		- Pause and resume object uploads. Upload must either complete or be terminated by the user
		- Begin an upload before you know the final object size: You can upload an object as you are creating it.
- Transfer acceleration
	- Use edge locations to improve speed for data transfer of large objects across the world
	- Uses the AWS CDN (Content Distribution Network), CloudFront
- Transfer Family (a fully-managed option from AWS)
	- Allows for SSH, SFTP, FTP, FTP Secure, and Applicability Statement for transfer into or out of S3 buckets and/or the Elastic File System
	- No upfront costs, only pay for what is used
	- [[Cloud Overview|Serverless]] file transfer workflow that can setup, run, automate, and monitor
## Storage Classes
- General purpose offers high durability and availability for frequently-accessed resources
	- Good for standard workloads that need low latency and high throughput
- Intelligent Tiering helps reduce costs at the object level by looking at access patterns and <mark style="background: #FFB86CA6;">moving data to the correct storage class automatically</mark>
	- No performance impact, retrieval fees, or operational overhead
	- Good to use for virtually any workload, especially data lakes, data analytics, new applications, and user-generated content
- Infrequent Access class types offer a less costly storage option but have a higher retrieval cost
	- Good for older digital images or older log files
	- Has a <mark style="background: #FFB86CA6;">30-day minimum storage requirement</mark> and higher retrieval costs but much lower storage costs
	- An even lower cost to Standard Infrequent Access is Single Zone Infrequent Access where data is only maintained in one availability zone
		- Good for data that can be easily replicated or for replications of data from other regions
- Archive
	- Meant for extremely infrequently accessed data
	- Some options allow for fast retrieval (S3 Glacier Instant) while others take longer but have even lower storage costs
		- Glacier Flexible Retrieval balances these with asynchronous data retrieval in minutes at no cost
			- Ideal solution for backup, disaster recovery, and offsite data storage needs
		- 90-day minimum storage requirements for Glacier Instant and Glacier Flexible
	- S3 Glacier Deep Archive is the lowest-cost storage class in Amazon S3
		- Good for long-term retention of regulatory required data
		- 180-day minimum storage requirements
	- AWS Outputs (a fully-manages on-prem hardware solution) allows for instant access with data on-premises
 ![[Pasted image 20240908140954.png]]
## Versioning
- Prevents objects from accidental overwrites and deletes
- When you use the DELETE command to remove an object, all versions remain in the bucket, and Amazon S3 inserts a delete marker for the version specified
- <mark style="background: #FFB86CA6;">If the most recent version has a delete marker, a GET operation fails</mark>
- A hard delete can be used to permanently delete an object using a version ID
## Security and Access
- S3 supports cross-origin resource sharing (CORS)
	- Accessing a static website that is stored in an S3 container
	- To allow cross-origin requests, a CORS configuration is created and attached to the bucket
		- This XML config file specifies what operations are allowed from which domains and any other operation-specific information
- Security Configurations
	- All buckets and objects are private and protected by default
	- Server-side encryption is enables by default with SSE-S3 encryption as default
- Tools for security

| **Tool**                    | **Description**                                                                                                       |
| --------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| Block Public Access feature | Makes buckets inaccessible to the public                                                                              |
| AWS IAM policies            | Authenticates users by using IAM                                                                                      |
| Bucket policies             | Defines access based on specific written rules                                                                        |
| Access control lists (ACLs) | Sets rules for access to buckets and objects (bucket policies are the preferred method for controlling bucket access) |
| Amazon S3 access points     | Configures access with names and permissions specific to each application                                             |
| Preassigned URLs            | Grants time-limited access to others with temporary URLs                                                              |
| AWS Trusted Advisor         | Provides a bucket permission check                                                                                    |
## Caching
- Caching is used to delivery regularly accessed content to users in a faster and more cost efficient way by <mark style="background: #FFB86CA6;">using a content delivery network</mark>
- Types of content cached
	- Static content like personal profiles, HTML, javascript, CSS files, images, and videos
	- Results of computationally intense calculations
	- Results of time-consuming, frequently-used of complex database queries
- Pros and Cons
	- Pros: reduce latency and cost, improve availability, alleviate load on origin source. and provide predictable performance
	- Cons: Requires addtl engineering, require someone to determine how to cache and <mark style="background: #FFB86CA6;">deal with stale data</mark>
- AWS Services for Caching
	- Cloudfront: Retrieve data from nearest edge location (static content only)
		- Each user request is reouted to CloudFront edge servers
		- Web Application Firewall and AWS shield help prevent against DDoS attacks
		- Time to live setting for how long the content should be stored at the edge node before having to re-request from the origin server
		- Combined with AWS Elastic Transcoder or the Elemental Media Converter, video streaming is possible
		- Regional edge caches are fewer and farther away, but have larger cache memories for less popular content
	- Elasticache: Retrieve content from an in-memory database layer
		- Can be used with any type of database
		- Fully-managed, key-value, in-memory datastore that sits between an app and origin datastore
		- Supports both the memcached and redis engines
			- Memcached is better for basical models and many concurrent operations with multithreading
			- Redis is used for complex data types (strings, hashes, lists, sets), key store persistence, sorting in-memory datasets, and [[Building Resilient Architecture|pub/sub message subscribing]]
- Handling Stale Data
	- Lazy Loading (update cache after the data is requested)
		- Cache only has data the application requests
		- Requires a programmatic strategy to handle keeping the cache up to date
	- Write-Through (update cache immediately after database)
		- Data will most likely be found in the cache
		- Increase in cost to store data in-memory that may not be used
