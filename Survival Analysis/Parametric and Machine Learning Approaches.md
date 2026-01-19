|      Course Name      |           Topic           |       Professor        |       Date       |       Tags       |
| :-------------------: | :-----------------------: | :--------------------: | :--------------: | :--------------: |
| **Survival Analysis** | Advanced Survival Methods | Anna Freni Sterrantino | 19 décembre 2025 | #MachineLearning |

[Class Video Link](URL)

# Summary
*In addition to the classic methods for modeling [[Duration Data and Survival Analysis Overview|duration data]], parametric and ML approaches were created to handle for various complexities and leverage advances in other fields. As these methods become increasingly complex and black-box, interpretability and evaluation is paramount, so there are many model-agnostic explanation methods and metrics.*

# Key Takeaways
1. Accelerated failure time focuses on survival time whereas [[Semi-Parametric Approaches|Cox PH]] focuses on the hazard rate
2. The greater the survival difference between the nodes, the better the split

# Definitions
- Log-Rank: A measure of separation between two sets of subjects with survival times

# Additional Resources
- [AFT Model](https://en.wikipedia.org/wiki/Accelerated_failure_time_model)
- [XGBoost Survival Cox vs AFT]([https://xgboosting.com/configure-xgboost-survivalaft-objective/](https://xgboosting.com/configure-xgboost-objective-survivalcox-vs-survivalaft/))
- [LIME Values (Interpret)](https://interpret.ml/docs/lime.html)
- [Survex (model-agnostic explanations for Survival ML models)](https://cran.r-project.org/web/packages/survex/readme/README.html)

# Notes
## Situations for Other Models
- When the [[Semi-Parametric Approaches|proportional hazard assumption]] does not hold: Accelerated Failure Time
- When there are multiple events: Competing Risk
- When there are too many covariates: [[Variable Selection - Linear Model|Penalized Regression]]
- When there are interaction or nonlinear effects which must be included: [[CART Algorithm & Random Forests|Random Forest]] Survival
## Parametric Approaches
- Survival time is modeled as a function of the predictor variables
	- But this requires you to choose a distribution unlike the Cox Model
- Accelerated Failure Time
	- Model the survival time directly
		- Common popular distributions are log-logistic and Weibull
	- Assume the effect of covariates is to accelerate or decelerate the time to event
	- Model Specification
		- $Y = \log(T) = \alpha + \beta X + \sigma\epsilon$ ; with $T$ the survival time
		- Without censoring, we could use standard [[Simple Linear Model|OLS]]
	- Interpretation
		- Positive coefficients indicate that an increase in the covariate leads to an increase in survival time
	- Acceleration factor is similar to the hazard ratio except that a value > 1 demonstrates a survival benefit
		- Must have the AFT assumption for this to be true: $S(t) = q$ ("the <mark style="background: #FFB86CA6;">effect of a covariate is to accelerate or decelerate the survival time by some constant</mark>")
		- $\gamma = \dfrac{[-\log(q)]exp(\alpha_0 + \alpha_1X)}{[-\log(q)]exp(\alpha_0)} = exp(\alpha_1)$
- Weibull Model
	- Fully-parameterized modeling of the [[Duration Data and Survival Analysis Overview|hazard function]]
	- Specification
		- $h(t) = \lambda pt^{p-1}; \lambda, p > 0$
	- Interpretation
		- $p > 1$ increases hazard $p = 1$ constant, and $p < 1$ decreases the hazard
	- A hazard ratio can be estimated from this model if the PH assumption holds
	- An acceleration factor can be estimated if the AFT assumption holds
- Use Case Summary
	 ![[Pasted image 20260119165906.png]]
## Penalized Regression
- Ridge and lasso handle for problems with multicollinearity or high dimensionality
- Elastic net introduces a dual penalty which uses both the [[Variable Selection - Linear Model|L1 and L2 norms]]
	- This can be applied in R using `glmnet` with parameter `family="cox"`
	- We add the elastic net penalty to the [[Semi-Parametric Approaches|partial likelihood]] calculation
## Random Survival Forest
- Many individual trees predict survival time and then are averaged out
- For survival analysis, the [[CART Algorithm & Random Forests|split decision]] is based on the maximum log rank
	- As log rank increases, survival difference between the nodes increases
- The terminal nodes of the individual trees then use bootstrapped [[Non-Parametric Approaches|nonparametric estimation]] to derive the survival function
## Explaining Models
- `SurvSHAP` values create a survival model's prediction decomposed into contributions of features over time
	- SHAP values are calculated at each time point
	- The <mark style="background: #FFB86CA6;">attribution curves for each predictor are time-dependent</mark>. A variable may increase survival early on but then have a different effect later
- `SurvLIME` values are a simpler view that don't provide a time-dependent decomposition
	- Fits a simple surrogate model around the observation (simulates data in the neighborhood of the observation) being explained (usually Cox)
	- The coefficients of the surrogate model are the explanation for that observation
- Global Model Explanations
	- Variable dependence uses Ceteris Paribus profiles to understand the effect of a change of a variable on the change in the outcome
	- The Brier Score is another method which represents the time-dependent mean squared error adjusted for censoring
	- The area under curve metric measures how well the model of interest differentiate observations who experienced the event of interest by a time t (cumulative cases) from observations for which the event occurred after this time (dynamic controls)
	- The C-index is non-time dependent and looks at the ranking quality of a model's risk scores and measures the ratio of concordant pairs