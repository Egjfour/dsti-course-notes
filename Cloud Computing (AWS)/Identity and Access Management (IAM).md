|  Course Name   |      Topic      | Professor |         Date          |         Tags         |
| :------------: | :-------------: | :-------: | :-------------------: | :------------------: |
| **Amazon AWS** | Securing Access |   Ayoub   | 04, 06 September 2024 | #CloudComputing #AWS |

# Summary
*AWS Identity and Access Management (IAM) is a service that is used to execute fine-grained control over user permissions to AWS resources. There are many ways to streamline IAM with filters and by creating and using groups*

# Key Takeaways
1. AWS IAM supports federated identity management and MFA
2. When a user assumes a role, their own permissions are forgotten
3. Users can be in many groups and will inherit the permissions of all groups
4. Deny permissions are evaluated prior to allow permissions in cases of conflict
5. By default, all requests are denied unless explicitly allowed

# Definitions
- Principle of Least Privilege: An entity should have access to the minimum necessary subset of resources on the cloud to perform tasks
	- INSIGHT SFTP access. Only have permissions to the folders for the projects I'm assigned to
	- Follows the [[AWS Well-Architected Framework|WA Framework]]
- Authentication: Identify a user/entity using credentials
- Authorization: Permissions to access specific resources
	- After the requester has been authenticated, what should they be allowed to do?
- Identity-based Policy: Policies that are attached to an IAM user, group, or role and indicate what the user is permitted to do.
- Resource-based Policy: Policies that are attached to a resource and indicate what a specified user (or group of users) is permitted to do with the resource

# Additional Resources
- [IAM Overview](https://aws.amazon.com/iam/?nc1=h_ls)
- [IAM Users Video](https://www.youtube.com/watch?v=bO25vbkoJlA&list=PL7iMyoQPMtAN4xl6oWzafqJebfay7K8KP)
- [IAM Assume Role Video](https://www.youtube.com/watch?v=MkiWa31iV6U&list=PL7iMyoQPMtAN4xl6oWzafqJebfay7K8KP&index=3)

# Notes
## Users, Groups, and Roles
- An IAM user is a specific person or application that needs to be able to access AWS resouces
	- Me logging in, 
- A user can get their permissions from many places
	- Directly assigned to them
	- Inherited from a group
	- A role
- Roles are temporary permissions that users can assume
	- When a user is assuming a role, their permissions are forgotten
## Creating and Evaluating Policies
- A policy is the set of rules that defines what permissions a given entity has
- AWS resolves policies by first checking for explicitly denies and then looking for an explicit allow
	- If there is neither, an implicit deny is assumed
	 ![[Pasted image 20240907163947.png]]
 - Policies are either identity or resource based
	 - This distinction is seen in the principal of the IAM policy document
	 - Are you setting permissions for an entity (users or groups) or a particular resource (instances, storage, etc)
 - Policies all have the following components in their JSON body
	 - Version of the policy language that you want to use
	 - Statement: list of the various permissions
	 - Effect: allow vs deny
	 - Principal: Implied in an identity-based policy OR the entity (user, group, etc) that the policy will apply to for a resource-based policy
	 - Action that is allowed or denied
		 - s3:GetObject
		 - ec2:CreateInstance
	 - Condition (optional): Filters that must be met for the rule to apply
![[Pasted image 20240907164813.png]]
![[Pasted image 20240907164840.png]]
## IAM Terminology Glossary
- **Policy**: A JSON document that defines permissions, specifying allowed or denied actions on AWS resources. <mark style="background: #FFB86CA6;">Policies are attached to identities (users, groups, roles) or resources</mark> to manage access.
    
- **Role**: An IAM identity that provides <mark style="background: #FFB86CA6;">temporary permissions to entities</mark> (users, services, applications) to perform actions on AWS resources. Roles are assumed, not assigned credentials.
    
- **Group**: A collection of <mark style="background: #FFB86CA6;">IAM users that share the same permissions</mark>. Groups simplify permission management by allowing policies to be attached to multiple users simultaneously.
    
- **User**: An identity in AWS that represents<mark style="background: #FFB86CA6;"> a person or an application needing direct access to AWS resources.</mark> Users have unique credentials (username, password, access keys).
    
- **Principal**: An entity that can perform actions and access resources in AWS. This can be an IAM user, role, federated user, or AWS service.
    
- **Identity**: A generic term representing an entity in AWS IAM (e.g., users, groups, roles) that can be authenticated and authorized to access AWS resources.
    
- **Entity**: A representation of an IAM object within an AWS account, such as a user, group, or role, that requires permissions to access resources.
    
- **Resource**: An AWS entity that can be the target of actions performed by a principal. Examples include EC2 instances, S3 buckets, DynamoDB tables, etc.
    
- **Organization**: An <mark style="background: #FFB86CA6;">AWS service for centrally managing multiple AWS accounts</mark>. It allows you to consolidate accounts, apply policies, and control access at the organization level.
    
- **Service Control Policy (SCP)**: A policy used in AWS Organizations to set the<mark style="background: #FFB86CA6;"> maximum permissions available for member accounts.</mark> SCPs restrict access across all users and roles within an account or organizational unit.

| **Term**         | **Definition**                                   | **Purpose**                                            | **Attachment**                                 | **Persistence**                               | **Examples**                                       |
| ---------------- | ------------------------------------------------ | ------------------------------------------------------ | ---------------------------------------------- | --------------------------------------------- | -------------------------------------------------- |
| **Policy**       | Document defining permissions on AWS resources   | Controls access by specifying allowed/denied actions   | Attached to users, groups, roles, or resources | Permanent until deleted/modified              | Inline policies, managed policies                  |
| **Role**         | Temporary permissions assigned to entities       | Grant permissions temporarily                          | Assigned to users, services, or applications   | ==Temporary (session-based)==                 | EC2 instance role, Lambda execution role           |
| **Group**        | Collection of users with shared permissions      | Simplify managing multiple users' permissions          | Associated with users                          | Permanent (inherits policies from group)      | Admin group with read/write permissions            |
| **User**         | Individual identity with credentials             | Represents individuals or applications                 | Has policies attached directly                 | Permanent until deleted/modified              | Developer user, service account user               |
| **Principal**    | Any entity allowed to perform actions on AWS     | Represents any authenticated entity in AWS             | Defined as users, roles, AWS services, etc.    | N/A (generic term for any active AWS actor)   | IAM user, assumed role, AWS Lambda service         |
| **Identity**     | Generic term for an IAM entity                   | Represents any object that can access AWS              | Users, groups, roles, and principals           | Permanent until entity is modified or removed | IAM user, group, role                              |
| **Entity**       | Object representing a user, group, or role       | Specific IAM object within an AWS account              | Defined entities such as users, roles, groups  | Permanent until entity is deleted             | IAM user, IAM role                                 |
| **Resource**     | AWS object that is the target of actions         | Target of actions defined by policies or principals    | Can have policies attached                     | Permanent (until resource is deleted)         | S3 bucket, EC2 instance, RDS database              |
| **Organization** | Manages multiple AWS accounts centrally          | Consolidate accounts, manage policies, governance      | Applied to organizational units or accounts    | Permanent until modified                      | Organization with multiple AWS member accounts     |
| **SCP**          | Policy defining max permissions for AWS accounts | ==Restrict access across accounts in an organization== | Applied to org units or accounts               | Permanent until modified                      | SCP restricting actions across all member accounts |
## IAM Policy and Trust Policy

- IAM Policy (Permissions Policy):
    - Defines **what actions** an entity (like a user, group, or role) is **allowed or denied** to perform on AWS resources.
    - These policies specify which services, actions, and resources the entity can interact with.
    - For example, an IAM policy could grant permission for a role to access an S3 bucket by including something like the below
    -  This policy controls <mark style="background: #FFB86CA6;">what the role can do once it is assumed</mark>—i.e., access S3 in this case.
```json
{
	"Effect": "Allow",
	"Action": "s3:GetObject",
	"Resource": "arn:aws:s3:::example-bucket/*"
}
```
- Trust Policy:
    - Defines **who (or what service)** is allowed to assume the role.
    - In other words, it defines <mark style="background: #FFB86CA6;">which entities are trusted to use the role’s permissions.</mark>
    - Without this trust policy, even though the role has the permissions to access S3 (as defined in the **IAM policy**), no entity (like EC2) can assume the role to actually use those permissions.
    - For example, to allow EC2 instances to assume the role, you need a trust policy like this:
```json
{
  "Effect": "Allow",
  "Principal": {
    "Service": "ec2.amazonaws.com"
  },
  "Action": "sts:AssumeRole"
}

```
- How They Work Together:
	- The **trust policy** says, "I trust this entity (like EC2) to assume my role."
	- The **IAM policy** attached to the role says, "Here are the specific permissions that this role has for interacting with AWS resources (like S3)."
	- For the EC2 instance to access S3:
	    1. The **trust policy** must allow EC2 to assume the role.
	    2. The **IAM policy** must allow actions like `s3:GetObject` or `s3:PutObject` on the S3 bucket

## Tagging
- Allows for attribute-based access control 
	- Policy checks whether an attribute that’s applied to the IAM user is also applied to the resource that they want to access
- Tags are case-sensitive key-value pairs that represent resource metadata
- Max number of keys for a resource is 50 and with maximum lengths of 128 chars for the key and 256 for the value
 ![[Pasted image 20240922235800.png]]
## Identity Federation
- Allows user authentication to be provided by a (potentially) separate identity provider (single sign-on)
	- Access control to resources is managed by the service provider still
- IAM provides temporary credentials to externally federated users so they can access resources
## Service Control Policies and Permission Boundaries
- Using AWS Organizations (account management service), we can set limits on abilities across accounts
	- Defines the <mark style="background: #FFB86CA6;">maximum permissions that a group or user account can be granted</mark> through IAM policies
- SCPs cannot be overridden by the local administrator
- SCPs do not themselves grant permissions
- Many different use cases for policy enforcement such as:
	- Block service access or specific actions. For example, deny users from disabling AWS CloudTrail in all member accounts.
	- Enforce the tagging of resources. For example, do not allow users to launch an Amazon Elastic Compute Cloud (Amazon EC2) Amazon Machine Image (AMI) unless it has a specific tag on it.
	- Prevent member accounts from leaving the organization.
- When combined with IAM policies, a permission must be granted in both the SCP and IAM to be accessed (due to the implicit deny in IAM policy resolution)
- Permission Boundaries
	- An entity's permissions boundary allows it to <mark style="background: #FFB86CA6;">perform only the actions that are allowed by both its identity-based policies and its permissions boundaries</mark>
	- Applied to an IAM entity or role as opposed to all accounts in an organization

| Feature                 | Service Control Policies (SCPs)          | Permission Boundaries                        |
| ----------------------- | ---------------------------------------- | -------------------------------------------- |
| **Scope**               | Organization-wide, affects all accounts  | Entity-specific, applies to users and roles  |
| **Attachment**          | Applied to accounts/organizational units | Applied to individual IAM users or roles     |
| **Grants Permissions?** | No, only restricts what can be granted   | No, limits what an IAM policy can allow      |
| **Purpose**             | Set organization-wide permission limits  | Limit permissions for specific entities      |
| **Use Case**            | Restrict permissions across accounts     | Limit permissions for individual users/roles |
