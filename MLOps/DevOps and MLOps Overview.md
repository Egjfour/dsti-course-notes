|   Course Name    | Topic |  Professor  |      Date      | Tags |
| :--------------: | :---: | :---------: | :------------: | :--: |
| **Name in Bold** | Topic | Joe Sanchez | Date of course |      |

[Professor Notes Link (Devops)](https://github.com/adaltas/dsti-mlops-2025-spring/blob/main/01.devops-introduction/index.md)
[Professor Notes Link (MLOps)](https://github.com/adaltas/dsti-mlops-2025-spring/blob/main/02.mlops-introduction/index.md)

# Summary
*The core principles of both DevOps and MLOps are around automation and quality control. While both of these paradigms apply to deployed code in production systems, MLOps also concerns itself with data and the deployed model as an entire pipeline.*

# Key Takeaways
1. DevOps is a culture of human communication, technical processes, and tools
2. Semantic versioning follows the `MAJOR.MINOR.PATCH-LABEL` format
3. MLOPs brings models to production by automating individual repetitive steps

# Definitions
- DevOps: Setting up automation to ensure high quality code in production
- Service Level Indicator (SLI): Metric for software solutions monitored over time
	- Latency, Failures per request, downtime, etc
- Service Level Objectives (SLO): Targets for the cumulative success of SLIs over a period of time
	- Green/Yellow/Red business metric objectives
- Service Level Agreement (SLA): Promise by a service provider to a customer about availability
	- Processing will be complete in one hour
- MLOps: Streamline and optimize the ML lifecycle to address critical challenges in modern data science

# Additional Resources
- [Site Reliability Engineering Principles](https://medium.com/@alexbmeng/site-reliability-engineering-principals-fd52229bfcd6)
- [Continuous Delivery and Automation Pipelines in Machine Learning](https://cloud.google.com/architecture/mlops-continuous-delivery-and-automation-pipelines-in-machine-learning)

# Notes
## DevOps (Development Operations)
- DevOps came about as part of site reliability engineering in 2014 and adopted many principles of the [[Agile|Agile]] development framework
- DevOps is a culture that is focused on using tools to automate and track every aspect of the software's lifecycle from development to decommissioning
- ![[Pasted image 20250323093341.png]]
## Naming and Versioning
- Since communication is a cornerstone of DevOps, it is important for there to be consistency and meaning in how things are named
- Naming
	- Names should be meaningful, differentiated, singular, using full names when possible, and as short as possible while still ensuring other quality conditions 
	- Naming with different scopes
		- Typically the ordering it `project_component_environment`
	- Conflicts
		- First apply rules of the community/ecosystem then then company/project, then your own rules
- Versioning (Semantic Versioning)
	- This system is commonly used for software packages and follows the following syntax
		- `MAJOR.MINOR.PATCH-LABEL`
	- `MAJOR` - version when you make incompatible API changes,
	- `MINOR` - version when you add functionality in a backward compatible manner, and
	- `PATCH` - version when you make backward compatible bug fixes.
	- `LABEL` - for pre-release and build metadata are available as extensions
		- Example: `1.0.0-beta`
## MLOps (Machine Learning Operations)
- MLOps is about introducing quality and reproducibility by automating individual steps
- While code is also deployed (pre-processing/feature engineering) like in DevOps, MLOps also deploys a model and sometimes data
	- A <mark style="background: #FFB86CA6;">full pipeline</mark> is deployed in MLOps
- ![[Pasted image 20250323104742.png]]