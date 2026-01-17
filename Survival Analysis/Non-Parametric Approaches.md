|      Course Name      |           Topic           |       Professor        |       Date       |    Tags     |
| :-------------------: | :-----------------------: | :--------------------: | :--------------: | :---------: |
| **Survival Analysis** | Kaplan-Meier and Log-Rank | Anna Freni Sterrantino | 17 décembre 2025 | #Statistics |

[Class Video Link](https://dstisas.sharepoint.com/sites/RecordingsArchive/_layouts/15/stream.aspx?id=%2Fsites%2FRecordingsArchive%2FShared%20Documents%2FA24%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20251217%5F085734%2DMeeting%20Recording1%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E7f4fc28a%2Dea40%2D457f%2D9b71%2D1c349ed5b6ab)

# Summary
*Non-parametric methods are powerful and often-used in survival analysis because of their flexibility, lack of assumptions, and interpretability. These methods are used to estimate [[Duration Data and Survival Analysis Overview|survival functions]] using empirical data. Among the estimators, the most well-known is the Kaplan-Meier estimator. There are also non-parametric tests which allow for comparison of survival functions across groups. The most well known of these is the log rank test and its variants.*

# Key Takeaways
1. With the Kaplan-Meier estimator, survival estimates do not change if someone drops due to censoring, but the number of subjects at-risk will drop
2. The Fleming-Harrington test is useful for studies with delayed effects

# Definitions
- Kaplan-Meier [[Point Estimators|Estimator]]: The proportion of those at risk that survive time point $t_i$
	- $\hat S_{km}(t) = \underset{t_i \le t}{\Pi}(1 - \hat q_i) = \underset{t_i \le t}{\Pi}(1 - \dfrac{d_i}{n_i})$ with
		- $n_i$: the number of subjects at risk time $t_i$
		- $d_i$: the number of subjects failing at time $t_i$
- Stratified Testing: Comparing survival between groups controlling for potentially confounding factors (gender, age group, hospital, etc)

# Additional Resources
- [Kaplan-Meier Estimator Overview](https://stats.oarc.ucla.edu/wp-content/uploads/2025/02/survival_r_full.html#formula-for-kaplan-meier-estimator)
- [Hypergeometric Distribution Models](https://www.geeksforgeeks.org/engineering-mathematics/mathematics-hypergeometric-distribution-model/)

# Notes
## The Kaplan-Meier Estimator
- [[Point Estimators|Non-parametric estimators]] work by ordering all observations by failure time ascending and creating an empirical step [[Duration Data and Survival Analysis Overview|survival function]]
- To handle [[Duration Data and Survival Analysis Overview|censoring]], the censored observations are not counted as an event, but rather we consider the conditional probabilities between actual observations
- The estimator considers, at each relevant timestep, the <mark style="background: #FFB86CA6;">proportion of the number of events relative to the number of remaining subjects</mark>
- Example
	 ![[Pasted image 20260117114525.png]]
	- $0 < t < 50$: $\hat S(t) = 1$
	- $t = 50$: $\hat S(t) = 1 - \frac{1}{5} = 0.8$
	- $50 < t < 70: \hat S(t) = 0.8$ (since no events happen in this period, survival prob. is constant)
	- $t = 70$:
		- $Pr(T > 70) = Pr((T > 70) \cap (T > 50)) = Pr(T > 70 | T > 50) \cdot Pr(T > 50)$
		- $\hat S(t) = (1 - \frac{1}{3}) \cdot \frac{4}{5} \approx 0.533$
- Censored subjects <mark style="background: #FFB86CA6;">only contribute to the probability while they remain in the study</mark>
	- Thus, this estimator is a [[Properties of Sums and Products|product]] of [[Conditional Probability and Independence|conditional probabilities]]
- The R [[Duration Data and Survival Analysis Overview|survival plot]] uses this estimator by default
- The example above can be summarized into the following
	 ![[Pasted image 20260117120059.png]]
- This estimator (and the result table above) is what is calculated when using `survfit` in R
	- `survfit(Surv(time, status) ~ 1, data = df)`
	- Can be automatically plotted using `plot`
## Nelson-Aalen / Fleming-Harrington Estimator
- Consider that $q_j$ is the empirical estimation of instantaneous risk at time $t_j$
- These can then be cumulated to estimate the [[Duration Data and Survival Analysis Overview|hazard function]]
	- $\hat H_j = \underset{i=1}{\overset{j}{\sum}}q_i$
- The survival estimator can then be calculated as $\hat S_{NA}(t_j) = e^{-\hat H_j}$
	- This estimator takes advantage of the relationship between the survival and hazard functions
- In R, we still use function `survfit` but change parameter `type` to `"fh"`
- Using the example above, this estimator is calculated using the following
	 ![[Pasted image 20260117125149.png]]
## Group Comparisons: Log-Rank Test
- A [[Hypothesis Testing|hypothesis test]] is used to <mark style="background: #FFB86CA6;">compare survival functions</mark>
	- $H_o: S_1(t) = S_0(t)$
	- $H_1:$ This is not the case
- This test considers the following table
	 ![[Pasted image 20260117125628.png]]
- Under the assumption of independence, $d_{0i}$ follows a hypergeometric distribution
	- Hypergeometric is a version of the [[Distributions of Probability and Random Variables|geometric distribution]] where <mark style="background: #FFB86CA6;">selections are made without replacement</mark>
	- $\mathbb E[d_{0i} | n_i, d_i, n_{0i}, n_{1i}] = n_{0i}d_i/n_i$
	- $\mathbb V[d_{0i} | n_i, d_i, n_{0i}, n_{1i}] = \dfrac{(n_{0i}n_{1i}d_i(n_i - d_i))}{n^2_i(n_i - 1)}$
- We sum over all time points $t_i$
	- $U_0 = \sum(d_{0i} - e_{0i})$
	- with $\mathbb V[U_0] = \sum \mathbb V[d_{0i}] = V_0$
- This produces the [[Hypothesis Testing|test statistic]]
	- $\dfrac{U_0^2}{V_0} \sim \chi^2_1$
- We can perform this test using the `survdiff` function from the `survival` package in R
	![[Pasted image 20260117130603.png]]
- A weighted version of the log-rank test is the Fleming-Harrington test
	- $U_0(w) = \sum w_i(d_{0i} - e_{0i})$
	- $\mathbb V[U_o] = \sum w_i^2 v_{0i} = \mathbb V_0(w)$
	- To perform this test in R, we provide parameter `rho` to the `survdiff` function
		- If `rho = 0`, we have standard log-rank, and as `rho` increases, we have a higher weight on the earlier survival times
- If we have a categorical stratification, the stratified log-rank test can be used
	- In this case, we compare sums of $U_0$ and $V_0$ across all the groups
	- $X^2 = \dfrac{(\sum_g U_{0g})^2}{\sum_g V^2_{0g}} \sim \chi^2_1$
	- In R, we use the `strata` wrapper when defining the model specification
		- `survdiff(Surv(time, status) ~ group + strata(factor), data = df)`