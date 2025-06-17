|                        Course Name                        |        Topic         |    Professor    |     Date      |    Tags     |
| :-------------------------------------------------------: | :------------------: | :-------------: | :-----------: | :---------: |
| **Foundations of Statistics and Machine Learning Part 2** | Parameter Estimation | Christine Malot | 30 avril 2025 | #Statistics |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/blaise_pascal_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fblaise%5Fpascal%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FA24%20%2D%20Common%20Link%20DS%5FDE%5FDA%2D20250430%5F085052%2DMeeting%20Recording%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Edbce762b%2Dd817%2D45a2%2Da676%2Dcacdf48cff7e)

# Summary
*Point estimators take observations of random variables and use a [[Real Functions of a Real Variable|real function]] to produce an estimation of the parameters for the underlying distribution of the random variable. Estimators are random variables, but estimators are real values. Given that, estimators can have an expected value (and other moments) as well as a density function. This expected value tells us if the estimator is unbiased (i.e., the expected value is equal to the parameter being estimated).*

# Key Takeaways
1. The goal of point estimation is to get an idea about parameters ($\theta$) thanks to observations\
2. An estimator MUST NOT depend on the unknown value of itself or any other parameter
3. Estimators are random variables but estimation is a real, not a random object
4. For all [[Distributions of Probability and Random Variables|identically distributed]] random variables, $\mathbb E[\bar X_n] = \mathbb E[\bar X_1]$
5. Asymptotically unbiased estimators are biased
6. The distribution function of the uniform distribution is $(F_X(t))^n$

# Definitions
- Parametric Estimation: Identify the parameters of the distribution of a [[Random Variables|random variable]]
- Non-Parametric Estimation: Estimate density of a random variable without the underlying parameters
	- Example: Histograms
- Estimator: A function of $X_1, \dots, X_n$ for which we can compute a value for $\theta$ thanks to the dataset/observations
- Point Estimation: The value of the estimator computed thanks to the observations
- Unbiasedness: The expected value of the estimator of a parameter is the parameter
	- $\forall n \ge 1;\hspace{1.5mm} \mathbb E[\hat\theta_n] = \theta$
- Asymptotically Unbiasedness: An estimator which is unbiased only as the sample size approaches infinity
	- $\underset{n \to \infty}{lim}\mathbb E[\hat \theta_n] = \theta$
- Bias: The difference between the expected value of the estimator and the actual parameter
	- $b_{\theta}(\hat\theta_n) = \mathbb E[\hat\theta_n] - \theta$

# Additional Resources
- [Parametric vs Nonparametric Methods](https://www.geeksforgeeks.org/difference-between-parametric-and-non-parametric-methods/)

# Notes
## Estimators for Point Estimation
- When first analyzing data, always plot it to try and understand the likely distribution family
- Some naive estimators can be created, but not all are correct
	- Using $min(X_1)$ and $max(X_1)$ is correct for estimating the parameters $a$ and $b$ of a [[Random Variables|uniform random variable]], but using the height of the first histogram class is a bad estimator for the [[Random Variables|exponential distribution]] parameter $\lambda$
- General Framework:
	- We have observations $X_1, \dots, X_n$ and $X_i$ is an observation of the random variable $X_i$
	- We additionally assume that $X_1, \dots, X_n$ are [[Distributions of Probability and Random Variables|iid]] random variables with a common distribution $P_{\theta}, \theta$ unknown
	- Create a function which provides an idea about $\theta$ based on the observations
- Example: For a [[Random Variables|Gaussian random variable]], $\mu$ and $\sigma^2$ are the parameters we want to estimate
	- $\dfrac{1}{n}\underset{k=1}{\overset{n}{\sum}}(X_k - \mu)^2$ is NOT an estimator for $\sigma^2$ since it relies on unknown parameter $\mu$
	- $\dfrac{1}{n}\underset{k=1}{\overset{n}{\sum}}(X_k - \bar X)^2$, however, is an estimator for $\sigma^2$ since it has no unknown parameter values
- Notation: An estimator for parameter $\theta$ constructed with $X_1, \dots, X_n$ is denoted $\hat \theta_n$
	- The hat generally means estimator and $n$ is the length of the dataset
	- The same notation is also used for the estimation of the estimator
## Biasedness
- A biased estimator is one such that the expectation of the estimator does not yield the parameter value being estimated
- When $\hat \theta_n$ is not unbiased, the bias is defined as $b_{\theta}(\hat\theta_n) = \mathbb E[\hat\theta_n]-\theta$
- Estimators which are not biased may, however, be asymptotically unbiased such that the expectation of the estimator only equals the parameter as the sample size approaches infinity
	- $\underset{n \to \infty}{lim}\mathbb E[\hat \theta_n] = \theta$
### Example - Determine if an estimator is biased
- Problem Statement
	- Are the following estimators unbiased for $X_1, \dots, X_k$ i.i.d. $\mathcal U(0, \theta)$
	- $\hat\theta_{n,1} = max(X_k)$ and $\hat\theta_{n,2}=2\cdot\bar x_n$
- First, identify that both are estimators
	- Neither $\hat\theta_{n,1}$ nor $\hat\theta_{n,2}$ rely on unknown parameters. Thus, they are estimators
- Calculate the expectation for $\hat\theta_{n,1}$
	- Since this is not a linear transformation, we must determine the distribution of $\hat\theta_{n,1}$ and cannot use the transfer formula
		- For this, we need a [[Random Variables|density function]]
	- Density function process:
		- Need to determine a [[Distributions of Probability and Random Variables|distribution function]] and then deduce by taking the derivative of the distribution
	- Distribution function $F_{\hat\theta_{n,1}}$:
		- Let $t \in \mathbb R$, $F_{\hat\theta_{n,1}}(t) = P(\hat\theta_{n,1} \le t) = P(max(X_k) \le t)$
		- This also equals the joint probability that each observation $\le t$
			- Since observations are independent., this is the product of each probability: $\underset{k=1}{\overset{n}{\prod}}P(X_k \le t)$
			- Additionally, since they are identically distributed, this product can use a single random variable from the vector $=P(X_1 \le t)^n = (F_X(t))^n$
		- Since we have $X \sim \mathcal U(0,\theta)$, we have $F_X(t) = \begin{cases}0 \text{ if } t \lt 0\\ \dfrac{t}{\theta} \text{ if } t \in [0, \theta]\\ 1 \text{ otherwise }\end{cases}$
		- This gives for our parameter $F_{\hat\theta_{n,1}}\begin{cases}0 \text{ if }t \lt 0\\ \dfrac{t^2}{\theta^2}\text{ if } t \in [0, \theta]\\1 \text{ if }t \gt \theta\end{cases}$
	- Density function $f_{\hat\theta_{n,1}}$:
		- $f_{\hat\theta_{n,1}} = F_{\hat\theta_{n,1}}'$
		- So, $f_{\hat\theta_{n,1}} = \begin{cases}n\cdot\dfrac{t^{n-1}}{\theta^n}\text{ if }t\in]0,\theta[\\0\text{ otherwise }\end{cases}$
	- Now compute the expectation of the density function $\mathbb E[f_{\hat\theta\_{n,1}}]$
		- $\int_{\mathbb R}x\cdot\dfrac{nx^{n-1}}{\theta^n}=\dfrac{n}{\theta^n}[\dfrac{X^{n+1}}{n+1}]_0^{\theta} = \dfrac{n}{\theta^n}\cdot\dfrac{\theta^{n+1}}{n+1} = \dfrac{n}{n+1}\cdot\theta$
	- As we can see, this expectation does not equal $\theta$, so $\hat\theta_{n,1}$ is not unbiased
		- However, since $\underset{n\to\infty}{lim}\dfrac{n}{n+1} = 1$, $\underset{n\to\infty}{lim}\mathbb E[f_{\hat\theta_{n,1}}] = \theta$
		- Thus, $\hat\theta_{n,1}$ is asymptotically unbiased
- Calculate the expectation for $\hat\theta_{n,2}$
	- $\mathbb E[\hat\theta_{n,2}] = \mathbb E[2\cdot \bar X_n] = 2 \cdot \mathbb E[\bar X_n]$
	- The expectation of $\bar X_n$ is the expectation of one observation of the random variable because they are i.i.d. $\mathbb E[\bar X_n] = n\cdot\dfrac{1}{n}\cdot\mathbb E[X_1]=\mathbb E[X_1]$
	- Since $X \sim \mathcal U(0, \theta)$, $\mathbb E[X_1] = \dfrac{\theta}{2}$
	- Thus, the $\mathbb E[\hat\theta_{n,2}] = 2 \cdot \dfrac{\theta}{2} = \theta$
	- So, $\hat\theta_{n,2}$ is unbiased
## Transforming a Biased Estimator Into an Unbiased One
- We need to modify the estimator to have an expectation equal to $\theta$
- BEWARE: This <mark style="background: #FFB86CA6;">modification cannot involve introducing unknown parameters</mark>
	- Example: $\hat\theta_{n,3} = \hat\theta_{n,1} + \dfrac{\theta}{n + 1}$ has a dependency on $\theta$ and is NOT an estimator
- Consider the example from above $\hat\theta_{n,1} = max(X_n)$
	- We know $\mathbb E[\hat\theta_{n,1}] = \dfrac{n}{n+1}\cdot\theta, \text{ so }\dfrac{n+1}{n}\cdot\mathbb E[\hat\theta_{n,1}] = \theta$
	- Therefore, a debiased estimator $\hat\theta_{n,4}$ can be defined as $\dfrac{n+1}{n}\cdot max(X_k)$
- Ultimately, any estimator can be debiased by finding a way to make the expected value of the estimator equal the parameter being estimated so long as such a method does not introduce the unknown parameter into the estimator function