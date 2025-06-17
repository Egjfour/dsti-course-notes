|                        Course Name                        |        Topic         |    Professor    |     Date      |    Tags     |
| :-------------------------------------------------------: | :------------------: | :-------------: | :-----------: | :---------: |
| **Foundations of Statistics and Machine Learning Part 2** | Estimator Evaluation | Catherine Malot | 30 avril 2025 | #Statistics |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/blaise_pascal_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fblaise%5Fpascal%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FA24%20%2D%20Common%20Link%20DS%5FDE%5FDA%2D20250430%5F085052%2DMeeting%20Recording%201%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Ebbb30791%2D1501%2D493e%2Da623%2D8efefd2bc69f)

# Summary
*Estimators which are unbiased are not inherently convergent. For an estimator to converge, it must converge in probability towards the actual parameter. To show this, the Bienaymé-Tchebyshev inequality is used because it provides an upper bound on the probability of the absolute difference between the random variable and its expectation.*

# Key Takeaways
1. For [[Distributions of Probability and Random Variables|identically distributed]] random variables, $\mathbb E[\bar X_n] = \mathbb [X_1]$, and when they are additionally independent, $\mathbb V[\bar X_n] = \dfrac{\mathbb V[X_1]}{n}$
2. One [[Point Estimators|estimator]] is considered better than another if the mean quadratic error is lower
3. When an estimator is unbiased, the mean quadratic error equals the variance
4. If an estimator is [[Point Estimators|unbiased or asymptotically unbiased]] and the variance approaches zero as n approaches infinity, then the estimator is convergent

# Definitions
- Convergent/Consistent Estimator: An estimator which [[Convergence|converges in probability]] towards the actual parameter
- Cramer-Rao Bound: The level at which an estimator cannot be improved. This is defined as 1 over the Fisher information $\dfrac{1}{I(\theta)}$

# Additional Resources
- [Mean Square Convergence](https://www.statlect.com/asymptotic-theory/mean-square-convergence)
- [Bienaymé-Tchebyschev](https://proofwiki.org/wiki/Bienaym%C3%A9-Chebyshev_Inequality#google_vignette)

# Notes
## Convergence of Estimators
- Definition
	- Let $\hat\theta_n$ be an estimator for $\theta$, we say that $\hat\theta_n$ is convergent if $\hat\theta_n\underset{p}{\to}\theta$
- Proposition: Bienaymé-Tchebyshev Inequality
	- Let $X$ a random variable with a variance (we know therefore that there is an expectation as well)
	- $\forall \epsilon \gt 0, \hspace{1mm} P(|X-\mathbb E[X]| \gt \epsilon) \le \dfrac{\mathbb V[X]}{\epsilon^2}$
	- This can be used to identify an upper bound and prove convergence
- Example: Consider $X_1, \dots, X_n$ iid with $\mathcal U(0,0)$. We know that $\hat\theta_{n,2}=2\bar X_n$ is unbiased. Is it also convergent?
	- Need to see if $\forall \epsilon \gt 0, P(|\hat\theta_{n,2} - \theta| \gt \epsilon) \underset{n \to \infty}{\to} 0$
		- Can use $\theta = \mathbb E[\hat\theta_{n,2}]$ because it is unbiased
	- We know, thanks to the Bienaymé-Tchebyshev inequality that if $\mathbb V[\hat\theta_{n,2}]$ exists, then $\forall \epsilon \gt 0, \hspace{1mm} P(|\hat\theta_{n,2} - \mathbb E[\hat\theta_{n,2}]| \gt \epsilon) \le \dfrac{\mathbb V[\hat\theta_{n,2}]}{\epsilon^2}$
	- So we need to calculate $\mathbb V[\hat\theta_{n,2}]$
		- $\mathbb V[\hat\theta_{n,2}]=\mathbb V[2\cdot\bar X_n] = \mathbb V[\dfrac{2}{n}\underset{k=1}{\overset{n}{\sum}}X_k] = \dfrac{4}{n^2}\mathbb V[\underset{k=1}{\overset{n}{\sum}}X_k]$
		- Because of independence: $\dfrac{4}{n^2}\underset{k=1}{\overset{n}{\sum}}\mathbb V[X_k]$
		- Because identical distributions: $\dfrac{4}{n}\mathbb V[X_1] = \dfrac{4}{n}\cdot\dfrac{\theta^2}{12}=\dfrac{\theta^2}{3n}$
	- This variance gives $P(|\hat\theta_{n,2} - \mathbb E[\hat\theta_{n,2}]| \gt \epsilon) \le \dfrac{\theta^2}{3n \cdot \epsilon^2}$
		- As $n\to\infty$, this quantity approaches 0
	- And since the inequality is upper bounded, $\forall \epsilon,\hspace{1mm} P \to 0$ as $n\to\infty$
- We see that when $\hat\theta_n$ is unbiased (or asymptotically unbiased), if the variance approaches zero as n approches infinity, then it is also convergent
## Estimator Comparison
- The mean quadratic error is used to compare estimators to each other
	- Defined as $MQE(\hat\theta_n)=\mathbb E[(\hat\theta_n - \theta)^2]$
	- The MQE represents a distance between $\hat\theta_n$ and $\theta$
	- We say that $\hat\theta_{n,1}$ is better than $\hat\theta_{n,2}$ is $MQE(\hat\theta_{n,1}) \le MQE(\hat\theta^{n,2})$
- <mark style="background: #FFB86CA6;">Practical formulation of MQE:</mark>
	- $MQE(\hat\theta_n) = \mathbb V[\hat\theta_n] + (b_{\theta}(\hat\theta_n))^2$
		- Variance plus the [[Point Estimators|squared bias]]
		- When the estimator is unbiased, the mean quadratic error is equal to the variance because the bias is zero
- Cramer's Rule: $\forall \hat\theta_n$ unbiased, we have Cramer-Rao bound $\le \mathbb V[\hat\theta_n]$
	- If an estimator is equal to this bound, there can be no improvement
	- The Cramer-Rao Bound is 1 over the Fisher Information with Fisher information as
		- $n \mathbb E_{x;\theta}[(\dfrac{\partial log(X;\theta)}{\partial \theta})^2]$ with $log(X;\theta)$ is the log-likelihood, and in the case of iid variables is just the density function