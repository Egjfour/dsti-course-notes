|  Course Name   |        Topic        | Professor |         Date         |         Tags         |
| :------------: | :-----------------: | :-------: | :------------------: | :------------------: |
| **Amazon AWS** | Architecture Design |   Ayoub   | 03-12 September 2024 | #CloudComputing #AWS |

# Summary
*When designing solutions, it's important to ensure that it is built to handle scale and potential disaster. Applications scale effectively when they are decoupled and use load balancers to spread work across many instances (web servers, app servers, databases, etc). It's also important to make sure that architecture deployment is well-maintained by facilitating the stack deployment through templates. This also allows for good disaster recovery to be put in place since architecture components can be automatically reprovisioned when there is an issue.*

# Key Takeaways
1. [[AWS Managed Services|Route 53]] is a [[Internet Protocol (IP) and LAN|DNS resolution service]] provided by AWS that additionally is useful for automatic failover across regions
2. Automating architecture deployment is important because manual processes do not support repeatability at scale, do not have version control, and often lead to inconsistent configurations 
3. AWS Quick Starts are gold-standard deployments that are templates created by AWS architects to allow for rapid architecture setup and deployment
4. A microservice architecture divides app functions into parts that scale and fail independently
5. Microservices are stateless

# Definitions
- Load Balancers: Automatically distribute traffic across multiple targets in one or more AZ
	- Single point of contact for clients accessing a server
- Open Systems Interconnection: A model that separates network traffic into seven layers
- Infrastructure as Code (IaC): Provisioning and managing cloud resources by defining them in a template file
- Stack: Resources which have been deployed in the overall cloud architecture
- Change Set: Preview CloudFormation changes before implementing and updating the stack
- Drift Detection: See which manual commands (if any) have been executed to resources on a stack
- Decoupling Architecture: Every element of the architecture is inside its own component
- RPO: Maximum acceptable data loss measured in time
	- Time between last backup and a disaster
- RTO: Maximum acceptable amount of time after a disaster that a business process can remain out of commission (downtime)

# Additional Resources
- [OSI Model (CloudFlare)](https://www.cloudflare.com/learning/ddos/glossary/open-systems-interconnection-model-osi/)

# Notes
## Load Balancers
- Elastic load balancer supports application, network, gateway, and classic load balancers
- Primary components are listener and target groups
- Application Load Balancer (7th layer of OSI model - Application Layer)
	- Used for HTTP/HTTPS traffic
	- Targets such as EC2 instances, containers, IP addresses, and Lambda functions
	- Supports automatic target weights
- Network Load Balancer (4th layer of OSI model - Transport Layer)
	- TCP, UDP, TCP_UDP, and TLS protocols
	- Ultra-low latency
	- Millions of requests per second and routes connections to targets such as EC2 instances, containers, Application Load Balancers, and IP addresses
- Gateway Load Balancer (3rd layer of OSI model - Network Layer)
	- Single entry and exit point for applications to route towards things like firewalls, intrusion detection and prevention systems, and deep packet inspection systems
	- Used to improve security, compliance, and policy controls
- Classic Load Balancer (4th and 7th layers of OSI model - Transport and Application)
	- Basic load balancing across multiple EC2 instances, and it operates at both the application level and network transport level
	- HTTP, HTTPS, TCP, and SSL
	- Older implementation that is <mark style="background: #FFB86CA6;">no longer recommended for use</mark>
## Infrastructure as Code (Iac)
- Creating templates to provision and manage cloud resources
- Rapid deployment with configuration consistency, automatic propagation of changes to the stack, and deletion of the stack
- Provides for version control which gives rollback capabilities
	- Uses AWS Code Commit or Github
- AWS CloudFormation is the simplified service for the creation and management of templates to launch stacks of resources ("CloudFormation stacks")
	- Templates are written as either YAML or JSON documents
- Many AWS managed services use CloudFormation
	- Elastic Beanstalk, Quick Starts, Serverless Application Model (SAM), Amplify, and Cloud Development Kit (CDK)
- CloudFormation Template Anatomy
	- **Format Version**: CloudFormation template version (Not API or SAM version)
	- **Description**: This section includes a text string that describes the template and must always follow the template Format Version section.
	- **Metadata**: Objects that provide additional information about the template
	- **Parameters**: Values to pass to your template at runtime (when you create or update a stack.
	- **Rules**: Validates a parameter or a combination of parameters passed to a template during a stack creation or stack update.
	- **Mappings**: Mapping of keys and associated values that you can use to specify conditional parameter values, similar to a lookup table.
	- **Conditions**: Conditions that control whether certain resources are created or whether certain resource properties are assigned a value during stack creation or update.
	- **Transform**: For serverless applications, the Transform section specifies the version of the AWS SAM to use. When you specify a transform, you can use AWS SAM syntax to declare resources in your template.
	- **Resources** <mark style="background: #FFB86CA6;">(required): This section specifies the stack resources and their properties, such as an EC2 instance or an S3 bucket</mark>. ONLY REQUIRED SECTION
	- **Outputs**: This section describes the values that are returned whenever you view your stack's properties.
- CloudFormation also has Designer, a UI-based template generator
- Change Sets help ensure that changes to the stack are desired by letting you preview changes
- Drift Detection shows detailed reports of resource-level configuration changes from the template
	- Does not have the ability to resolve any issues
## Decoupling
- When elements are tightly coupled (connected directly to each other) scaling and failure management is more difficult
- Between architecture tiers, load balancers decouple elements since they direct traffic automatically to new resources during scaling/failover
- Even entire tiers of an architecture (application tier for example) can be decoupled into microservices
	 ![[Pasted image 20240926123838.png]]
	 - The anti-pattern above is highly susceptible to problems in unrelated elements impacting each other
 - In a microservices architecture, different app servers would have many different microservices which increases availability even as one microservice has issues
	  ![[Pasted image 20240926124113.png]]
## Serverless
- Runtime is managed by AWS and payment model is based on service usage for really short (tens of milliseconds) lengths of time
- Suitable for [[Monitoring and Events|event-driven]] and microservices architecture
 ![[Pasted image 20240926214817.png]]
- Microservice patterns
	- RESTful APIs (API Gateway calls lambda which calls a serverless data store)
		- Lambda functions have a max of 15 minutes duration
	- Containers (API gateway calls an app load balancer which calls Fargate which calls a serverless data store)
		- Good option if a microservice requires more than 15 minutes to complete
	- [[Data Ingestion and Engineering|Streaming]] (Kinesis calls lambda which calls a serverless data store)
## Disaster Recovery
- Important to have a business continuity plan that outlines maximal acceptable data loss (RPO) and maximal acceptable downtime (RTO)
- Disaster recovery should span multiple regions
	- Use [[Data Storage (S3 and Caching)|cross-region replication]]
- Block storage on EC2 instances can be backed up using volume snapshots (EBS) or File System Replication (EFS or FSx)
	- Uses AWS DataSync
- Custom [[Computation (EC2, Lambda, Containers)|AMIs and container images]] allow for fast recovery and redeployment of compute resources
	- Especially true when combined with Autoscaling groups (EC2) or an Elastic Container Service cluster (Containers)
- Route53 can perform health checks using global endpoints and perform automated failover
- Recovery Patterns
	- Backup and Restore: Data is backed up and sent offsite/to other regions regularly
		- Long time to recover but low cost
		- AWS Storage Gateway let on-prem apps connect to cloud storage using a VM or hardware gateway appliance
	- Pilot Light: Minimal backup version of the environment is always running
		- Faster recovery than backup and restore because core system elements are always running
	- Warm Standby: Similar to pilot light but with more resources already running
		- Scaled-down version of a fully functional environment always running
		- Can also use the secondary system for non-production work when primary environment is working
	- Multi-Site: A complete, fully provisioned secondary environment is always running
		- Most expensive but fastest recovery time
	 ![[Pasted image 20240927141912.png]]