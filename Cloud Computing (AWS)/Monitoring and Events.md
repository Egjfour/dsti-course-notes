|  Course Name   |      Topic       | Professor |       Date        |         Tags         |
| :------------: | :--------------: | :-------: | :---------------: | :------------------: |
| **Amazon AWS** | Cloud Monitoring |   Ayoub   | 09 September 2024 | #CloudComputing #AWS |

# Summary
*When building an architecture that is fault-tolerant, a decoupled architecture pattern which breaks application components into microservices is an effective strategy for accomplishing this. In this paradigm, components within and among layers of the architecture communicate via messages or events. AWS provides tools for this communication through their queue and notification services.*

# Key Takeaways
1. Reactive architectures allow for large amounts of data to be processed with sub-second response times and close to 100% uptime by being elastic, responsive, resilient, and message driven
2. Most DB types need [[Databases|read replicas]] to scaling and vertical scaling in a DB always takes longer and involves downtime
3. A FIFO queue guarantees exactly-once processing
4. The consumer is responsible for deleting messages in a queue
5. There is no recall capability for messages sent in the pub/sub notification service

# Definitions
- Publisher/Subscriber Design Pattern: Process messages such that a publisher makes available a message to any number of subscribers without knowledge of who is subscribed or downstream processes
- Point-to-Point Messaging (Queue): An asynchronous decoupling method that has a sending application send a message to only one specific receiving application
- Pipe: point-to-point integrations between one source and one target
- Event Bus: Routers that receive events and optionally delivers them to one or multiple targets
- Elastic Scaling: Mechanism to dynamically scale resources
- Vertical Scaling: Expand the resources that the existing server uses to increase capacity
	- Complex and time-consuming since it involves upgrading memory, storage, or processing power
- Horizontal Scaling: Increasing the number of servers that the database tuns on
	- Capacity added while database is running (no downtime to scale)
- Metric: <mark style="background: #FFB86CA6;">Time-ordered set of data points</mark> with a unit of measurement such as bytes, seconds, count, and percentage

# Additional Resources
- [Pub/Sub vs Queues](https://medium.com/@osama94/pub-sub-system-vs-queues-9a5fd872f474)

# Notes
## CloudWatch
- Collect and aggregate logs and calculate metrics across AWS services
	- Metrics are time-ordered and are stored in a repo with a namespace container
	- Metrics for different apps are not mistaken and aggregated together thanks to the namespace
- Metrics are stored separately for each region, but CloudWatch can consolidate across regions
- Alarms
	- Triggers that go to the simple notification service (SNS) or to auto-scaling policies when a particular metric passes a given threshold
- Dashboards
	- Connects to AWS Management Console dashboards and custom dashboard solutions
## EventBridge
- Process events with an event bus or pipe
- Serverless service that uses events to connect application components together
- Supports rules in the event bus to decide where to route messages
 ![[Pasted image 20240923114302.png]]
## AWS Autoscaling and AWS Application Autoscaling
- AWS Autoscaling: Manage policies across many resources
	- Amazon Aurora: Increase or decrease the <mark style="background: #FFB86CA6;">number of Aurora read replicas</mark> that are provisioned for an Aurora DB cluster
	- [[Computation (EC2, Lambda, Containers)|Amazon EC2 Auto Scaling]]: <mark style="background: #FFB86CA6;">Launch or terminate EC2 instances</mark> by increasing or decreasing the desired capacity of an Auto Scaling group
	- Amazon Elastic Container Service (Amazon ECS): Increase or decrease the <mark style="background: #FFB86CA6;">desired task count</mark> in Amazon ECS
	- Amazon DynamoDB: Increase or decrease the <mark style="background: #FFB86CA6;">provisioned read and write capacity</mark> of a DynamoDB table or a global secondary index.
- Application Autoscaling: Scale multiple resources for applications outside of EC2
	- Able to scale AWS Autoscaling (really just a superset of AWS Autoscaling)
	- Similar to Amazon EC2 Auto Scaling groups in that you can use Application Auto Scaling to automatically scale with target tracking, [[Computation (EC2, Lambda, Containers)|step]], and scheduled scaling policies
## Queues (Amazon Simple Queue Service (SQS))
- Sending application (producer) sends a message to exactly one receiving application (consumer)
- Messages are stored in a message queue until a consumer uses a pull mechanism
- Messages can be up to 256KB and can contain XML, JSON, and unformatted text
- Messages remain in the queue until the consumer deleted them or they receive the queue's message retention period (default is 4 days; max is 14 days)
- Standard and FIFO Queues
	- Standard provides:
		- At-least-once delivery: A message is delivered at least once, but occasionally more than one copy of a message is delivered.
		- Best-effort ordering: Occasionally, <mark style="background: #FFB86CA6;">messages might be delivered in an order that is different from the order in which they were sent.</mark>
		- Nearly unlimited throughput: Standard queues support a nearly unlimited number of API calls per second for each API operation
	- FIFO provides:
		- First-in-first out delivery: Messages are delivered in the exact order that they are sent.
		- Exactly once processing: <mark style="background: #FFB86CA6;">Messages are processed exactly once.</mark>
		- high throughput: FIFO queues support up to 300 API calls per second for each API operation. When you batch 10 messages per operation (maximum), FIFO queues can support up to 3,000 API calls per second.
- Configuration Options
	- Polling type (short vs long) determines how often consumers ask for messages 
		- Short polling (receive message wait time of 0) is default
		- Long polling has a max value of 20 seconds
		- Short polling increases number of responses (this cost) due to messages even if there is no message found
		- Long polling provides less frequent responses but is cheaper because it reduces number of empty receives
	- Message Visibility: the period of time when Amazon SQS prevents other consumers from receiving and processing the same message
		- If a consumer fails to process and delete the message within the timeout period, the <mark style="background: #FFB86CA6;">message becomes visible again to other consumers</mark>
		- Default is 30 seconds and max is 12 hours
## Pub/Sub (Amazon Simple Notification Service (SNS))
- Instant event notifications that can be broadcast to many systems asynchronously
- The sending application (publisher) needs to send a message to multiple receiving applications (subscriber) with little to no knowledge about the receiving applications
	- A radio broadcast doesn't know who is listening but broadcasts for anyone
- Publishers only have to publish the message to a topic and subscribers are always listening for messages to appear on that topic
	- <mark style="background: #FFB86CA6;">There is no guaranteed message delivery in this system or options for message recall</mark>
- The delivery mechanism is a push (passive) from the publisher vs a queue where consumers actively pull from the message queue
![[Pasted image 20240926213748.png]]
## Step Functions
- Used for workflow management across multiple AWS services
- Uses state machines that contain a series of events that is tracked either synchronously (express workflows) or asynchronously (standard workflows)
- Used for microservice orchestration, data processing, machine learning, and security automation
- Able to choose paths based on conditions, handle errors, retry tasks, and manipulate data
- State machine state (step) types
	- Work states: 
		- Task -  perform an action using an AWS service
		- Activity - Perform a task hosted anywhere
		- Pass - Passes <mark style="background: #FFB86CA6;">or filters input</mark> to output without performing work
		- Wait - Delay the state machine for a specified time
		- Wait for Callback State: Pause workflow and wait for callback
	- Transition State:
		- <mark style="background: #FFB86CA6;">Choice - Adds conditions to control flow to next state</mark>
		- Parallel - Adds branches of nested state machines inside a state machine
		- Map - Separates workflow for each data record in data set that runs in parallel
	- Stop States:
		- Success - Stops state machine and marks execution as successful
		- Fail - Stops state machine and marks execution as failed
		- State has the end parameter - Stops state machine