|                             Course Name                             |    Topic    |     Professor      |      Date       |    Tags     |
| :-----------------------------------------------------------------: | :---------: | :----------------: | :-------------: | :---------: |
| **Foundations of Statistical Analysis and Machine Learning Part 1** | Convergence | Christophe Bécavin | 17 janvier 2025 | #Statistics |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/johnny_najjar_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fjohnny%5Fnajjar%5Fdsti%5Finstitute%2FDocuments%2FRecordings%281%29%2FA24%20%2D%20Common%20Link%20%2D%20DS%2DDE%2DDA%2D20250117%5F095153%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Eaf980465%2D9a2f%2D407d%2Dbe63%2D73b314a28a40)

# Summary
*Convergence is the link between theoretical distributions and random variables to concrete data from the real world. Of course, it is not technically feasible to measure statistics from the entire population, so a random sample is instead used. This random sample, provided it is iid, converges in distribution towards the expectation for the random variable as the size of the sample increases.*

# Key Takeaways
1. As sample size increases, the distribution of a sample approaches the theoretical distribution
2. Almost-sure convergence $\implies$ convergence in probability $\implies$ convergence in distribution
3. The universal boundary exists for every distribution
4. For convergence to be achieved, the values in the random sample must be [[Distributions of Probability and Random Variables|independently and identically distributed]]

# Definitions
- Random Sample: A sample with size n drawn from the population of parameter distribution $f(\theta),$ the parameter $\theta \in \Theta$ (the parameter space)
- Statistics: Measuring samples from a [[Random Variables|random variable]] using functions of the random sample

# Additional Resources
- [Proof of the Central Limit Theorem](https://medium.com/@oguo/proof-of-the-central-limit-theorem-214813be6e2c)
- [Weak vs Strong Law of Large Numbers](https://math.stackexchange.com/questions/2024255/what-is-the-difference-between-the-weak-and-strong-law-of-large-numbers)
- [Almost-Sure Convergence (and general convergence)](https://www.probabilitycourse.com/chapter7/7_2_7_almost_sure_convergence.php)

# Notes
## Convergence in Distribution
- Notation:
	- $X_i$ - statistical (from a random sample)
	- $X$ - probabilistic (describes a population)
	- $X_i \sim X$: The statistic is distributed according to a population random variable
- $X_n \overset{d}{\to} X \textrm{ iff } \forall x, \underset{{n \to \infty}}{lim} F_{X_n}(x) = F_X(x)$
	- The random sample converges in distribution to the random variable if and only if for all random samples, the cumulative distribution function of the random sample at value x for a sample n is equal to the cumulative distribution function of the random variable as n approaches infinity
- Conditions
	- All the observations are mutually independent
	- All the observations are [[Distributions of Probability and Random Variables|identically distributed]]
		- $X_i \sim f(\theta), \forall i$
- If the samples are not iid, then we get a stochastic process (e.g., a Markov Process)
## Universal Boundary
- $P(|X - \mu| \le t\sigma) \ge \frac{1}{t^2}$
	- The probability that a centered random variable is at least t standard deviations away from the the mean is at least one over t-squared
	- This is true no matter the distribution of X
	- <mark style="background: #FFB86CA6;">For the normal distribution, this is an equality</mark>
## Law of Large Numbers
- $\underset{n \to \infty}{lim} P(|\bar{x}_n - \mu| < \epsilon) = 1, \forall \epsilon \in \mathbb R^+$
	- As the sample size increases, the probability that the sample average deviates from the expected value $\mu$ by more than $\epsilon$ becomes increasingly small
- This implies [[Probability Theory|almost-sure convergence]] in the Strong Law of Large Numbers
	- The Weak Law of Large Numbers only implies convergence in probability
- Central Limit Theorem
	- $\sqrt n (\bar X_n - \mu) \overset{d}{\to} \mathcal N(0, \sigma^2)$ as $n \to \infty$
	- The difference between sample means from a sequence of random variables and the true mean converges in distribution to a centered normal distribution as the sample sizes get sufficiently large
	 ![[Pasted image 20250125110432.png]]