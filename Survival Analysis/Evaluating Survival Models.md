|      Course Name      |            Topic             |       Professor        |       Date       |    Tags     |
| :-------------------: | :--------------------------: | :--------------------: | :--------------: | :---------: |
| **Survival Analysis** | Model Evaluation and Testing | Anna Freni Sterrantino | 18 décembre 2025 | #Statistics |

[Class Video Link](https://dstisas.sharepoint.com/sites/RecordingsArchive/_layouts/15/stream.aspx?id=%2Fsites%2FRecordingsArchive%2FShared%20Documents%2FA24%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20251218%5F085809%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Edff478c6%2Dc220%2D43b9%2Db214%2D389c10e5f293)

# Summary
*Evaluating survival models, while similar to [[Evaluation of ML Models & Improving Results|traditional ML model evaluation]] and [[Goodness of Fit Testing for Multiple Regression|goodness of fit]] for regression, has many additional considerations due to the nature of [[Duration Data and Survival Analysis Overview|duration data]]. In particular, measures for assessing predictive power must be modified to fit this context. It is also important to ensure model assumptions are followed, and specific methods exist for ensuring this is the case for [[Semi-Parametric Approaches|Cox models]].*

# Key Takeaways
1. [[Variable Selection - Linear Model|Nested models]] can use the Likelihood Ratio Test
2. Non-nested models can use procedures like [[Variable Selection - Linear Model|stepwise regression]]
3. The sum of squared martingale residuals is not a [[Goodness of Fit Testing for Multiple Regression|goodness of fit]] indicator
4. Highly influential points should be removed and can be identified looking at the case deletion residuals (`"dfbetas"`) of the model

# Definitions
- Concordance Index: Fraction of pairs of subjects whose survival times are correctly order by the model's fitted hazard to <mark style="background: #FFB86CA6;">demonstrate predictive power</mark>

# Additional Resources
- [Model Selection and Calibration (Python - lifelines)](https://lifelines.readthedocs.io/en/latest/Survival%20Regression.html#model-selection-and-calibration-in-survival-regression)

# Notes
## Comparing Nested Models - Likelihood Ratio Test
- Used for analyzing nested models only
- Compares a restricted model ([[Hypothesis Testing|null hypothesis]]) against a less restrictive
	- $H_0: \theta \in \Theta_0$
	- $H_1: \theta \notin \Theta_0$
	- "A simpler model versus a more complex one"
- Rejecting the null means that the more complex model is the better fit
- Test statistic:
	- $LRT_n = \dfrac{sup\{\mathcal L(\theta; y): \theta \in \Theta_0\}}{sup\{L(\theta; y): \theta \in \Theta\}}$
- This is provided as part of the `coxph` output in R against the <mark style="background: #FFB86CA6;">null hypothesis of an intercept-only model</mark>
	- Two fitted [[Semi-Parametric Approaches|Cox models]] can be provided to the `anova` function as well to compare subsets of coefficients directly
## Comparing Non-Nested Models - [[Variable Selection - Linear Model|AIC and BIC]]
- AIC can compare any set of models <mark style="background: #FFB86CA6;">on the same dataset</mark>
- $AIC = -2 \cdot\log(\mathcal L(\theta)) + 2k$
	- Lower AIC implies better model quality
- AIC can be used in [[Variable Selection - Linear Model|stepwise regression]] procedures to automatically identify the best model which balances complexity and fit
	- Requires that we first define a full model
	- Then we use function `step`
## Assessing Predictive Power
- Concordance Index
	- Fraction of pairs of patients whose survival times are correctly ordered by the model-fitted hazard
	- One of the outputs of the `summary` function
	- A <mark style="background: #FFB86CA6;">higher value is better</mark>
- [[Conditional Probability and Independence|Sensitivity and Specificity]]
	- The classic definition changes in the context of survival to account for [[Duration Data and Survival Analysis Overview|duration data]]
		- $Z = min(c, t)$: Minimum of censoring time or the event time ("follow-up time")
		- $\delta$ as a censoring indicator
			- 1 if $T \le C$ else 0
		- $D(t) = 1$ if $R \le t$  (failure status/disease)
			- The event has not yet happened at time $t$
		- $X$ is a continuous variable of interest
			- We <mark style="background: #FFB86CA6;">use a predictor to inform sensitivity and specificity</mark> in survival analysis
		- $sens(c, t) = Pr(X > c|D(t) = 1) = S_1(c, t)$
		- $spec(c, t) = Pr(X \le c|D(t) = 0) = S_0(c, t)$
		- The challenge is to choose the right value of $c$
			- *Could* use the predicted time as $X$ and set a threshold $c=t$
	- These metrics in a survival analysis context look at a <mark style="background: #FFB86CA6;">single point in time</mark> and are not a global metric to assess the model
- ROC/AUC
	- Sensitivity and specificity are used to create a harmonized index relative to the best possible model (100% correct)
	- R offers the `survivalROC` package which calculates survival ROC curves
		- Need to extract the predicted time by calling `predict({cox model}, type = "lp")`
## Diagnostics: Analyzing Residuals
- Martingale Residuals
	- Properties
		- Sum to 1
		- Distributed between $-\infty$ and 1
		- Each has an expected value of 0
		- Sum of squares does not show goodness of fit
		- Patterns may suggest <mark style="background: #FFB86CA6;">alternative functional forms for continuous covariates</mark>
- Case deletion (`type = "dfbetas"`)
	- Measures difference between a model fitted with the given observation and one which excludes the current observations to look for overly influential points
	- Large residuals should be removed from the data and the model refitted

## Testing the [[Semi-Parametric Approaches|Proportional Hazards Assumption]]
- We can see potential violations by examining the log-log plot
	- $-\log(-\log(S(t)))$
	- The curves should be parallel across time
- Schoenfeld residuals can be used to test the model under the <mark style="background: #FFB86CA6;">assumption that the hazards are proportional</mark>
	- Evaluated in R using `cox.zph({cox model})`
	- These residuals are distributed $\chi^2$
- Schoenfeld residuals can also be plotted with time on the x-axis and the estimates coefficient on the y-axis
	- A flat line indicates proportional hazards (coefficients do not change as a function of time)
	 ![[Pasted image 20260118163328.png]]
- If we reject proportional hazards, the Cox model has many [[Semi-Parametric Approaches|extensions]] to solve for this