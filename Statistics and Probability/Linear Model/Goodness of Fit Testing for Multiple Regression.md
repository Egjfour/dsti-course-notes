|                 Course Name                  |        Topic         |    Professor    |       Date       |    Tags     |
| :------------------------------------------: | :------------------: | :-------------: | :--------------: | :---------: |
| **Advanced Statistics and Machine Learning** | Linear Model Testing | Christine Malot | 06 novembre 2025 | #Statistics |

[Class Video Link](https://dstisas.sharepoint.com/sites/RecordingsArchive/_layouts/15/stream.aspx?id=%2Fsites%2FRecordingsArchive%2FShared%20Documents%2FA24%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20251106%5F084942%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Ed61c708c%2Dfe34%2D4269%2Dbf5d%2D576b40734e56)

# Summary
*A 3-4 sentence description of what was learned in italics*

# Key Takeaways
1. The main challenge with testing the Gaussian noise assumption is that there are no observed values of the error term, so we must instead consider the model residuals
2. Like in the simple case, [[Simple Linear Model|standardized and particularly studentized residuals]] are essential for performing tests on a multiple regression
3. The [[Hypothesis Testing|KS test]] will tend to under-reject the null hypothesis for small datasets since $\sqrt n D_n$ only converges as $n$ increases
4. In Chi-Square Goodness-of-Fit testing, we should not have theoretical counts less than 5 (else the approximations may not be correct), so we must group infrequent categories
5. If the Gaussian assumption is violated, we can look to make clusters of individuals for whom we can assume constant noise. This is done by calculating a new response vector, $A^{-1}Y$

# Definitions
- The Projection Matrix on $\mathbb X$ ($P_{\mathbb X}$): The matrix which moves our observed output values into the linear subspace defined by our design matrix
	- $P_{\mathbb X} = \mathbb X(\mathbb X^T\mathbb X)^{-1}\mathbb X^T$
- 

# Additional Resources
- Name the hyperlink in brackets then outside the brackets put the URL in parens

# Notes
## Residuals
- We know from the simple linear model, that our model residuals vector $\hat U = RY$ with $R = I - P_{\mathbb X}$
	- This gives an expectation of 0 and a variance of $\sigma^2R$
- The issue arises that the residuals have unequal variances and thus are NOT identically distributed, so we must transform them for analysis
	- This means <mark style="background: #FFB86CA6;">histograms for residuals are inappropriate</mark>
- Standardized Residuals
	- Fix the problem by creating identically distributed residuals, but we do not know their distribution
	- $T_i = \dfrac{\hat \epsilon_i}{\hat\sigma_n\sqrt{1 - h_i}}$ with $h_i$ as the diagonal term of the projection matrix
- Studentized Residuals
	- Much more computationally heavy but result in residuals which are identically distributed student random variables
	- The process calculates a model for each observation excluding that observation to estimate the standard deviation
	- $T_i^* = \dfrac{\hat \epsilon_i}{\hat\sigma_{n,i}\sqrt{1-h_i}}$ with $\hat\sigma_{n,i}$ an [[Point Estimators|estimator]] for $\sigma^2$ <mark style="background: #FFB86CA6;">without observation i</mark>
	- Ultimately, $\forall i \in [1,n], T_i^* \sim \mathcal T((n-1)-rk(\mathbb X))$
## Kolmogorov Smirnov (KS)-Test
- This is a test on the distribution of the residuals. In particular, the studentized residuals
- In R, we perform this using `kd.test(data_vector, {dist. fxn}, {dist. params})`
- Test Overview
	- Let $X_1, \dots, X_n$ observations to an [[Random Variables|iid random variable]]
	- Let $F$ a [[Distributions of Probability and Random Variables|distribution function]]
	- Hypotheses
		- $H_0$: $F$ is the distribution function of the $X_i$
		- $H_1$: This is not the case
- We consider the distribution function using the [[Descriptive Statistics|empirical cumulative distribution function]], <mark style="background: #FFB86CA6;">not the density function</mark>
	- The ECDF, $F_n$, is a random object and represents a trajectory when evaluated on a dataset
- The KS Statistic: $D_n = \underset{x}{sup}|F_n(x) - F(x)|$
	- This converges towards the KS Distribution: $\sqrt n D_n \underset{n\to\infty}{\to}K$
	- We also know that $F_n \underset{n\to\infty}{\to}F_{X_1}$ with $F_{X_1}$ the distribution function of $X_1$
	- We want to compare $F_{X_1}$ and $F$, but since $F_{X_1}$ is unknown, we replace with $F_n$
- To perform this with a linear model in R
	- Create the model object using `lm()`
	- Get the studentized residuals by passing the fitted model into `rstudent`
	- Use the output of `rstudent` (`resids`) in `ks.test(resids, pt, {df})`
		- $df = n - rk(\mathbb X) - 1$ with $rk(\mathbb X)$ the number of explanatory variables plus the intercept
## Chi-Square Goodness of Fit Test
- The KS test is generally preferable for a continuous outcome, but in practice, many people use the $\chi^2$-GOF test
	- This test is generally more appropriate for discrete variables (counts, categories, etc)
- The traditional test compares $X_i$ against a fully-precised distribution $P_\theta$
	- Rejecting the null may mean either the same distribution function with different parameters (e.g., $\theta^1 \ne \theta$) or an entirely different distribution (e.g., $P^1 \ne P$)
- We create an ordered table of values with observed and theoretical counts

| Value | Observed Count ($x_i$) | Theoretical Count ($m_i$)                       |
| ----- | ---------------------- | ----------------------------------------------- |
| 1     | $n_1$                  | $nP_1$                                          |
| 2     | $n_2$                  | $nP_2$                                          |
| ...   | ...                    | ...                                             |
| k-1   | $n_{k-1}$              | $nP{k-1}$                                       |
| k     | n_k                    | $(1 - \underset{k=1}{\overset{k-1}{\sum}}P_k)n$ |
- The last theoretical count handles everything $\ge k$
- Calculate the $\chi^2$ statistic as the sum of the squared distances
	- $\sum\dfrac{(x_i - m_i)^2}{m_i} = \sum\dfrac{x_i^2}{m_i} - n = D^2$
	- Intuitively: $\dfrac{(\textrm{observed} - \textrm{expected})^2}{\textrm{expected}}$
- Under $H_0$, $D^2 \sim \chi^2(k-1)$
- This test can be generalized to a test of a family of distributions
	- We first, estimate the parameters of the distribution of interest given the data
	- Then compute the estimation of $P_i$ using the theoretical distribution with the estimated parameters
	- Then we calculate $D^2$ using the estimations of $P_i$
		- <mark style="background: #FFB86CA6;">This estimation, however, changes the degrees of freedom</mark> for the distribution to $k-1-m$ with $m$ the number of estimated parameters
	- Since the degrees of freedom are different, we must manually calculate the p-value
		- In R: `1 - pchisq(chisq_stat, df_corrected)`