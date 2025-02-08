|  Course Name   |       Topic       | Professor |       Date        |         Tags         |
| :------------: | :---------------: | :-------: | :---------------: | :------------------: |
| **Amazon AWS** | Compute Instances |   Ayoub   | 04 September 2024 | #CloudComputing #AWS |

# Summary
*EC2 instances are virtual machines that run on hardware provisioned by AWS. These are fully-functional systems that allow complete control by the cloud architect to meet various needs. EC2 instances offer a wide range of instance types (the actual underlying hardware) that can be easily fit for purpose and storage types. EC2 instances can be saved as templates called AMIs that allow for quick and repeatable deployment. There are many pricing options for EC2 instances as well ranging from a bidding system for spare capacity all the way to complete control over instance placement on dedicated hardware. In addition to EC2 instances, AWS has container-based options including a serverless option, Fargate, as well as lambda functions for short-lived, low-memory jobs.*

# Key Takeaways
1. Instance storage is not persistent, so the data will not be preserved when the instance is no longer running unlike the Elastic Block Storage (EBS) solution
2. An AMI is required to be specified when launching an EC2 instance
3. An AMI can be created from a modified EC2 instance
4. An AMI is only available in the region is was created. Need to copy if adding to other regions
5. A terminated instance cannot be connected to or recovered
6. Charges are not incurred for any instances that are in a stopped or terminated state
	1. The charges are also not incurred while stopping or terminating
7. The latest generation in an instance family is generally the best cost-to-performance ratio
8. An EBS optimized instance improves I/O performance by creating a dedicated network connection to attached EBS volumes
9. The user data script only runs when the instance is first launched

# Definitions
- Amazon Machine Image (AMI): A template for an EC2 to use while initializing
	- Includes information about the OS, storage type, CPU Architecture, and virtualization type
- Security Group: Set of firewall rules that controls traffic)
- User Data: A script that is run at instance launch time that can be used to automatically perform installations and updates
- Step Scaling: Apply a scaling policy based on metrics and designated thresholds
- Container: Standardized application code packages that contain the code and the code dependencies

# Additional Resources
- [AMI Overview](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AMIs.html)
- [EC2 Storage Overview](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/Storage.html)
- [EC2 Instances Comparison](https://ec2instances.info)

# Notes
## Compute Resources on AWS
- Many options exist for all different needs ranging from a full VM to serverless options
 ![[Pasted image 20240908173648.png]]
## Amazon EC2 Overview
- EC2 is a [[Virtual Machines|virtual machine]] that runs on a physical host in the AWS cloud
- These can be provisioned in minutes and support autoscaling
- CPU and Memory configurations can be chosen by the user
- All EC2 instances provide network connectivity
- Different storage options including instance (temporary) and Elastic Block Store (persistent)
	- This is storage that is specific to the VM instance unlike [[Data Storage (S3 and Caching)|S3 storage]] which can be accessed by anyone with permissions
## Provisioning an EC2 Instance (Step-by-Step)
1. Start with an Amazon Machine Image (AMI)
2. Select an instance type
	a. 1.Instance types comprise varying combinations of CPU, memory, storage, and networking capacity.
3. Specify a key pair for Secure Shell (SSH) or Remote Desktop Protocol (RDP) -- optional
4. Specify network placement and addressing
	a. All instances are deployed within a network in a [[Networking and Virtual Private Cloud (VPC)|virtual private cloud (VPC)]]
	b. Decide whether there should be a public [[Internet Protocol (IP) and LAN|IP Address]] or DNS Address
5. Assign a security group
6. Choose the storage options
	a. This is <mark style="background: #FFB86CA6;">what the OS will boot from</mark> and can either be instance storage (ephemeral) or an EBS volume
	b. Additional block volumes can be attached to the instance if needed
7. Attach an [[Identity and Access Management (IAM)|IAM role]] if the instance will need to call AWS API calls
8. Specify any user data
![[Pasted image 20240908181309.png]]
## Amazon Machine Image (AMI)
- Templates for the root volume that specify the OS and any other installed software 
- Improves the <mark style="background: #FFB86CA6;">repeatability, reusability, and recoverability</mark> of EC2 instances
- Many sources exist including ones we create, ones from Amazon, and ones created by others
- AMIs should be chosen based on region, OS, storage, CPU architecture, and the virtualization
	- <mark style="background: #FFB86CA6;">Hardware Virtual Machine has better performance</mark> than paravirtual
- The choice between instance types really comes down to whether persistent storage is needed or not. Though, there are other differences between instance-based and EBS-based storage
	- EBS tends to boot faster
	- EBS root capacity is 16 tebibytes compared to 10 GB for instance-based
	- An EBS-backed instance can be stopped but instance store can only be rebooted or terminated
	- EBS can cost more since EBS volume usage and snapshot is billed vs just the AMI on S3
		- Both types charge for the instance usage itself
## Instance Lifecycle
- All instances go into a pending state while launching
- Rebooted instances maintain the same public DNS name and public IP address
![[Pasted image 20240908185200.png]]
## Instance Type Options
- Various combinations of hardware resources that are good for different use cases
![[Pasted image 20240908185855.png]]
## Storage on EC2 Instances
- Main differences between options are if root volume is needed, if a single instance or multiple instances will need access, and the OS
- Instance stores are typically HDD or SSD, are temporary, and are attached to a single instance
	- Used mostly for buffers, cache, and scratch data
	- Instance stores that use NVMs have higher I/O performance
	- Instance store is dedicated to a particular instance but the disk subsystem is shared among instances on a host computer
	- <mark style="background: #FFB86CA6;">Cannot be stopped - can only be rebooted or terminated</mark>
- Elastic Block Storage (EBS) is persistent storage that is also attached only to a single instance
	- Also has a dedicated internet connection which increases I/O throughput
	- Extremely low access latency since they are mounted on the instance -- can used to be run a database
	- SSD vs HDD EBS backend types (<mark style="background: #FFB86CA6;">all types can be a boot volume</mark>)
		- SSD is better for Input/Output Operations per Second (IOPS)
			- General Purpose balances price and and performance and provisioned IOPS is good for mission-critical workloads that need low latency
		- HDD is better when the focus is on throughput (large datasets and large I/O sizes)
			- Throughput optimized HDD is a low-cost volume type for frequently accessed throughput-intensive workloads and Cold HDD is the lowest cost HDD volume used for less frequently accessed workloads
- Elastic File System (EFS) and FSx are used for multiple instances (Managed Services)
	- EFS is for linux systems and FSx is for Windows
	- Ensures performance and read-after-write consistency of a network file system
	- EFS specifies a mount target which is a specific address in an availability zone
		- The mount target provides the IP address which is then mounted with its DNS name
		- Standard class storage would create a mount target in each AZ
		- Subnets in the same AZ can share the same mount target
		- It is also possible to mount to only one AZ and access from other AZs (however there are data access charge for EC2 instances crossing AZs)
			- One Zone storage class is for <mark style="background: #FFB86CA6;">frequently accessed data that doesn’t require highest levels of durability and availability</mark> like blog pages of a website
## User Data
- Optional script that is passed to an instance's OS that is used to initialize it
	- Examples: patching and updating installed software, installing new software, etc
- Runs with root/admin privileges after the instance is launched but before it's available on the network
 ![[Pasted image 20240914114716.png]]
- The cloud-init package is an open source app that is used to bootstrap linux in cloud environments to configure additional cloud-related system elements. Most notably, the SSH & authorized keys
- Instance metadata (Public IP, hostname, MAC Address) can all be accessed from the user data by accessing the following link-local address `http://169.254.169.254/latest/meta-data/`
- To <mark style="background: #FFB86CA6;">modify user data, an instance must be stopped.</mark> Then user data can be edited. Once the config_scripts_user file is removed, the user data script can be rerun by restarting the instance or running the command `/var/lib/cloud/instance/scripts/part-001`
## Pricing Models
- Purchase Models (Big savings for different use cases)
	- On-demand: high flexibility with not long-term contract and low rates. Short-term, spiky, and unpredictable workloads. Good for developing and testing. Pay by the hour or second
	- Reserved Instances: Reserve computing capacity for a 1 or 3-year term with lower hourly costs. Fixed price for as long as the instance is owned. Predictable or steady-state needs
	- Savings Plans: Flexible model with low prices on EC2, Lambda, and Fargate in exchange for a consistent amount of usage commitment
		- Compute Savings Plans: Most flexibility and help reduce costs. Automatically apply to EC2 instance usage regardless of family, size, AZ, or region and can be transferred
		- EC2 Instance Savings Plans: apply to specific instance family w/in a specific region but have the <mark style="background: #FFB86CA6;">largest discount</mark> (up to 72%)
	- Spot Instances: Bid on unused EC2 instances and request spare computing at substantial savings. Can be stopped and restarted by Amazon with a 2-minute notification
- Capacity reservations (reserved instances that guarantee availability)
	- On-demand: Reserve compute capacity in a specific AZ for any duration to mitigate the risk of being unable to get on-demand capacity
	- EC2 Capacity Blocks for ML: GPU instances for a future date to run ML workloads. Only paying for the amount of compute time needed w/ no long-term commitment
- Dedicated Models (dedicated hardware to meet compliance and regulatory needs)
	- Dedicated Instances: Run on hardware that is dedicated to a single customer. Two dedicated instances that belong to the same AWS account are physically isolated. However, a dedicated instance <mark style="background: #FFB86CA6;">may share hardware w/ other instance from the same AWS account that are not dedicated</mark>
		- Billed per instances (hourly per-instance usage fee and dedicated per-Region fee paid hourly)
	- Dedicated Hosts: A physical EC2 server fully dedicated to a single customer. Can be purchased on-demand (hourly) or as part of savings plans. Gives visibility and control over how instances are placed on a physical server
		- Billed per host with 3 models (On-demand, reservation, and savings plans)
## Autoscaling
- EC2 Autoscaling is a free service from Amazon that allows <mark style="background: #FFB86CA6;">user-defined conditions, ELB health checks, or scheduled actions</mark> to automatically launch and retire EC2 instances from a template
- Manages a logical collection of Amazon Elastic Compute Cloud (Amazon EC2) instances called an Amazon EC2 Auto Scaling group across Availability Zones
	- Number of instances (min and max) is set in the capacity settings for the group
- Can also specify what percentage of the desired capacity should be fulfilled with On-Demand Instances, Reserved Instances, and Spot Instances
- Step Scaling
	- One or more step adjustments that automatically scale the capacity of the target dynamically based on the size of the alarm breach
## Lambda Functions and Containers
- Lambda functions
	- Run small compute jobs with low time and memory needs
		- Max 15 minutes and 10 GB
	- Works synchronously (lambda service runs function and waits for a response) or asynchronously (lambda service places the event in an internal queue with an error queue as well)
	- Lambda layers are zip file archives that contain supplementary code or data (libraries, custom runtimes, or config files)
- Containers
	- Long or memory-intensive workloads are much cheaper in containers
	- Containers are standardized application code packages that contain the code and the code dependencies that run on top of a container engine with read access to part of the host OS
	- Fargate is the serverless option for container management that offers automatic scaling, per second billing, and no cluster/server management
	- The elastic container service consists of compute nodes on a platform such as Fargate or EC2. Deploying contains uses an ECS task definition
	- The elastic Kubernetes service uses pods to deploy that don't directly interact with the container. A deployment can also be created which owns a ReplicaSet which is responsible for keeping a specified number of pods running
	 ![[Pasted image 20240926225724.png]]