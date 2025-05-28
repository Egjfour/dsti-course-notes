|                        Course Name                        |   Topic   |    Professor    |      Date      |    Tags     |
| :-------------------------------------------------------: | :-------: | :-------------: | :------------: | :---------: |
| **Foundations of Statistics and Machine Learning Part 2** | Intervals | Christine Malot | 05-06 mai 2025 | #Statistics |

[Class Video Link 1](https://dstisas-my.sharepoint.com/personal/blaise_pascal_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fblaise%5Fpascal%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FA24%20%2D%20Common%20Link%20DS%5FDE%5FDA%2D20250505%5F085243%2DMeeting%20Recording%201%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E31320220%2Db160%2D4d6c%2Db594%2Debcebb2b4ef3)

# Summary
*A 3-4 sentence description of what was learned in italics*

# Key Takeaways
1. The smaller the value of $\alpha$, the wider the interval will be
2. Before calculating an interval, we \should be able to calculate a point estimator and have some idea about its distribution
3. In the Gaussian setting with known variance, the reduced version of $\bar X_n - \mu$ is distributed $\mathcal N(0, \frac{\sigma^2}{n})$
4. A confidence interval for $\mu$ with level $100(1-\alpha)\%$ when $X_1, \dots, X_n$ are iid [[Random Variables|Gaussian random variables]] with known variance $\sigma^2$ is $[\bar X_n - \frac{\sigma}{\sqrt N} \cdot Z_{1-\alpha_2},\hspace{1.5mm} \bar X_n + \frac{\sigma}{\sqrt N} \cdot Z_{1-\alpha_1}]$
5. A plug-in may change the distribution used for the estimator
6. A confidence interval for $\mu$ with unknown variance with level $100(1-\alpha)$ when $X_1,\dots,X_n$ are iid Gaussian random variables is $[\bar X_n - \frac{\hat\sigma_n}{\sqrt N} \cdot t_{1-\alpha_2;\hspace{1mm}n-1},\hspace{1.5mm} \bar X_n + \frac{\hat\sigma_n}{\sqrt N} \cdot t_{1-\alpha_1;\hspace{1mm}n-1}]$
7. Thanks to the [[Convergence|Central Limit Theorem]], we know that $\sqrt n \frac{\bar X_n - \mu}{\sigma}\underset{d}{\to}\mathcal N(0,1)$, so when $n \ge 30$, an approximated distribution for $\sqrt n \frac{\bar X_n}{\sigma}$ is $\mathcal N(0,1)$
8. We can approach a [[Distributions of Probability and Random Variables|binomial distribution]] by a Gaussian to estimate intervals of estimators of proportions
9. In a binomial distribution, the smaller the probability of success, the greater the inaccuracy and need for many observations
10. An interval for an estimator of variance in the Gaussian setting is $[\hat\sigma^2_n \cdot \frac{n-1}{C_{1-\alpha_2;\hspace{1mm}n-1}};\hspace{1.5mm}\hat\sigma^2_n \cdot \frac{n-1}{C_{\alpha_1;\hspace{1mm}n-1}}]$

# Definitions
- Confidence Interval: A confidence interval for $\theta$ with confidence level $100(1-\alpha)$ is an interval $[A_n, B_n]$ such that $A_n$ and $B_n$ are functions of $X_1, \dots, X_n$ that can be evaluated thanks to data and which produce $P(\theta \in [A_n, B_n]) = 1 - \alpha$
	- The probability of our [[Point Estimators|point estimator]] is within the range created by $A_n$ and $B_n$
- Plug-in: Replacing one unknown parameter with an estimator
- Symmetric Confidence Interval: A confidence interval such that $\alpha_1 = \alpha_2$ and that is centered around the estimator
	- Gaussian w/ known variance: $[\bar X_n - \frac{\sigma}{\sqrt n}\cdot Z_{1-\alpha/2};\hspace{1.5mm}\bar X_n + \frac{\sigma}{\sqrt n} \cdot Z_{1-\alpha/2}]$
- Unilateral Confidence Interval: A confidence interval for an upper or lower bound. The other side of the interval is $+\infty$ or $-\infty$
	- Gaussian w/ known variance - upper bound: $]-\infty;\hspace{1.5mm}\bar X_n + \frac{\sigma}{\sqrt n} \cdot Z_{1-\alpha}]$
- Slutsky Theorem: Given a pair of random variables, if one [[Convergence|converges in distribution]] to a random element and the other towards a constant ($X_n \underset{d}{\to} X$ and $Y_N \underset{d}{\to} c$), then:
	- $X_n + Y_n = X + c$
	- $X_n \cdot Y_n = cX$
	- $X_n / Y_n = X/c$

# Additional Resources
- Name the hyperlink in brackets then outside the brackets put the URL in parens

# Notes
## Overview
- Confidence intervals are important because estimations for estimators vary, so we want to understand the magnitude of these fluctuations
- Just like estimators, a confidence interval cannot depend on unknown parameters
- The default level of $\alpha$ is 0.05
	- The goal is to make this as small as possible while still providing useful information
- There is no general method to construct the functions which comprise the interval: $A_n$ and $B_n$, but there is a typical framework
	- Step 1: Identify the distribution for the estimator
	- Step 2: Use the estimator to create the functions for $A_n$ and $B_n$ using $P_n$ and $S_n$
		- Note: $A_n$ and $B_n$ are random variables themselves
	- Step 3: Write the equations of $A_n$ and $B_n$ as a probability that the true parameter is inside the interval
	- Step 4: Modify the probability such that $P_n$ and $S_n$ are by themselves and such that the probability is equal to $\alpha$
	- Step 5: Change the center portion of the inequality to get to a known distribution
	- Step 6: Write the [[Probability Theory|probability of the disjoint events as the sum of the probability]]
	- Step 7: Set these probabilities as equal to $\alpha_1$ and $\alpha_2$ respectively and recognize this as a [[Distributions of Probability and Random Variables|quantile function]]
	- Step 8: Solve for $P_n$ and $S_n$ and then substitute back into $A_n$ and $B_n$
## Interval for Expectation - Gaussian - Known Variance
- Framework: Consider $X_1, \dots, X_n$ iid random variables. We want to calculate a confidence interval for the expectation $\mu$ with confidence level $100(1-\alpha)\%$
	- Assume $X_1,\dots, X_n \sim \mathcal N(\mu, \sigma^2)$ with $\sigma^2$ known
- The classical estimator for $\mu$ is $\bar X_n$
- Step 1: Identify the distribution for the estimator
	- Since $X_1, \dots, X_n$ iid <mark style="background: #FFB86CA6;">(must have independence)</mark>, $\begin{pmatrix}X_1\\ \vdots \\ X_n\end{pmatrix}$ is a [[Random Vectors|Gaussian Random Vector]]
		- Because $\bar X_n$ is a linear combination of this Gaussian Random Vector, it is a Gaussian Random Variable
	- So, we know that $\mathbb E[\bar X_n] = \mu$ and $\mathbb V[\bar X_n] = \frac{\mathbb V[X_1]}{n} = \frac{\sigma^2}{n}$
	- Thus $\bar X_n \sim \mathcal N(\mu, \frac{\sigma^2}{n})$ -- note, this is an exact distribution, not an approximation
- Step 2: Use the estimator to create the functions for $A_n$ and $B_n$ using $P_n$ and $S_n$
	- Since $\bar X_n$ is around $\mu$: $A_n = \bar X_n - S_n$ and $B_n = \bar X_n + P_n$
		- Note: Having $S_n = P_n$ is <mark style="background: #FFB86CA6;">not necessarily required</mark> though is common
- Step 3: Write the equations of $A_n$ and $B_n$ as a probability that the true parameter is inside the interval
	- $P(\mu \in [A_n, B_n]) = P(\mu \in [\bar X_n - S_n, \bar X_n + P_n]) = 1 - \alpha = I$
	- Also stated as $P(\bar X_n - S_n \le \mu \le \bar X_n + P_n)$
- Step 4: Modify the probability such that $P_n$ and $S_n$ are by themselves and such that the probability is equal to $\alpha$
	- Rearrange the probability from step 3: $P(-S_n \le \bar X_n - \mu \le P_n) = 1-\alpha$
- Step 5: Change the center portion of the inequality to get to a known distribution
	- See that $\bar X_n - \mu \sim \mathcal N(0,\frac{\sigma^2}{n})$
	- Need to consider the reduced/scaled version of $\bar X_n - \mu$ by dividing by the standard deviation: $(\bar X_n - \mu)/\sqrt{\frac{\sigma^2}{n}} = \sqrt n (\frac{\bar X_n - \mu}{\sigma}) \sim N(0,1)$ 
	- So, $I = P(\frac{-\sqrt n P_n}{\sigma} \le \sqrt n (\frac{\bar X_n - \mu}{\sigma}) \le \frac{\sqrt n S_n}{\sigma}) = 1 - \alpha$
- Step 6: Write the probability of the disjoint events as the sum of the probability
	- Take the complementary event: $\alpha = P(\{\sqrt n (\bar X_n - \mu)/\sigma \lt \frac{-\sqrt n P_n}{\sigma}\} \cup \{\frac{\sqrt n S_n}{\sigma} \lt \sqrt n (\bar X_n - \mu)/\sigma\})$
- Step 7: Set these probabilities as equal to $\alpha_1$ and $\alpha_2$ respectively and recognize this as a quantile function
	- Take $\alpha_1, \alpha_2$ positive with a $\alpha_1 + \alpha_2 = \alpha$
	- $\alpha_1 = P(\sqrt n (\bar X_n - \mu)/\sigma \lt \frac{-\sqrt n P_n}{\sigma})$
	- $\alpha_2 = P(\frac{\sqrt n S_n}{\sigma} \lt \sqrt n (\bar X_n - \mu)/\sigma)$
		- Need to solve for $1-\alpha_2$ since $\alpha_2$ does not represent a distribution function
- Step 8: Solve for $P_n$ and $S_n$ and then substitute back into $A_n$ and $B_n$
	- $\frac{-\sqrt n P_n}{\sigma} = Z_{\alpha_1} \Leftrightarrow P_n = \frac{-\sigma}{\sqrt n} \cdot Z_{\alpha_1}$
	- $\frac{\sqrt n S_n}{\sigma} = Z_{1-\alpha_2} \Leftrightarrow S_n = \frac{\sigma}{\sqrt n} \cdot Z_{1 - \alpha_2}$
	- Thus, $A_n = \bar X_n - \frac{\sigma}{\sqrt n} \cdot Z_{1-\alpha_2}$ and $B_n = \bar X_n - \frac{\sigma}{\sqrt n} \cdot Z_{\alpha_1}$
		- We know that $B_n \lt A_n$ because $1-\alpha_2$ is the right tail
		- So, we convert $B_n$ to be $\bar X_n + \frac{\sigma}{\sqrt n}z_{1-\alpha_1}$ since the Gaussian is symmetric
	- This gives us a confidence interval for $\mu$ with confidence level $100(1-\alpha)\%$ when $X_1,\dots,X_n$ are iid Gaussian random variables with expectation $\mu$ and known variance
		- $[\bar X_n - \frac{\sigma}{\sqrt n}z_{1-\alpha_2};\hspace{1.5mm}\bar X_n + \frac{\sigma}{\sqrt n}z_{1-\alpha_1}]$ with $\alpha_1 \ge 0, \alpha_2 \ge 0, \alpha_1 + \alpha_2 = \alpha$
## Interval for Expectation - Gaussian - Unknown Variance
- Framework: Consider $X_1, \dots, X_n$ iid random variables. We want to calculate a confidence interval for the expectation $\mu$ with confidence level $100(1-\alpha)\%$
	- Assume $X_1,\dots, X_n \sim \mathcal N(\mu, \sigma^2)$ with $\sigma^2$ unknown
	- The previous intervals cannot be used since they would depend on an unknown parameter
	- $\sigma^2$ should be replaced with an estimator: $\hat \sigma^2$
- Steps 1-4 are the same as the Gaussian case with known variance
	- Producing $P(-S_n \le \bar X_n - \mu \le P_n) = 1-\alpha$
- Step 5: Change the center portion of the inequality to get to a known distribution
	- We cannot use $\sqrt n (\bar X_n - \mu)/\sigma$ since it depends on unknown parameter $\sigma$
	- Instead, we should consider $\sqrt n (\bar X_n - \mu)/\hat\sigma_n$, but we also should have an idea about the distribution of this random variable
	- Properties of $\hat\sigma^2_n$ <mark style="background: #FFB86CA6;">(only apply because we are in the Gaussian setting)</mark>
		- An unbiased estimator for $\hat\sigma_n^2$ is $\frac{1}{n-1}\underset{k-1}{\overset{n}{\sum}}(X_k - \bar X_n)^2$
			- Can be rewritten as $(n-1)\frac{\hat\sigma_n^2}{\sigma^2}$
		- We see that this estimator is distributed $\chi^2(n-1)$ with $\mathbb E[Y_k] = 0$ and $\mathbb V[\hat\sigma_n^2] = \frac{n-1}{n}$
			- $Y_k = \frac{X_k - \bar X_n}{\sigma} = \frac{1}{\sigma}(X_k - \bar X_n)$
		- We also know that $\hat\sigma_n^2 \perp \!\!\! \perp \bar X_n$
	- We can decompose $\sqrt n (\bar X_n - \mu)/\hat\sigma_n$ as $\frac{\sqrt n (\bar X_n - \mu)/\sigma}{\sqrt {\frac{(n-1)(\hat\sigma_n^2/\sigma^2)}{n-1}}}$
		- This gives us a [[Random Variables|Student variable]] distributed $\mathcal T(n-1)$
	- Therefore, we can state that we want to find $P(\frac{\sqrt n P_n}{\hat\sigma_n} \le \sqrt n \frac{\bar X_n - \mu}{\hat\sigma_n} \le \frac{\sqrt n S_n}{\hat\sigma_n}) = 1 - \alpha$
- The remaining steps are the same as in the Gaussian case with known variance except that we use the Student - $\mathcal T(n-1)$ - distribution
	- $-\frac{\sqrt n P_n}{\hat\sigma_n}$ and $\frac{\sqrt n S_n}{\hat\sigma_n}$ are quantiles of the Student distribution
- Applying the quantiles, we get the interval $[\bar X_n - \frac{\hat\sigma_n}{\sqrt n}t_{1-\alpha_2;\hspace{1mm}n-1}; \hspace{1.5mm} \bar X_n + \frac{\hat \sigma_n}{\sqrt n}]$
## Interval for Expectation - Not Gaussian - Known Variance
- Framework: Let $X_1, \dots, X_n$ be a random variable with expectation $\mu$ and variance $\sigma^2$. Scope is a confidence interval for $\mu$
- The classical point estimator is still $\bar X_n$ with $\mathbb E[\bar X_n] = \mu$ and $\mathbb V[\bar X_n] = \frac{\sigma^2}{n}$
- The Central Limit Theorem lets us solve this in the exact same way as the Gaussian case with known variance because $\sqrt n \frac{\bar X_n - \mu}{\sigma}\underset{d}{\to}\mathcal N(0,1)$
- So, the calculation is exactly the same as the interval for the expectation in the Gaussian setting EXCEPT we now <mark style="background: #FFB86CA6;">only have asymptotical convergence of the estimation</mark>
	- $e.g., \underset{n\to\infty}{lim}P(\mu \in [\bar X_n - \frac{\sigma}{\sqrt n}Z_{1-\alpha_2};\hspace{1.5mm}\bar X_n + \frac{\sigma}{\sqrt n}Z_{1-\alpha_1}]) = 1-\alpha$
## Interval for Expectation - Not Gaussian - Unknown Variance
- Framework: Let $X_1, \dots, X_n$ be a random variable with expectation $\mu$ and unknown variance $\sigma^2$. Scope is a confidence interval for $\mu$
- Again, consider $\bar X_n$ an estimator for $\mu$ which gives $\sqrt n \frac{\bar X_n - \mu}{\sigma}\sim \mathcal N(0,1)$ thanks to the Central Limit Theorem
- Like in the Gaussian case with unknown variance, we use the plug-in method with $\sqrt n \frac{\bar X_n - \mu}{\hat\sigma_n}$
	- But we should have an idea about the distribution of this random variable
- This is not $\mathcal T(n-1)$ because $\sqrt n \frac{\bar X_n - \mu}{\hat\sigma_n}$ is not $\mathcal N(0,1)$ and $(n-1) \frac{\hat\sigma_n^2}{\sigma^2}$ not $\chi^2(n-1)$
	- But we can say that $\hat\sigma_n^2 \underset{as}{\to}\sigma^2$ and thus $\hat\sigma_n \underset{as}{\to} \sigma$ since square root is a continuous function
	- This additionally means that $\hat\sigma_n \underset{p}{\to} \sigma$, and therefore, $\frac{\hat\sigma_n}{\sigma}\underset{p}{\to}1$
	- We can show <mark style="background: #FFB86CA6;">through the application of Slutsky, that</mark> $\sqrt n \frac{\bar X_n - \mu}{\hat\sigma_n} \underset{d}{\to} \mathcal N(0,1)$
- Thus, $1-\alpha = P(-\sqrt n/\hat\sigma_nP_n \le \sqrt n \frac{\bar X_n - \mu}{\hat\sigma_n} \le \sqrt n S_n / \hat\sigma_n)$
	- And this gives that $1-\alpha = P(-\sqrt n/\hat\sigma_nP_n \le N \le \sqrt n S_n / \hat\sigma_n)$ with $N \sim N(0,1)$ as an <mark style="background: #FFB86CA6;">approximated/asymptotic confidence interval</mark>
- Once we solve, we get the interval as $[\bar X_n - \frac{\hat\sigma_n}{\sqrt n}Z_{1-\alpha_1}; \hspace{1.5mm}\bar X_n + \frac{\hat\sigma_n}{\sqrt n}Z_{1-\alpha_2}]$
## Interval for Proportions
- Framework: Consider $X_1, \dots, X_n$ iid $\mathcal B(p)$. Goal is to estimate $p$ and construct an interval for $p$
- Remark: $\mathbb E[X_1] = p$, so we want an estimator for the [[Moments of Random Variables|expectation]]
- Remark: $\mathbb V[X_1] = p(1-p)$
- Because of the two remarks, this is a <mark style="background: #FFB86CA6;">special case of the interval for a Gaussian expectation with unknown variance</mark>
	- A classical estimator for $p$ is $\bar X_n$ (thanks to remark 1)
- Remark: $n\bar X_n = \underset{k=1}{\overset{n}{\sum}}X_k \sim \mathcal B(n; p)$ and by the central limit theorem, we have that $\frac{\sqrt n \bar X_n -p}{\sqrt{p(1-p)}} \underset{d}{\to}\mathcal N(0,1)$
	- So, for $n$ large enough, an approximated distribution for $\bar X_n$ is $\mathcal N(p, p(1-p)/n)$ and we can approach a binomial distribution with a Gaussian
- Using the same computations as the non-Gaussian, known variance expectation interval
	- $A_n = \bar X_n - \frac{\sqrt {p (1-p)}}{\sqrt n}\cdot Z_{1-\alpha_2}$ and $B_n = \bar X_n + \frac{\sqrt{p(1-p)}}{\sqrt n}\cdot Z_{1-\alpha_1}$
	- These cannot, however, be confidence interval bounds since they depend on $p$
	- Since $Z_{1-\alpha_1} \ge 0, Z_{1-\alpha_2} \ge 0$, and $\sqrt{p(1-p)} \le 1/4$, $\bar X_n - \frac{1}{2\sqrt n}Z_{1-\alpha_2} \le A_n$ and $\bar X_n - \frac{1}{2\sqrt n}Z_{1-\alpha_1} \le B_n$
	- AND $P(p \in [A_n, B_n]) \le P(p \in [\bar X_n - \frac{1}{2\sqrt n}Z_{1-\alpha_2};\hspace{1.5mm} \bar X_n + \frac{1}{2\sqrt n}Z_{1-\alpha_1}])$
- This produces an asymptotic confidence interval defined as
	- $[\bar X_n - \frac{1}{2\sqrt n}Z_{1-\alpha_2};\hspace{1.5mm}\bar X_n + \frac{1}{2\sqrt n}Z_{1-\alpha_1}]$
## Interval for Variance - Gaussian
- Define a [[Point Estimators|point estimator]] for $\sigma^2 = \hat\sigma_n^2 = \frac{1}{n-1}\underset{k=1}{\overset{n}{\sum}}(X_i - \bar X_n)^2$
- In the Gaussian setting, we have $(n-1)\frac{\hat\sigma_n^2}{\sigma^2} \sim \chi^2(n-1)$
	- Want to find $A_n$ and $B_n$ such that $1-\alpha = P(A_n \le \sigma^2 \le B_n)$
- We can define $A_n$ and $B_n$ using $\hat\sigma^2_n$ since it is close to $\sigma^2$
	- $A_n = \hat\sigma^2_n \cdot S_n$
	- $B_n = \hat\sigma^2_n \cdot P_n$
- Thus (step 3), $P(\hat\sigma_n^2S_n \le \sigma^2 \le \hat\sigma_n^2P_n) = 1-\alpha$
- We divide by $\sigma^2$ so we can get the desired random variable ($\chi^2(n-1)$)
	- $P(\frac{\hat\sigma_n^2S_n}{\sigma^2} \le 1 \le \frac{\hat\sigma_n^2P_n}{\sigma^2}) = 1-\alpha$
	- Rewrite: $P(\frac{n-1}{S_n} \le (n-1)\frac{\hat\sigma^2_n}{\sigma^2} \le \frac{n-1}{P_n}) = 1-\alpha$ since $C = (n-1)\frac{\hat\sigma^2_n}{\sigma^2} \sim \chi^2(n-1)$
- The main difference with the other scenarii is that Chi-squared is an asymmetric distribution
	- $P_n = \frac{n-1}{C_{\alpha_1;n-1}}$ and $S_n = \frac{n-1}{C_1-\alpha_2; n-1}$
- This produces a final confidence interval of $[\hat\sigma_n^2\cdot\frac{n-1}{C_{1-\alpha_2;n-1}};\hspace{1.5mm}\hat\sigma_n^2\cdot\frac{n-1}{C_{\alpha_1;n-1}}]$