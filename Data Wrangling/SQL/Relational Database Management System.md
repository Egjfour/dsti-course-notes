|         Course Name         | Topic | Professor |    Date     | Tags |
| :-------------------------: | :---: | :-------: | :---------: | :--: |
| **Data Wrangling with SQL** | RDBMS |   Hanna   | 14 May 2024 | #SQL |

# Summary
*A relational database management system is a type of software that needs to be installed. There are many different flavors of RDBMS software from different open-source and proprietary providers. RDBMS software follows a client-server architecture. Typically SQL Server engines are stored on a dedicated virtual machine for security reasons.*

# Key Takeaways
1. Proprietary RDBMS software is often desirable despite the cost because of the added security and support that is guaranteed by the provider and the fact that the code is not available to be read by potential malicious actors

# Definitions
- Client: This is the additional software that is used to communicate with the SQL Server
	- The SQL Server Management Studio Application
	- Additional scripts (Python, R, etc via an API)
- Server: This is where the data is stored and acted upon as queries are received

# Additional Resources
- [Client Server Architecture](https://intellipaat.com/blog/what-is-client-server-architecture/#:~:text=Client%2Dserver%20architecture%20is%20a,are%20delivered%20over%20a%20network.)

# Notes
## Relational Database Management Systems (RDBMS)
- Software that serves the purpose of storing data in a table format
	- It may not always be the case that we want a table
- This software is specifically meant to store and retrieve/query data
- Examples

| Proprietary ($) | Open-Source |
| :-------------: | :---------: |
|  Microsoft SQL  |    MySQL    |
|     Oracle      | PostgreSQL  |
|   DB/2 (IBM)    |   MariaDB   |
|     Hadoop      |   SQLite    |
|   AWS Aurora    |             |
- Proprietary software is preferable for enterprise-level databases because of the additional support and security offered despite the costs
	- "Client-server architecture is a computing model in which the server hosts, delivers, and manages most of the resources and services requested by the client. It is also known as the networking computing model or client-server network as all requests and services are delivered over a network"
## Architecture
- RDBMS software follows a client-server architecture allowing a client to interact with (send queries and view results) the data on a server
- ![[Pasted image 20240524175010.png]]

|                     Client                     |                           Server                            |
| :--------------------------------------------: | :---------------------------------------------------------: |
|                   Query Data                   | <mark style="background: #FFB86CA6;">Database engine</mark> |
|                  Receive Data                  |                     Storage/Management                      |
|  User Interface (Google or Amazon Search Bar)  |                      Query Interpreter                      |
| Software (SQL Management Studio, PBI, Tableau) |                    Security (encryption)                    |
|      API (Command Line, ODBC in python/R)      |                                                             |
## Installation Options
- Installation options
	- Can handle this locally (*not recommended*)
		- The DB engine and the client software is on your local PC
	- Dedicated VM
		- Everything (client and server is on a dedicated machine)
	- Hybrid
		- Client is local but the server is on a dedicated machine