|                        Course Name                        |                        Topic                        |    Professor    |    Date     |    Tags     |
| :-------------------------------------------------------: | :-------------------------------------------------: | :-------------: | :---------: | :---------: |
| **Foundations of Statistics and Machine Learning Part 2** | Method of Moments and Maximum Likelihood Estimation | Christine Malot | 05 mai 2025 | #Statistics |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/blaise_pascal_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fblaise%5Fpascal%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FA24%20%2D%20Common%20Link%20DS%5FDE%5FDA%2D20250505%5F085243%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Eb7eb5ff4%2D2dc4%2D4c19%2Da4ff%2D199939f9ae53)

# Summary
*There are two primary ways to construct estimators: the method of moments and maximum likelihood estimation. The method of moments is useful when there is only one parameter to estimate and a moment of the random variables can be expressed as a function of the unknown parameter. Maximum likelihood, on the other hand, is more suited to complex solutions and may not arrive at an exact solution. Internally, maximum likelihood estimation solves an optimization problem to find the best parameters given the data provided.*

# Key Takeaways
1. Method-of-moments estimation is mostly for estimation of a single parameter
2. [[Point Estimators|Estimators]] constructed using method-of-moments are note necessarily [[Point Estimators|unbiased]]
3. Maximum Likelihood Estimation involves finding the parameters which have the maximum likelihood given a provided dataset
4. A common estimator (unbiased and convergent) for the [[Moments of Random Variables|expected value of a random variable]] is the empirical mean: $\hat\theta_n = \bar X_n$
5. A common estimator for the **population** variance (**biased**) is $\frac{1}{n}\underset{k=1}{\overset{n}{\sum}}(X_k - \bar X_n)^2$
6. A common estimator for the **sample** variance (**unbiased**) is $\frac{1}{n-1}\underset{k=1}{\overset{n}{\sum}}(X_k - \bar X_n)^2$
7. When a model is assumed to be Gaussian, the maximum likelihood estimation is the same as [[Simple Linear Model|least squares minimization]]

# Definitions
- Likelihood ($\mathcal L(X_1, \dots, X_n;\theta)$): The probability of our parameters correctly specifying the distribution given the observations that we have

# Additional Resources
- [Maximum Likelihood Estimation Explained](https://medium.com/data-science/probability-concepts-explained-maximum-likelihood-estimation-c7b4342fdbb1)

# Notes
## Method of Moments
- The method of moments is a consequence of the [[Distributions of Probability and Random Variables|Law of Large Numbers]]
- Framework
	- Let $X_1, \dots, X_n$ iid random variables whose density depends on an unknown parameter
	- Let $\theta$ a <mark style="background: #FFB86CA6;">function of this unknown parameter</mark>
		- We do not need to estimate the parameter $\theta$ but ANY function of it
- Version 1: Using raw moments
	- Let $k \in \mathbb N$ such that $\exists$ a function $g$ with $\mathbb E[X_1^k] = g(\theta)$
		- "The moment of order $k$ is a function of the unknown parameter $\theta$"
	- An estimator $\hat\theta_n$ for $\theta$ is a solution of $g(\hat\theta_n) = \frac{1}{n}\underset{i=1}{\overset{n}{\sum}}X_i^k$
- Version 2: Using [[Moments of Random Variables|centered moments]]
	- Let $k \in \mathbb N$ such that $\exists$ a function $h$ with $\mathbb E[(X_1 - \mathbb E[X_1])^k] = h(\theta)$
		- "The centered moment of order $k$ is a function of the unknown parameter $\theta$"
	- An estimator $\hat\theta_n$ for $\theta$ is a solution of $h(\hat\theta_n) = \frac{1}{n}\underset{i=1}{\overset{n}{\sum}}(X_i - \bar X_n)^k$
		- with $\bar X_n = \frac{1}{n} \underset{i=1}{\overset{n}{\sum}}X_i$
- Example: Let $X_1,\dots,X_n$ iid on $\mathcal U(0, \theta)$
	- Using the first moment:
		- We know that $\mathbb E[X_1] = \frac{\theta}{2} = g(\theta)$ with $g(x) = \frac{x}{2}$
		- So, an estimator $\hat\theta_{n,1}$ for $\theta$ is $\frac{\hat\theta_{n,1}}{2} = \frac{1}{n}\underset{i=1}{\overset{n}{\sum}}X_i = \bar X_n$
		- Thus $\hat\theta_{n,1} = 2 \cdot \bar X_n$
	- Using the second moment
		- We know that $\mathbb V[X_1] = \frac{\theta^2}{12} = h(\theta)$ with $h(x) = \frac{x^2}{12}$
		- So an estimator $\hat \theta_{n,2}$ for $\theta$ is $\frac{(\hat\theta_{n,2})^2}{12} = \frac{1}{n}\underset{k=1}{\overset{n}{\sum}}(X_k - \bar X_n)^2$
		- Which gives $\hat\theta_{n,2} = \sqrt{\frac{12}{n}\underset{k=1}{\overset{n}{\sum}}(X_k - \bar X_n)^2}$
		- We can see that the complexity for using/computing this estimator is much greater than the first moment
## Maximum Likelihood Estimation
- Framework
	- We have a dataset and want to find the maximum likelihood of the given parameters
	- Let $X_1,\dots,X_n$ iid random variables whose distribution depends on an unknown parameter $\theta$. 
	- In this context, Likelihood is $\mathcal L(X_1,\dots,X_n;\theta) =$
		- Discrete Case: $\underset{k=1}{\overset{n}{\prod}}P(X_1 = X_k)$
		- Continuous Case: $\underset{k=1}{\overset{n}{\prod}}f(X_k)$
- An estimator $\hat\theta_n$ for $\theta$ is such that $\mathcal L(X_1,\dots,X_n;\theta) = \underset{a \in \mathbb R}{max}\mathcal L(X_i,\dots,X_n; a)$
- These estimators are also not necessarily biased, and there is <mark style="background: #FFB86CA6;">no guarantee to have a unique solution</mark>
