|                             Course Name                             |           Topic           |     Professor      |        Date        |    Tags     |
| :-----------------------------------------------------------------: | :-----------------------: | :----------------: | :----------------: | :---------: |
| **Foundations of Statistical Analysis and Machine Learning Part 1** | Probability Distributions | Christophe Bécavin | 15-16 janvier 2025 | #Statistics |
| **Foundations of Statistical Analysis and Machine Learning Part 2** |     Random Variables      |  Christine Malot   |   28 avril 2025    |             |

[Class Video Link 1](https://dstisas-my.sharepoint.com/personal/johnny_najjar_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fjohnny%5Fnajjar%5Fdsti%5Finstitute%2FDocuments%2FRecordings%281%29%2FA24%20%2D%20Common%20Link%20%2D%20DS%2DDE%2DDA%2D20250116%5F095107%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E00f8464c%2D5165%2D473e%2Dba3a%2D6418387d76cf)
[Class Video Link 2](https://dstisas-my.sharepoint.com/personal/johnny_najjar_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fjohnny%5Fnajjar%5Fdsti%5Finstitute%2FDocuments%2FRecordings%281%29%2FA24%20%2D%20Common%20Link%20%2D%20DS%2DDE%2DDA%2D20250428%5F085826%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E2e01d2df%2Df23f%2D4d58%2D8e3d%2De9bd3cfbac91)

# Summary
*Distributions allow us to express the shape of the expectations around an event as a real number space. Every event has a cumulative distribution function which represents the likelihood that the random variable for the event is less than or equal to a given value. For specific values of probability given a point, we use the probability mass function for discrete variables and the probability density function for continuous variables. Many of the same concepts from [[Probability Theory|probability theory]] related to independence apply as well.*

# Key Takeaways
1. Probability distributions are able to be plotted since they are in the real number space $\mathbb R$
2. The standard normal distribution has a mean of 0 (centered) and a standard deviation of 1 (scaled)
3. Probability Mass Functions are for discrete random variables and Probability Density Functions are for continuous random variables and are represented as $f_X$
4. Probability density functions must be positive, $\forall x \in \mathbb R, \mathcal f(x) \ge 0$, and have an integral which sums to one, $\int_{\mathbb R} \mathcal f(x)dx = 1$

# Definitions
- Probability Distribution of a [[Random Variables|Random Variable]]: The proportion of all outcomes for which we get a specific outcome
- Identically Distributed: The probabilities among observations come from the same distribution
	- If I flip a coin 100 times, the 101st flip is still a Bernoulli distribution with $p = 0.5$
	- <mark style="background: #FFB86CA6;">Does NOT mean that each outcome is equally likely</mark>
- Marginal Distribution: The probability of one random variable within the joint distribution
	- Sum of all probabilities for all values $Y$ given a fixed $X=x$
	- [[Conditional Probability and Independence|Marginal probability]] of a random variable
- Density Function: The distribution of a continuous random variable

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
- Cumulative Distribution/Density Function (CDF)
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
	- It is essential that $\mathcal f_X(x)$ is positive, otherwise, we allow for negative probabilities which is impossible
### Example of Probability Density Function
- Such functions need not be common distributions. They simply must meet the positivity and integral conditions
- Let $f: \mathbb R \to \mathbb R$ with $f(x) = \begin{cases}cx^2 \text{ if } x \in [1,2]\\ 0 \text{ otherwise }\end{cases}$
- Question: What should $c$ be such that $f(x)$ is a density function
	- First prove positivity
		- Since $x^2$ is positive on $\mathbb R$, $cx^2$ is positive where $c \ge 0$
	- Then, solve for the integral $\int_{\mathbb R}cx^2dx = 1$
		- Pull the constant out: $c \cdot \int_{\mathbb R}x^2dx$
		- Separate the integral to focus on the support only: $c \cdot \int_{1}^{2}x^2dx$
		- Apply the [[Integration|power rule]]: $c \cdot [\dfrac{1}{3}x^3]_1^2 = c \cdot (\dfrac{8}{3} - \dfrac{1}{3}) = c \cdot \dfrac{7}{3}$
		- Solve for $c$: $c = \dfrac{3}{7}$ which satisfies the positivity condition as well
- Question: If $X$ is a [[Random Variables|random variable]] w/ density function $f$, compute $P(X \in [0, 1.2]\cup [1.8,2])$
	- We want to calculate the cumulative density of the regions, so we integrate the PDF
	- Since we have a union of disjoint events, we can simply sum the probabilities/integrals
	- $\int_0^{1.2} \dfrac{7}{3}x^2dx + \int_{1.8}^2 \dfrac{7}{3}x^2dx$
	- We can further separate the first integral to isolate the support ($[1,2]$)
		- $\int_1^{1.2} \dfrac{7}{3}x^2dx + \int_{1.8}^2 \dfrac{7}{3}x^2dx$
	- Now evaluate
		- $\dfrac{3}{7}([\dfrac{x^3}{3}]_1^{1.2} + [\dfrac{x^3}{3}]_{1.8}^{2})$
	- Using R to solve: `"The probability of [0, 1.2] U [1.8, 2] is 0.414"`
		```r
		solve_primitive <- function(x){
		    val <- (x^3)/3
		    return(val)
		}
		expression <- (3/7) * ((solve_primitive(1.2) - solve_primitive(1)) +
						(solve_primitive(2) - solve_primitive(1.8)))
		
		print(paste("The probability of [0, 1.2] U [1.8, 2] is",
					round(expression, 3)))
		```
## Common Probability Distributions
- Uniform (Discrete): Rolling a single die
	- Equal probability
- Bernoulli (Discrete): Tossing a coin
	- [[Random Variables|Support]] is binary
	- $\mathbb E[X] = p$
	- $\mathbb V[X] = p(1-p)$
- Binomial (Discrete): Tossing a coin multiple times
	- Repeated trials of a binary event
	- Expected value = number of trials * probability of success
		- $\mathbb E[X] = np$
	- $\mathbb V[X] = Np(1-p)$
- Poisson (Discrete): Counting the number of people in a store
- Normal (Continuous): Grades
	- Standard normal has an [[Random Variables|expected value]] of 0 and a variance/standard deviation of 1
		- mean, median, and mode are all the same
		- Parameterized with the mean and standard deviation (English): $\mathcal N(\mu, \sigma)$
			- Mean and variance (France): $\mathcal N(\mu, \sigma^2)$
- Geometric (Discrete): Tossing a coin until heads
	- Repeated trials of a binary event until a desired outcome is achieved
	- Parameterized with $p$ as the prob. of success and $k$ as # of trials
		- PMF: $P(X = k) = p(1-p)^{k-1}$ 
		- CDF: $P(X > k) = (1-p)^k$
- Logistic (continuous): Logistic regression tasks and neural networks
	- $F_X(x) = \dfrac{1}{1 + exp(- \dfrac{x - \mu}{\sigma})}$
	- Calculating probability on an interval
		- With CDF: $F_X(b) - F_X(a)$ based on the [[Continuity & Derivability|mean value theorem]]
		- With PDF: $\int_a^bf_X(x)dx$ as an integral
			- $f_X(x) = \dfrac{d}{dx}F_X(x) = \dfrac{e^{-x}}{(1+e^{-x})^2}$
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
	- $f(y|x)=\dfrac{f(x,y)}{f_X(x)}, \forall x: f_X > 0$
	- <mark style="background: #FFB86CA6;">This is a valid pmf/pdf</mark>
	- Independence is determined by the same condition as [[Conditional Probability and Independence|independence for probability]]
		- $f(y|x) = \dfrac{f(x,y)}{f_X(x)}=\dfrac{f_X(x)f_Y(y)}{f_X(x)}=f_Y(y)$