|      Course Name      |    Topic     |       Professor        |         Date          |    Tags     |
| :-------------------: | :----------: | :--------------------: | :-------------------: | :---------: |
| **Survival Analysis** | Cox PH Model | Anna Freni Sterrantino | 17 & 18 décembre 2025 | #Statistics |

[Class Video Link]((https://dstisas.sharepoint.com/sites/RecordingsArchive/_layouts/15/stream.aspx?id=%2Fsites%2FRecordingsArchive%2FShared%20Documents%2FA24%2FA24%20-%20Common%20Link%20DSDEDA-20251217_085734-Meeting%20Recording1%2Emp4&ga=1)

# Summary
*The Cox Proportional Hazards model is the flagship method for performing general regression-based analysis of survival data. It natively supports multiple covariates (including continuous) unlike [[Non-Parametric Approaches|non-parameteric tests]] and has a convenient interpretation through the hazard ratio. This model assumes proportional hazards which is critical to its validity, and because of the [[Duration Data and Survival Analysis Overview|link between the hazard and survival functions]], can be used to predict survival.*

# Key Takeaways
1. The Cox Proportional Hazards Model allows for testing of multiple groups, assessing continuous factors, and, in-general, performing regression analysis
2. Partial likelihood is necessary since failure times are [[Duration Data and Survival Analysis Overview|censored]]
3. Failing to account for non-constant hazard ratios threatens validity of Cox model estimates
4. With a lower hazard ratio, the treatment has fewer expected events and thus, a better survival rate than the control
5. Hazard ratios are centered at 1, meaning that if an estimated hazard ratio is 1, there is no difference on risk between treatment and control
6. A hazard ratio of 2 means that the treatment has twice the hazard of the control or a 100% increase - therefore, a worse survival

# Definitions
- Partial [[Constructing Estimators|Likelihood]]: Compare the hazard of subject $i$ to the [[Duration Data and Survival Analysis Overview|cumulative hazard]] of all subjects at-risk at time $j$
	- $\mathcal l(\beta) = \underset{j=1}{\overset{D}{\prod}}\dfrac{h_0(t_j)exp(x_{i_{(j)}}\beta)}{\underset{k \in R}{\sum}h_0(t_j) exp(x_k\beta)} = \underset{j=1}{\overset{D}{\prod}}\dfrac{exp(x_{i_{(j)}}\beta)}{\underset{k \in R}{\sum}exp(x_k\beta)}$
	 ![[Pasted image 20260117134320.png]]
- Hazard Ratio: The ratio comparing the hazard for treatment to control
	- $HR = \dfrac{h(t|X_1 = 1)}{h(t | X_1 = 0)} = \dfrac{h_0(t)exp(b_1)}{h_0(t)} = exp(b_1)$
- Proportional Hazards: The effects of the covariates on the hazard are constant over time
	- Represented by parallel survival curves that should not cross
	 ![[Pasted image 20260117153735.png]]

# Additional Resources
- [Understanding Cox PH and Partial Likelihood (Medium)](https://medium.com/data-science/survival-analysis-optimize-the-partial-likelihood-of-the-cox-model-b56b8f112401)

# Notes
## Cox Proportional Hazards Model
- Instead of estimating $S(t)$ directly, this model <mark style="background: #FFB86CA6;">estimates changes to the hazard function</mark>
- Considered semi-parametric since no distribution is assumed
- Model naturally accommodates right censoring and time-varying covariates
- Highly extensible
	- Random effects or recurrent events/clustering
	- Competing risk modeling
- Model specification
	- $h_i(t) = h_0(t) exp(x_i^T\beta)$ with
		- $h_i(t)$: The hazard for subject $i$ at time $t$
		- $h_0(t)$: The baseline hazard at time $t$
		- $x_i^T$: The vector of covariates for subject $i$
		- $\beta$: The vector of <mark style="background: #FFB86CA6;">multiplicative effects of each covariate on risk</mark>
	- $exp(x_i^T)$ is the hazard ratio for covariates $x_i$ comparing to a subject with $x = 0_p$
- The model does NOT require specification of the baseline
	- Instead, the <mark style="background: #FFB86CA6;">model focuses only on the effect of the covariates</mark>
- To estimate this effect, $\hat\beta$, we maximize the partial likelihood function
- Model Assumptions
	- The <mark style="background: #FFB86CA6;">key assumption of this model is proportional hazards</mark>
		- The effect of treatment does not change over time. Though an individual subject's hazard function can change over time
	- This assumption can be tested using [[Evaluating Survival Models|Schoenfeld residuals]]
- In R, we can estimate such a model using the `coxph` function from package `survival`
	- `coxph(formula = {Surv} ~ {features}, data = df)`
	 ![[Pasted image 20260117152651.png]]
## Interpretation of the Model
- The exponentiation of the estimated coefficients $\hat \beta$ gives the hazard ratio comparing to the baseline control
	- Or a one-unit increase of the regressor
- When this hazard ratio is lower, the treatment has fewer expected events = better survival
- The proportional hazard regression is lined via the log transformation to the hazard ratio
	- $\log(HR(x_i)) = \log (\dfrac{h(t|x)}{h_0(t)}) = \beta x$
- The log of the baseline acts as an intercept which can change over time
- Linear predictors act multiplicatively on the baseline odds
	- In contrast with the [[Simple Linear Model|linear model]] where the predictors are additive with respect to the intercept
- With multiple covariates, <mark style="background: #FFB86CA6;">a coefficient represents a change for that specific factor caeteris paribus</mark>
## Prediction Using the Cox Model
- Predicted Hazard: $\hat h_0(t_i) = d_i/\underset{j \in R_i}{\sum}exp(x_j\hat\beta)$
- Predicted Cumulative Hazard: $\hat H_0(t) = \sum h_0(t_j), t_j \le t$
- Predicted Survival: $\hat S_0(t) = exp(-\hat H_0(t))$
- <mark style="background: #FFB86CA6;">Predicted Conditional Survival:</mark> $\hat S(t|x) = [S_0(t)]^{exp(x\beta)}$
- In R, we can get these estimates on new data directly with
	- `survfit({fitted cox}, newdata = {data.frame})`