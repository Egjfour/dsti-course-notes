|  Course Name   |              Topic               | Professor |       Date        |         Tags         |
| :------------: | :------------------------------: | :-------: | :---------------: | :------------------: |
| **Amazon AWS** | AWS Global Physical Architecture |   Ayoub   | 03 September 2024 | #CloudComputing #AWS |

# Summary
*Amazon maintains a massive global network of physical hardware which powers the cloud. This hardware is stored in data centers which are segmented into availability zones which are designed to be isolated from incidents (fire, power issue, etc). Multiple availability zones make up a region which is what resources are hosted within. On the cloud, Amazon is responsible for the security and maintenance of the hardware, but the customer is responsible for their own security within the cloud.*

# Key Takeaways
1. It is recommended to [[AWS Well-Architected Framework|replicate across availability zones for consistency]]
2. The customer is responsible for security ***in*** the cloud, and Amazon is responsible for security ***of*** the cloud
3. Moving data within the AWS backbone is significantly faster and more secure than uploading/downloading

# Definitions
- Region: Geographical Area containing 2 or more availability zones
	- US-east-1 (N. Virginia)
	- US-east-2 (Ohio)
- Availability Zone: A group of one or more data centers within a region designed for fault isolation
- Local Zones: An extension of a region that allows for latency-sensitive portions of applications to be run closer to large population, industry, and IT centers <mark style="background: #FFB86CA6;">where no Regions exist today</mark>
- Data Center: The physical location where the hardware that stores and processes data resides
- Point of Presence: A combination of edge locations and mid-tier regional edge caches
- Edge Location: AWS data centers and servers located close to customers and designed to deliver services with the lowest latency possible
- Regional Edge Cache: AWS data centers between the origin server and the edge location that have a longer cache
- Client-side encryption: End-to-end protection for your object, in transit and at rest, from its source to storage
- Server-side encryption: Unencrypted data is sent through a secure pipeline and only encrypted in the server itself

# Additional Resources
- [AWS Infrastructure Documentation](https://docs.aws.amazon.com/whitepapers/latest/aws-fault-isolation-boundaries/aws-infrastructure.html)

# Notes
## Global Infrastructure
- Overview
	- Regions are the highest level of the infrastructure hierarchy
		- Represent a geographical area with at least two availability zones
		- Resources are deployed within a specific region
		- Resources in AWS can communicate across regions (unless those regions are in different partitions like China or the US Government)
	- Availability zones are located within a given region and provide <mark style="background: #FFB86CA6;">fault isolation among resources</mark> across availability zones
		- An Availability Zone is one or more discrete data centers with<mark style="background: #FFB86CA6;"> independent and redundant power infrastructure, networking, and connectivity</mark> in an AWS Region.
		- All Availability Zones in a Region are interconnected with high-bandwidth, low-latency networking, over fully redundant, dedicated metro fiber
	- Data Centers are where the physical hardware for the AWS cloud within an availability zone actually lives
	 ![[AWS Physical Architecture Image.jpg]]
- Additional Elements
	- Local zones
		- Latency-sensitive portions of applications delivered closer to users
	- Points of Presence
		- PoPs host Amazon CloudFront, a content delivery network (CDN); Amazon Route 53, a public Domain Name System (DNS) resolution service; and AWS Global Accelerator (AGA), an edge networking optimization service
		- Allow caching of popular data at mid-tier regional caches
## Shared Security Model
- Amazon is responsible for the <mark style="background: #FFB86CA6;">security of the foundation services</mark>
	- Compute, storage, networking, databases, and the global physical infrastructure
- The customer is responsible for the security of their use of the services
	- Identity and Access Management
	- Customer Data
	- Applications
	- Platform
- Because the customer is responsible for so much the [[AWS Well-Architected Framework|well-architectured framework]] strongly recommends employing the principle of least privilege
- Even though server-side encryption is provided in AWS, it is recommended still to perform client-side encryption