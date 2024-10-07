|  Course Name   |   Topic    | Professor |        Date        |         Tags         |
| :------------: | :--------: | :-------: | :----------------: | :------------------: |
| **Amazon AWS** | Networking |   Ayoub   | 5-6 September 2024 | #CloudComputing #AWS |

# Summary
*A virtual private cloud is like a [[Internet Protocol (IP) and LAN|local area network]] located on the AWS cloud. These are specified by the size of the range of IP addresses they cover. These can be divided into subnets which can be either public (internet accessible) or private (not internet accessible). There are many ways through which subnets and separate VPCs can communicate with each other. All instances of communication between segregated resources requires using the VPC (or subnet) routing tables.*

# Key Takeaways
1. A VPC is sized by a CIDR block. These exist across several availability zones and the addresses should be spread evenly (max size of /16 with 65,536 IP addresses)
2. A VPC contains a main route table with a set of route rules
3. Security groups are stateful and ACLs are stateless
4. Transitive peering is not supported by AWS

# Definitions
- Virtual Private Cloud (VPC): Programmatically defined, logically separated virtual networking belonging to a specific region
- Classless Inter-Domain Routing (CIDR) Block: A range of private [[Internet Protocol (IP) and LAN|IP addresses]]
	- 10.22.0.0/16 is all IPs starting from 10.22.0.0 and ending with 10.22.255.255
- Full-Mesh Architecture: Connect all networks to each other
- Hub and Spoke Architecture: Each network connects only to a central network which is responsible for making connections between all networks

# Additional Resources
- [Security Groups and ACLs (AWS)](https://docs.aws.amazon.com/whitepapers/latest/aws-best-practices-ddos-resiliency/security-groups-and-network-acls-bp5.html)
- [Bastion Hosts (Nord VPN)](https://nordvpn.com/cybersecurity/glossary/bastion-host/)
- [AWS Networking Basics (Video)](https://www.youtube.com/watch?v=2doSoMN2xvI)

# Notes
## Virtual Private Cloud (VPC)
- Overview
	- Programmatically defined, logically isolated virtual network
	- Defined by a CIDR block
		- When thinking of size requirements, note that Amazon reserves the first four and the last IP address in a block
	- Spread across multiple availability zones <mark style="background: #FFB86CA6;">in the same region</mark>
	- Every resource on the VPC is visible to each other thanks to the main route table entry that specifies the local address space
		- This main route table is used as the default if a more granular table doesn't have an entry for a specified resource
## Subnets
- Can be either public (allows direct internet access) or private (does not allow for direct internet access)
- Internet access in a public subnet is provided by an internet gateway and an entry in the route table for the public subnet that allows inbound and outbound internet traffic
 ![[Pasted image 20240922203410.png]]
- Elastic IP addresses are static, public IPv4 addresses that can be assigned to an EC2 instance, load balancer, or VPC network interface
	- These can be transferred to resources as they are created or terminated (though having an Elastic IP that is either not attached to a resource or attached to a stopped resource incurs an hourly cost)
- A [[Networking (TCP and UDP)|Network Address Translator (NAT)]] can be placed in a public subnet to allow for resources in a private subnet to communicate with internet resources without exposing their IP
	 ![[Pasted image 20240922203946.png]]
## Network Security
- Isolation in a public subnet isn't enough for security. Should also use secure protocols (HTTPS and TLS) as well as security groups and ACL
- Security Groups
	- Stateful firewalls that act at the instance or network interface level
		- If an inbound rule allows a connection, the information will still flow out even without a rule allowing that same type of outbound traffic
	- Span multiple AZs
	- Ports and protocols are specified for inbound and outbound traffic
	- Only supports allow rules, not deny
- Access Control Level (ACL)
	- Acts as a firewall for controlling traffic types into and out of a subnet
	- Every VPC must be associated with an ACL
	- Inbound and outbound rules that can either allow or deny traffic
	- Since it is <mark style="background: #FFB86CA6;">stateless, return traffic must be explicitly allowed by rules</mark>
	- These are numbered to signify precedence (lower takes precedence)
 ![[Pasted image 20240922210858.png]]
- There is no additional charge for using security groups or ACLs
- Bastion Hosts
	- A server (EC2 instance) on a public subnet that provides maintenance access to a private subnet from an external network
	- An inbound rule is setup for the bastion host server and then the security group of the bastion host is able to communicate with resources on the private subnet
## Interface and Gateway Endpoints (Connect to AWS Services)
- Interface endpoint is provided through the AWS PrivateLink network
	- Costs additional money but <mark style="background: #FFB86CA6;">uses private IP addresses</mark>
		- Priced based on hourly usage and volume of data
	- Services cannot initiate requests but only respond to requests from a VPC
- Gateway endpoints use route tables to directly connect a VPC to services
	- Not billed but only supports <mark style="background: #FFB86CA6;">S3 and DynamoDB</mark>
	- Uses public IP addresses
## Network Monitoring
- Flow logs are offered as a feature by Amazon VPC which provides packet-level information about the network traffic in a VPC
	- VPC Flow Logs delivers network traffic to Amazon CloudWatch logs, Amazon S3 buckets, or Amazon Kinesis Data Firehose streams
	- Operate outside the VPC, so no performance impacts
	- Access to view is controlled by IAM policies
- Additional Amazon VPC tools
	- The reachability analyzer is used to see if two addresses are reachable in a network
		- Identifies the blocking issue in connectivity problems
	- Network Access Analyzer is used to understand and improve network security posture by eliminating unintended network access. Also used for compliance demonstration
	- Traffic Mirroring lets us analyze actual traffic content including the actual message payload by making a copy of every packet sent and received
## Connecting Networks
- Transit Gateway is a managed service which provides a centralized, regional router to connect VPCs and on-prem networks
	- Also allows centralized routing of outbound traffic
	- The transit gateway must have a connection for each AZ in each VPC and must be on he VPC routing table in each VPC
- The transit gateway peering attachment allows route tables in different AWS accounts and/or regions to have access to each other
- A mesh network can be built to connect VPCs using direct peering connections between VPCs
	- This incurs <mark style="background: #FFB86CA6;">no additional cost unlike a Transit Gateway</mark>
	- Uses IP addresses as if each VPC is in the same network
	- Also allows for connecting VPCs across AWS accounts and regions
	- Traffic stays on the AWS global backbone (no internet) and all inter-Region traffic is encrypted. Also uses private IP addresses
	- Need to add the ID of the VPC peering connection to each VPC
- PrivateLink
	- Used to connect VPCs at the application level
		- privately connect to a service or application that resides in a service provider VPC from consumer VPCs within an AWS Region
	- Elastic Network Interface + Network Load Balancer
	- Only consumers can connect to the service provider and allows overlapping CIDR blocks