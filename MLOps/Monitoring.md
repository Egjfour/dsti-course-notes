| Course Name |            Topic            |  Professor   |     Date     | Tags |
| :---------: | :-------------------------: | :----------: | :----------: | :--: |
|  **MLOps**  | Drift Detection - Evidently | Alexis Marié | 24 mars 2025 |      |

[Professor Notes Link](https://github.com/adaltas/dsti-mlops-2025-spring/blob/main/11.monitoring/index.md)

# Summary
*ML models in production are at-risk for many problems even if the [[Deployment (CI-CD and Containers)|deployment]] is perfect. These arise from changes in the world that interacts with the model and manifests in the data. The Evidently library offers a framework for testing these underlying changes over time.*

# Key Takeaways
1. With ML in production, there are many places to monitor because ML depends on infrastructure, data, and the model 
2. MLFlow is organized around runs
3. MLFlow integrates into already-existing code

# Definitions
- Run: Executions of a piece of data science code
	- A full retraining of a model with reporting metrics calculation
- Data Drift: Change in the distribution of the variables
- Concept Drift: The statistical properties of the target variable change over time; business problem changes

# Additional Resources
- [How Often to Retrain (Evidently)](https://www.evidentlyai.com/blog/retrain-or-not-retrain)
- [Evidently Walkthrough](https://www.evidentlyai.com/blog/tutorial-1-model-analytics-in-production)

# Notes
## Motivations
- There are many concerns related ML deployments in production
- We want to discover failures before end-users do
	- Especially important to automate since many failures will be silent
 ![[Pasted image 20250329133349.png]]
## Data Monitoring
- 2 main issues that could arise over time
	- Quality Issues
		- Discontinued features
		- Content or feature type changes (age to age group)
		- Anonymization of data ([[GDPR|GDPR]])
	- Content Issues
		- Distribution changes
			- Market changes like competition / COVID
- Data Content
	- Data Drift: Change in distribution of predictors
		 ![[Pasted image 20250329135212.png]]
	- Concept Drift: Changes in the target variable
		- Can be sudden (market shock) or gradual (new competitor)
			 ![[Pasted image 20250329135319.png]]
## Handling Stale Models
- Model needs to learn new state of the world
	- Retrain
	- Build new model
- Qualifying Decisions
	- When is ‘bad behavior’ bad enough?
	- Is enough data available?
	- What are new underlying rules?