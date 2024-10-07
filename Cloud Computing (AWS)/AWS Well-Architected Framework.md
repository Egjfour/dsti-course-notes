|  Course Name   |     Topic      | Professor |       Date        |         Tags         |
| :------------: | :------------: | :-------: | :---------------: | :------------------: |
| **Amazon AWS** | Best Practices |   Ayoub   | 03 September 2024 | #CloudComputing #AWS |

# Summary
*The AWS Well-Architected Framework allows cloud architects to have a guide through which they can ensure they are building a well-designed solution. The 6 pillars will often likely need to be prioritized when there are conflicts, but by following AWS best practices, architects can ensure secure, resilient systems that deliver strong value. AWS also provides a self-service tool, the AWS WA Tool to help architects evaluate design decisions*

# Key Takeaways
1. The 6 main pillars of the framework
	1. Operational Excellence
	2. Reliability
	3. Performance Efficiency
	4. Cost Optimization
	5. Sustainability
	6. Security
2. Issues arise from single points of failure, lack of automation, and lack of elasticity
3. There will likely be trade-offs to prioritize among the pillars
4. When choosing a database (or any cloud) solution, one must consider many aspects and match the technology to the workload

# Definitions
- Operational Excellence: The ability to run and monitor systems that deliver business value
	- The uptime targets that companies set and report on
- Mechanical sympathy: using a tool or system with an understanding of how it best operates
	- Use the technology approach that best aligns with what we're doing
- Partition Tolerance: Does the system continue to operate despite messages being dropped/delayed
- Elasticity: The capability of a system to automatically scale its resources up or down in response to changes in demand
- Loosely Coupled Components: Different parts of a system are designed to operate independently, with minimal dependencies on one another

# Additional Resources
- [AWS Well-Architected Framework](https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html)
- [General Design Principles](https://docs.aws.amazon.com/wellarchitected/latest/framework/general-design-principles.html)

# Notes
## The 6 Pillars
#### 1. **Operational Excellence**
- **Definition**: Focuses on <mark style="background: #FFB86CA6;">running and monitoring systems to deliver business value</mark> and continually improve processes and procedures.
- **Key Practices**:
    - **Automate Operations**: Automate processes to reduce errors and increase efficiency (e.g., [[Building Resilient Architecture|infrastructure as code]]).
    - **Monitor and Improve**: Implement monitoring and alerting to detect and respond to incidents.
    - **Prepare and Evolve**: Regularly review and refine procedures, perform game days to simulate failures and improve readiness.
- **Summary**: Ensures that the workload is running efficiently and effectively, emphasizing <mark style="background: #FFB86CA6;">continuous improvement, automation, and proactive management</mark>.
#### 2. **Reliability**
- **Definition**: Focuses on ensuring that a <mark style="background: #FFB86CA6;">workload performs its intended function correctly and consistently</mark>, even when failures occur.
- **Key Practices**:
    - **Design for Failure**: Architect systems to handle failures gracefully, using techniques such as redundancy and failover.
    - **Automated Recovery**: Automate recovery processes to quickly restore operations after a failure.
    - **Test and Improve**: Regularly test recovery procedures and implement improvements to enhance reliability.
    - **Scaling and Monitoring**: Use AWS tools like [[Computation (EC2, Lambda, Containers)|Auto Scaling]] and Amazon CloudWatch to dynamically respond to changes in demand and detect potential issues.
- **Summary**: Ensures that applications can recover from failures and disruptions by designing for fault tolerance, automating recovery, and continuously monitoring and testing.
#### 3. **Performance Efficiency**
- **Definition**: Focuses on <mark style="background: #FFB86CA6;">using cloud resources efficiently</mark> to meet system requirements while maintaining high performance.
- **Key Practices**:
    - **Selection of Resources**: Choose the right AWS resources (e.g., instance types, storage options) for optimal performance.
    - **Monitoring and Review**: Continuously monitor and analyze performance metrics to identify and address bottlenecks.
    - **Optimize and Evolve**: Regularly update and optimize resources, configurations, and architectures to maintain or improve performance.
    - **Elasticity**: Use AWS services like Auto Scaling and Elastic Load Balancing to automatically adjust resources based on demand.
- **Summary**: Ensures that the application is performing efficiently by choosing the right resources, monitoring performance, and optimizing resource use.
#### 4. **Cost Optimization**
- **Definition**: Focuses on managing costs by optimizing and controlling expenditures while still delivering high value.
- **Key Practices**:
    - **Right-Sizing Resources**: <mark style="background: #FFB86CA6;">Match the supply of resources with actual demand to avoid over-provisioning</mark>.
    - **Cost Monitoring**: Use AWS Cost Explorer, AWS Budgets, and AWS Cost and Usage Reports to monitor and analyze spending.
    - **Usage of Pricing Models**: Take advantage of pricing models such as [[Computation (EC2, Lambda, Containers)|Reserved Instances, Spot Instances, and Savings Plans]] to reduce costs.
    - **Eliminate Waste**: Identify and eliminate underutilized resources and wasteful spending.
- **Summary**: Focuses on minimizing costs while maximizing value by using the right resources, monitoring expenses, and leveraging cost-effective options.
#### 5. **Security**
- **Definition**: Focuses on protecting data, systems, and assets to take advantage of cloud technologies' security features.
- **Key Practices**:
    - **Identity and Access Management**: Implement strong access controls, such as using [[Identity and Access Management (IAM)|AWS IAM roles and policies]].
    - **Data Protection**: Encrypt data at rest and in transit, and use secure storage and transfer mechanisms.
    - **Incident Response**: Develop and regularly test incident response plans to handle security breaches.
    - **Continuous Monitoring**: Use AWS services like Amazon GuardDuty, AWS CloudTrail, and AWS Config to monitor, detect, and respond to security threats.
- **Summary**: Prioritizes protecting data, systems, and assets by <mark style="background: #FFB86CA6;">implementing access control, encryption, monitoring, and incident response.</mark>
#### 6. **Sustainability**
- **Definition**: Focuses on minimizing the environmental impact of your workloads by optimizing for energy efficiency and reducing waste.
- **Key Practices**:
    - **Maximize Utilization**: Use efficient instance types and optimize workloads to make the best use of compute and storage resources.
    - **Improve Energy Efficiency**: Select [[AWS Physical Architecture|regions]] that use renewable energy and optimize data storage and processing to reduce energy use.
    - **Optimize Workloads**: Reduce waste by continuously optimizing and evolving your applications to consume fewer resources.
    - **Reduce, Reuse, Recycle**: Implement practices that reduce the need for new resources, such as using [[Computation (EC2, Lambda, Containers)|spot instances]] and consolidating workloads.
- **Summary**: Ensures that your workloads are as energy-efficient as possible, optimizing for both performance and sustainability.

### Summary

| Pillar                     | Definition                                                                     | Key Practices                                                                               |
| -------------------------- | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------- |
| **Operational Excellence** | Running and monitoring systems to deliver business value and improve processes | Automate operations, monitor and improve, prepare and evolve                                |
| **Reliability**            | Ensuring a workload performs its intended function consistently                | Design for failure, automated recovery, scaling, monitoring                                 |
| **Performance Efficiency** | Using resources efficiently while maintaining high performance                 | Right resource selection, monitoring, optimizing, elasticity                                |
| **Cost Optimization**      | Managing costs and optimizing spending                                         | Right-sizing, cost monitoring, efficient pricing models, eliminating waste                  |
| **Security**               | Protecting data, systems, and assets using cloud security features             | Identity management, data protection, incident response, continuous monitoring              |
| **Sustainability**         | Reducing environmental impact and maximizing energy efficiency                 | Maximize utilization, improve energy efficiency, optimize workloads, reduce/reuse resources |
- The AWS Well-Architected Tool
	- Self-service tool that provides you with on-demand access to current AWS best practices
	- You define your workload and answer a series of questions in the areas of operational excellence, security, reliability, performance efficiency, and cost optimization. The AWS WA Tool then delivers an action plan with step-by-step guidance on how to improve your workload for the cloud.
## CAP Theorem
- The **CAP Theorem** (Consistency, Availability, Partition Tolerance) states that in a distributed system, it is <mark style="background: #FFB86CA6;">impossible to simultaneously guarantee all three properties:</mark>
	1. **Consistency (C):** Every read receives the most recent write or an error.
	2. **Availability (A):** Every request receives a response, without guarantee that it contains the most recent write.
	3. **Partition Tolerance (P):** The system continues to operate despite network partitions.
- Given the theorem, most distributed systems must choose between **Consistency** and **Availability** while ensuring **Partition Tolerance** since network partitions are assumed to occur eventually.
## Best Practices for Solution Building
- Scalability
	- Use solutions like autoscaling in EC2 to create more capacity
	- Monitoring solutions like CloudWatch help with this
- Environment Automation (infrastructure as code)
	- Rapid deployment of duplicate environments
	- Reduce configuration errors
	- Propagate changes consistently to all stacks (templates)
	- Respond to failures quickly
	- Treat Resources as Disposable
		- Automate deployment with identical configurations
		- Stop resources not in use
		- Test updates on new resources
- Use Loosely Coupled Components
	- Web servers should not connect directly to app servers
	 ![[Pasted image 20240907110335.png]]
- Produce Services not Servers
	- Use the full breadth of the AWS services
	- Consider containers or serverless solutions
	- Message queues handle communications between applications
	- Static web assets (images) can be stored off-server (Amazon S3 for example)
	- Authentication and user state storage can be handled by managed AWS services
- Choose the right database solution
	- Consider and <mark style="background: #FFB86CA6;">predict the read/write, total storage, typical object size, durability, latency, maximum concurrent users, query nature, and required strength of data integrity controls</mark>
	- SQL is good for security and balances the CAP tradeoff
	- NoSQL is good for specific needs
		- Document -> Research
		- Graph -> Data Science
		- Column-Based -> Writing
		- Key-Value -> Small Data (local storage & caches)
	- Blob storage is good for large disk images that have no defined structure
		- images, videos, etc
- Avoid single points of failure
	- This does not mean we need to duplicate every component of the architecture
	- Use automated solutions that only launch components when needed (depending on SLA)
	- [[Data Storage (S3 and Caching)|Data replication]] in a secondary database can ensure resilience
- Optimize for Cost
	- Are the resources the right size and type?
	- What metrics can be monitored?
	- How/when can resources be turned off?
	- Would it be beneficial to use a managed service?
- Use Caching
	- Minimize redundant [[Cloud Overview|retrieval operations which cost money]]
	- Amazon CloudFront will cache retrievals and send data to an [[AWS Physical Architecture|edge node]] closest to the user
- Security
	- Log access, implement MFA, Isolate parts of the architecture, encrypt data, and automate deployment
	- Encrypt data at rest using client and server side encryption