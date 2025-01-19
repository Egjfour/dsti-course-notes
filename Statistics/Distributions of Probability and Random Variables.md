|   Course Name    | Topic | Professor |        Date        |    Tags     |
| :--------------: | :---: | :-------: | :----------------: | :---------: |
| **Name in Bold** | Topic | Professor | 15-16 janvier 2025 | #Statistics |

[Class Video Link](URL)

# Summary
*A 3-4 sentence description of what was learned in italics*

# Key Takeaways
1. Probability distributions are able to be plotted since they are in the real number space $\mathbb R$
2. The standard normal distribution has a mean of 0 (centered) and a standard deviation of 1 (scaled)
3. Probability Mass Functions are for discrete random variables and Probability Distribution Functions are for continuous random variables and are represented as $f_X$

# Definitions
- Probability Distribution of a [[Random Variables|Random Variable]]: The proportion of all outcomes for which we get a specific outcome
- Identically Distributed: The probabilities among observations come from the same distribution
	- If I flip a coin 100 times, the 101st flip is still a Bernoulli distribution with $p = 0.5$
	- <mark style="background: #FFB86CA6;">Does NOT mean that each outcome is equally likely</mark>
- Marginal Distribution: The probability of one random variable within the joint distribution
	- Sum of all probabilities for all values $Y$ given a fixed $X=x$
	- [[Conditional Probability and Independence|Marginal probability]] of a random variable

# Additional Resources
- [Independently and Identically Distributed](https://towardsdatascience.com/independent-and-identically-distributed-ce250ad1bfa8)
- [Geometric Distribution](https://calcworkshop.com/discrete-probability-distribution/geometric-distribution/)
# Notes
## Link to Probability Theory
- If x is a value in $\mathbb R$
	- $P_X(x) = P(X(\omega) = x) = P(\{\omega: X(\omega) = x\}) = P(X^{-1}(x)) = P(X=x)$
		- The probability that the random variable X assumes the value x equals the probability that the application of the random variable on the outcome $\omega$ is x which equals...
- If B is a $\sigma$-[[Probability Theory|algebra]] of $\mathbb R$
	- $P_X(B) = P(X(\omega) \in B) = P(\{\omega: X(\omega) \in B\}) = P(X^{-1}(B))$
	- The probability of B being in X equals the probability that the application of the random variable X on $\omega$ is in the sigma algebra which equals...
- <mark style="background: #FFB86CA6;">A probability space is defined as</mark> $(X(\Omega), \mathcal B, P_X)$
	- An application of a [[Random Variables|random variable]] on a [[Probability Theory|sample space]]
	- A support of a random variable
	- And a probability distribution of the random variable
## Distribution Functions of Random Variables
- Cumulative Distribution Function (CDF)
	- $F_X(t) = P(X \le t)$ with $t \in \mathbb R$
	- $F_X$ is defined for ALL values t since X is a random variable defined on $\mathbb R$
		- <mark style="background: #FFB86CA6;">This is true even for discrete sample spaces since random variables are continuous</mark>
	- If the random variable is continuous $F_X$ is continuous. If the r.v. is discrete, then $F_X$ will be a step function
	- X and Y are identically distributed (come from the same probability distribution: $X \thicksim Y$) iff $F_x = F_y$
	- Always defined for any random variable
	- The inverse ($F^{-1}_X$) is commonly known as the quantile function
- Probability Mass Function (PMF)
	- For discrete variables only
	- $f_X(x) = P(X=x), \forall x \in \mathbb R$
	- The probability mass function of a discrete random variable at value x equals the probability of the random variable assuming that value
- Probability Density Function (PDF)
	- For continuous variables only
	- $F_X(x) = \int_{-\infty}^\infty f_X(x)dx$
	- The cumulative distribution is the primitive of the probability density function
		- $F'_X = f_x$
	- <mark style="background: #FFB86CA6;">To calculate probability of specific values, it is generally easier to use the CDF</mark>
## Common Distributions
- Uniform (Discrete): Rolling a single die
	- Equal probability
- Bernoulli (Discrete): Tossing a coin
	- [[Random Variables|Support]] is binary
- Binomial (Discrete): Tossing a coin multiple times
	- Repeated trials of a binary event
- Poisson (Discrete): Counting the number of people in a store
- Normal (Continuous): Grades
	- Standard normal has an [[Random Variables|expected value]] of 0 and a variance/standard deviation of 1
		- mean, median, and mode are all the same
		- Parameterized with the mean and standard deviation: $\mathcal N(\mu, \sigma)$
- Geometric (Discrete): Tossing a coin until heads
	- Repeated trials of a binary event until a desired outcome is achieved
	- Parameterized with $p$ as the prob. of success and $k$ as # of trials
		- PMF: $P(X = k) = p(1-p)^{k-1}$ 
		- CDF: $P(X > k) = (1-p)^k$
- Logistic (continuous): Logistic regression tasks and neural networks
	- $F_X(x) = \frac{1}{1 + exp(- \frac{x - \mu}{\sigma})}$
	- Calculating probability on an interval
		- With CDF: $F_X(b) - F_X(a)$ based on the [[Continuity & Derivability|mean value theorem]]
		- With PDF: $\int_a^bf_X(x)dx$ as an integral
			- $f_X(x) = \frac{d}{dx}F_X(x) = \frac{e^{-x}}{(1+e^{-x})^2}$
## [[Random Variables|Multidimensional Random Variables]]
- Joint Distribution
	- Probability Mass (Discrete $X, Y$)
		- $f_{X, Y}(x, y) = P(X=x, Y=y)$
		- Probability of both events occurring simultaneously
	- Probability Distribution (Continuous $X, Y$)
		- $P((X, Y) \in A) = \int_A f(x,y)dxdy$
- Marginal Distribution
	- Discrete: $f_X(x) = \sum_{y \in \mathbb R}f_{X, Y}(x, y) = P(X=x, Y \in \mathbb R)$
	- Continuous: $\int_{- \infty}^\infty f(x, y)dy$
- Conditional Distribution
	- Same definition as [[Conditional Probability and Independence|conditional probability]]
	- $f(y|x)=\frac{f(x,y)}{f_X(x)}, \forall x: f_X > 0$
	- <mark style="background: #FFB86CA6;">This is a valid pmf/pdf</mark>
	- Independence is determined by the same condition as [[Conditional Probability and Independence|independence for probability]]
		- $f(y|x) = \frac{f(x,y)}{f_X(x)}=\frac{f_X(x)f_Y(y)}{f_X(x)}=f_Y(y)$