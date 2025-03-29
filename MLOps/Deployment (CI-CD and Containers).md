| Course Name |        Topic         |  Professor  |      Date       | Tags |
| :---------: | :------------------: | :---------: | :-------------: | :--: |
|  **MLOps**  | CI-CD and Containers | Joe Sanchez | 05-06 mars 2025 |      |

[Professor Notes Link (CI-CD)](https://github.com/adaltas/dsti-mlops-2025-spring/blob/main/05.ci-cd/index.md)
[Professor Notes Link (Docker Containers)](https://github.com/adaltas/dsti-mlops-2025-spring/blob/main/06.docker-containers/index.md)
[Professor Notes Link (Model Deployment)](https://github.com/adaltas/dsti-mlops-2025-spring/blob/main/10.deployment/index.md)

# Summary
*Automation around deployment is the crucial step which brings [[DevOps and MLOps Overview|DevOps and MLOps]] to life and allows models to actually go to production. DevOps best practices like [[Testing|testing]] can be automated through CI pipelines, and then deployment is handled through CD pipelines. A common deployment mechanism for transferable code is containerization with docker which allows us to package code and dependencies together and run in any hardware environment.*

# Key Takeaways
1. New releases of software (even containerized) are deployed to registries
2. Github Actions are a mechanism which allows for the automation of CI-CD pipelines
3. In containers, code and all dependencies are packaged together to let apps run quickly and reliably in different computing environments
4. In containers, applications are secure and Docker has strongest default isolation capabilities

# Definitions
- Delivery (ML): A step before deployment. Model is ready just waiting to be deployed
- Deployment (ML): Integrating a new model into existing environment
	- Does not require interaction with end users
- Continuous Integration (CI) - a practice in which members of a team integrate their work frequently.
- Continuous Delivery (CD) - automatically delivers the software to the testing or staging environment and requires human intervention for deployment to production.
- Continuous Deployment (CD) - this <mark style="background: #FFB86CA6;">extends Continuous Delivery</mark> by automating the deployment process so that code is automatically deployed to production after it passes automated testing.
- CI/CD Pipeline: The automated sequence of events that is initiated after code is updated
- Registries: Software package hosting services
- Serving (ML): A model put in disposition to end users
- Release: A version of a service is now responsible for serving production traffic

# Additional Resources
- [Understanding Github Actions](https://docs.github.com/en/actions/about-github-actions/understanding-github-actions)
- [CMD vs ENTRYPOINT in Docker](https://stackoverflow.com/questions/21553353/what-is-the-difference-between-cmd-and-entrypoint-in-a-dockerfile)
- [Deployment Strategies](https://www.harness.io/blog/blue-green-canary-deployment-strategies)

# Notes
## Continuous Integration/Continuous Delivery (CI/CD)
- This is the actual automation of the [[DevOps and MLOps Overview|DevOps processes]]
- CI Fundamentals
	- Single-source repository
	- Automated builds and deployments
	- Self-testing builds
	- Frequent iterations
	- Stable testing environments
	- Maximum visibility
- Tooling
	- Gitlab, Travis CI, Jenkins
- CD Fundamentals
	- Releases are deployed to registries
 ![[Pasted image 20250324153620.png]]
## Automation with Github Actions
- Actions are stored as yaml files in the `.github` folder of the repository
- These actions are executed using a runner either setup on your own server or provided by Github (configuration specified in the yaml file)
- Actions are used to run tests, perform linting, deploy code to registries, and more
- GH Actions are <mark style="background: #FFB86CA6;">event-driven</mark>
	- on push, on pull request, etc
- Anatomy of GH Actions
	- Event: specific activities that trigger a workflow run
	- Runner: a machine with the Github Actions runner application installed. Then runner waits for available jobs it can then execute
	- Workflow: an automated process that is made up of one or multiple jobs and can be triggered by an event
	- Job: multiple steps and runs in an instance of the virtual environment
		- Can be run independently or sequentially if necessary
	- Step: a set of tasks that can be executed by a job. Steps can run commands or actions.
	- Actions: the smallest portable building block of a workflow and can be combined as steps to create a job
	 ![[Pasted image 20250324153919.png]]
## Docker [[Computation (EC2, Lambda, Containers)|Containers]]
- Containers provide a stable, isolated environment for running code without having to deal with the cumbersome requirements of a virtual machine
	- Applications are abstracted from the environment in which they run
	- Provides for easy and consistent deployment
- Code and dependencies are packaged together
	- CPU, memory, storage, and network resources are handled at the OS level
- Docker containers should be simple: they do 1 thing and do it well
- Based off the client-server architecture
	- Client: CLI as a [[Cloud Overview|REST API]]
		- Commands including `docker build`, `docker run`, `docker push`, etc
	- Server: Docker Host
		- Daemon, containers, images, volumes
- Saved to registries like Docker Hub and Nginx
- Common CLI Commands
	- `docker help` - explore commands
	- `docker ps` - list running containers
	- `docker run <CONTAINER_NAME>` - list running containers
	- `docker container` - manage containers
	- `docker image` - manage images
	- `docker volume` - manage volumes
	- `docker network` - manage networks
	- `docker exec` - run a command in a running container
- Storage on docker is <mark style="background: #FFB86CA6;">preferably managed using volumes</mark> which creates a directory within Docker's storage directory
	- Example: `docker run -v path/on/host:/path/on/docker container-name:tag`
	- Bind mounts allow you to use a file or directory mounted from the host machine into the container
	- tmpfs is a temporary directory which can create files outside the container's writable layer
## Building and Publishing Docker Images
- Building Standard
	- A Dockerfile is used to specify the configuration for building images
	- In the file, we specify the directory, the base image to use
	- Any ports used should be specified using the `EXPOSE {port_number}` command
	- Containers should have an `ENTRYPOINT` which specifies what will happen when the container is run
		- `CMD` provides for additional arguments which will be run and passed to `ENTRYPOINT`
- Building with Docker Compose
	- Used for <mark style="background: #FFB86CA6;">multi-container docker applications</mark>
	- Works as a 3-step process
		- Define the environment with the Dockerfile
		- Define the services that make up the app in docker-compose.yml
		- Run `docker-compose up` and compose starts to run the whole app
- Publishing to Docker Registries (DockerHub)
	- First need to add a tag to the built container
		- `docker tag {container_name} <DOCKER_ACCOUNT_NAME>/<CUSTOM_IMAGE_NAME>`
	- Then login to DockerHub with `docker login`
		- For SSO or third-party sign-in, generate a Personal Access Token on DockerHub
	- Push to DockerHub using 
		- `docker push {container_name} <DOCKER_ACCOUNT_NAME>/<CUSTOM_IMAGE_NAME>`
## Containerized Model Deployment
- Model source code is not enough to deploy. The container must also include a model artifact which we can use for inference
- The `flask` library lets us run models as APIs and `gunicorn` lets us deploy production-grade deployment servers
	- Uses the same code, so we don't have to make any changes to productionize flask
- When we run the model API container, we will need to make sure to expose and bind to the correct port for our service to be accessible