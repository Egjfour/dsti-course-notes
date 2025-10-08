|       Course Name        |      Topic       |     Professor     |       Date        | Tags |
| :----------------------: | :--------------: | :---------------: | :---------------: | :--: |
| **Agent-Based Modeling** | Model Validation | Gregoriy Bobashev | 16 septembre 2025 |      |

# Summary
*Validation of ABM models is quite different than the other model types since there aren't expected rules or consistent methodologies. It is all highly model-dependent. Typically, we have to determine how to aggregate individual-level metrics. Additionally, it is imperative to ensure these models are calibrated correctly which requires doing sensitivity analyses among other things.*

# Key Takeaways
1. Sensitivity analysis on the model parameters and initial conditions is a highly effective way to determine the potential issues with your model
2. There are many types of uncertainty and the risk they pose to the validity of your model determines how to best handle them

# Definitions
- Internal Testing: Are the equations programmed correctly with no bugs
	- "First-order validation", "reliability", "verification"
- Internal Validation: Are inputs and outputs consistent with the data used to create the model
	- "Second-order validation", "calibration"
- External Validation: Does the model match other data, not explicitly used to create it
	- "Third-order validation"
- Cross Validation: Does the model reach the same conclusions as other models
- Predictive Validity: Does the model make accurate predictions about future events
- Face Validity: Does the model pass the sniff test/intuition
- Parameterization: Finding reasonable parameters values
- Calibration: A type of parameterization to reproduce specific values

# Notes
## Model Calibration
- Models are either parameterized with external analyses (statistical/expert) or can be calibrated such that parameters are chosen to achieve a specific result
- Calibration strategies
	- Select a certain number of parameters of interest
	- Choose categorical vs "best-fit" calibration
- Using Model Statistics
	- Important to note if we're looking for means or extreme values when comparing scenarii
	- 95% trajectory bands are useful to understand the space of likely outcomes
	- We can use correlative relationships to understand the impact of parameters and initial values
		- This is particularly possible with the Behavior Space add-in for [[NetLogo Programming|NetLogo]]
## Handling Uncertainty
- Sensitivity analyses allow us to explore the impact to the model for small changes in parameters and initial conditions
	- Uncertainty is the uncertainty in our parameter values and this translates directly to the trustworthiness of our model results
	- A sensitivity analysis in a joint parameter space requires evaluating a latin hypercube. Typically this is done with a global [[Model Types and Use Cases|Monte Carlo simulation]]
- Sources of Uncertainty
	- Structural uncertainty (robustness) where the change in structure is the condition upon which we evaluate
	- The inputs to the model itself and internal rules as well as parameter estimation are all sources of uncertainty
## Model Validation
- ABMs have a "triple curse"
	- There is no concept of a p-value or likelihood like in statistical models
	- There are not necessarily known laws and measurements like in [[Data Assimilation Overview|system dynamics]]
	- Process models repeat many times so we can get solid statistics unlike with ABMs
- Common Sense Issues
	- If a theoretical model follows common sense, it is useless
	- If there is an unusual outcome, how do we know if it's a model artifact or an actual discovery
- Practical Validation
	- Define with an [[ODD Protocol and Documentation|ODD]] to ensure objective alignment
	- SME validation of the conceptual model and results
	- Sensitivity analysis
	- Compare with observed data using statistics/ML to show plausibility
	- Visual inspection of the pattern observed from the model