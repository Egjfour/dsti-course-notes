|  Course Name   |          Topic           | Professor |       Date        |         Tags         |
| :------------: | :----------------------: | :-------: | :---------------: | :------------------: |
| **Amazon AWS** | Cloud Computing Overview |   Ayoub   | 03 September 2024 | #CloudComputing #AWS |

# Summary
*Cloud computing allows people to quickly deploy storage, compute, and other critical resources without having to invest in or maintain underlying hardware. A cloud architect is responsible for the researching of options, the design of the architecture, and the oversight of the building of the chosen design. There are many different types of architecture patterns to choose from such as front-end/back-end, serverless, and MVC that are best suited based on the use case.*

# Key Takeaways
1. The AWS cloud offers an environment that is highly <mark style="background: #FFB86CA6;">available, scalable, and reliable</mark> on top of the Amazon infrastructure
2. The three-tier architecture is typically used for microservices and includes a controller which uses an API to access a service which applied logic and connects to a data repository
3. AWS costs are driven primarily by <mark style="background: #FFB86CA6;">machine instances</mark>, <mark style="background: #FFB86CA6;">adding data</mark> to storage, and <mark style="background: #FFB86CA6;">getting data</mark> from storage

# Definitions
- REST API: A JSON-formatted API that offers many methods of access
	- GET, POST, PUT, etc.
- SOAP API: An XML-formatted API that must always contain a body which supports only POST
- Front-end/Back-end Architecture: A basic architecture separating the user interface from the server-side logic.
	- Microservices
- Model-View-Controller (MVC): A design pattern that organizes applications into three components: Model, View, and Controller such that business logic is separated from the presentation layer
- Serverless Architecture: The front-end directly access data storage via an API
	- A cloud-native architecture where functions are executed in response to events, offering scalability and reduced server management. (Chat GPT)
- Streaming Architecture: Direct real-time connection between back-end and database
- Stateless: No dependency to the host system (local files)
	- This includes user sessions

# Additional Resources
- [Cloud Services Overview (Video)](https://www.youtube.com/watch?v=gcfB8iIPtbY)
- [SOAP vs REST](https://aws.amazon.com/compare/the-difference-between-soap-rest/?nc1=h_ls)

# Notes
## Why Use the Cloud
- Prior to the cloud, setting up an environment took months
	- Need the database, compute, and storage components minimally. Then, you need security and possibly networking too
- Cloud services like Amazon let you have <mark style="background: #FFB86CA6;">access to expensive hardware without having to invest in and maintain it</mark>
	- Security of the cloud itself is also maintained by Amazon
## Costs on the AWS Cloud
- EC2 machine instances
	- Compute resources (uptime)
- Storage
	- Fixed cost for amount
	- Additional costs for sending/retrieving data (always between a client and server via an API)
## Types of Architecture
### Front-end/Back-end Architecture
**Overview**:  
The front-end/back-end architecture is a traditional approach to web development where the application is divided into two main parts:

- **Front-end**: The client-side part that users interact with directly, typically implemented using HTML, CSS, and JavaScript.
- **Back-end**: The server-side part that handles business logic, database operations, authentication, and other processes that are not visible to the user. Common languages include Python, Java, Node.js, etc.

**Key Features**:
- **Separation of Concerns**: <mark style="background: #FFB86CA6;">The front-end is responsible for the presentation, and the back-end handles the business logic and data management.</mark>
- **RESTful APIs**: Often use RESTful APIs or GraphQL to communicate between the front-end and back-end.
- **Scalability**: Front-end and back-end components can be<mark style="background: #FFB86CA6;"> scaled independently.</mark>

### Model View Controller (MVC) Architecture
**Overview**:  
MVC is a design pattern that separates an application into three interconnected components:
- **Model**: Represents the data and the business logic of the application. It is responsible for managing the data, logic, and rules of the application.
- **View**: Represents the UI (User Interface). It displays the data to the user and sends user commands to the Controller.
- **Controller**: Acts as an intermediary between Model and View. It listens to user inputs, processes them (by calling Model methods), and updates the View.

**Key Features**:
- **Separation of Concerns**: Isolates business logic from the user interface.
- **Reusability**: Components can be reused across different parts of the application.
- **Testability**: Each component can be tested independently, improving the test coverage.

### Three-Tier (Domain-Driven Design) Architecture
**Overview**:  
The three-tier architecture divides an application into three logical layers:
- **Presentation Layer**: Similar to the "View" in MVC, this is the user-facing part where the user interacts with the application.
- **Business Logic Layer (Domain Layer)**: This layer contains the core business logic and rules of the application. It manages the data flow between the presentation and data layers.
- **Data Layer**: Handles data storage and retrieval operations, such as interacting with a database or other storage systems.

**Key Features**:
- **Separation of Responsibilities**: Each tier has a distinct role (presentation, logic, data).
- **Scalability and Flexibility**: Allows scaling of each tier independently.
- **Domain-Driven Design (DDD)**: Focuses on the core domain and business logic, using domain models to capture the business rules.

### Serverless Architecture
**Overview**:  
Serverless architecture is a cloud computing execution model where the cloud provider dynamically manages the allocation of machine resources. <mark style="background: #FFB86CA6;">Instead of running applications on dedicated servers, developers write functions that are executed in response to events</mark>.

- **Functions-as-a-Service (FaaS)**: Small, single-purpose functions triggered by events.
- **Backend-as-a-Service (BaaS)**: Cloud services that provide ready-made back-end components such as databases, authentication, and storage.

**Key Features**:
- **No Server Management**: The cloud provider manages server maintenance, scaling, and provisioning.
- **Event-Driven**: Functions are triggered by specific events (e.g., HTTP requests, file uploads).
- **Cost Efficiency**: Pay-per-use model, where billing is based on the number of requests and execution time rather than server uptime.
### Streaming Architecture
**Overview**:  
Streaming architecture is designed to handle real-time data processing and analysis. This architecture is commonly used for applications that require continuous data input and processing, such as real-time analytics, monitoring, fraud detection, and IoT applications. The core idea is to <mark style="background: #FFB86CA6;">process data as it arrives (in streams) rather than waiting for batches of data.</mark>

Key components of streaming architecture include:

- **Data Producers**: Generate data continuously (e.g., sensors, applications, user interactions).
- **Stream Processors**: Process incoming data in real time using stream processing frameworks like Apache Kafka, Apache Flink, or <mark style="background: #FFB86CA6;">AWS Kinesis</mark>.
- **Data Consumers**: Applications or services that consume the processed data for storage, analytics, or other actions.

**Key Features**:
- **Real-Time Processing**: Processes data in near real-time, providing immediate insights and responses.
- **Scalability**: Can handle large volumes of data by scaling horizontally.
- **Fault Tolerance**: Provides mechanisms to ensure data consistency and reliability, even in the case of failures.

### Similarities and Differences Among Them

| **Feature / Architecture** | **Front-end/Back-end**                                 | **MVC**                                                                | **Three-Tier (DDD)**                                               | **Serverless**                                                   | **Streaming Architecture**                                                |
| -------------------------- | ------------------------------------------------------ | ---------------------------------------------------------------------- | ------------------------------------------------------------------ | ---------------------------------------------------------------- | ------------------------------------------------------------------------- |
| **Separation of Concerns** | Clear separation between front-end and back-end        | Clear separation into Model, View, and Controller                      | Separation into Presentation, Business, and Data layers            | Focuses on separating services into functions                    | Separation of data producers, processors, and consumers                   |
| **Scalability**            | Independent scaling for front-end and back-end         | Limited scaling, often requires full-stack adjustment                  | Independent scaling of each layer                                  | High scalability with automatic scaling                          | High scalability, designed to handle large-scale data streams             |
| **Design Pattern**         | Not a design pattern, more of an architecture approach | Design pattern (MVC)                                                   | Design pattern based on layers and domain-driven principles        | Event-driven model                                               | Real-time data flow and event-driven model                                |
| **Flexibility**            | Flexible, can use any front-end or back-end technology | Moderate flexibility but needs adherence to MVC                        | Flexible but often requires commitment to domain-driven principles | Highly flexible, adaptable to various cloud services             | Highly flexible, integrates with various data sources and consumers       |
| **Deployment**             | Deploy front-end and back-end separately               | Can deploy parts independently, but often tied together                | Typically deploys each layer separately                            | No deployment servers, deploy functions to the cloud             | Deploy data pipelines and stream processing components                    |
| **Maintenance**            | Requires management of servers and infrastructure      | Code is more maintainable due to clear separation                      | Easier to maintain due to separation of business logic             | Minimal maintenance, server management handled by cloud provider | Requires monitoring of data streams and pipeline components               |
| **Cost**                   | Depends on infrastructure usage                        | Can vary based on architecture and scale                               | Can be costly if not optimized                                     | Cost-effective, pay-per-use model                                | Can be cost-efficient, but depends on data volume and processing needs    |
| **Use Cases**              | General web development                                | Web applications, especially where separation of concerns is important | Large enterprise applications                                      | Event-driven applications, microservices, rapid development      | Real-time analytics, monitoring, IoT, fraud detection, and live streaming |
## APIs
- APIs allow for standardized app communication, microservice protection, and monetization of usage
- API types
	- REST
		- Stateless calls that are made up of a collection of routes and methods using HTTP verbs 
		- Advanced API management features like payload validation, private endpoints, etc
	- HTTP
		- Routes and methods, also stateless but are optimized for serverless workloads and microservices
		- Lower latency and cost than REST
	- WebSocket APIs
		- Collection of WebSocket routes that establishes a session between the client and backend services
		- Stateful and used for real-time applications