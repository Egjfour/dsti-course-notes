|                             Course Name                             |                       Topic                        |     Professor      |        Date        |    Tags     |
| :-----------------------------------------------------------------: | :------------------------------------------------: | :----------------: | :----------------: | :---------: |
|    **Foundations of Statistical Analysis and Maching Learning**     |             Distributions of Variables             | Christophe Bécavin | 15-16 janvier 2025 | #Statistics |
| **Foundations of Statistical Analysis and Maching Learning Part 2** | Common Distributions and Graphical Representations |  Christine Malot   |   28 avril 2025    |             |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/johnny_najjar_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fjohnny%5Fnajjar%5Fdsti%5Finstitute%2FDocuments%2FRecordings%281%29%2FA24%20%2D%20Common%20Link%20%2D%20DS%2DDE%2DDA%2D20250116%5F095107%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E00f8464c%2D5165%2D473e%2Dba3a%2D6418387d76cf)

# Summary
*Random variables are the mapping between events that can happen in the physical world and the real number space which allows for effective measurement. Like probability distributions, there are also common distributions of random variables which have known expectation and variance calculations.*

# Key Takeaways
1. Random variables are the link between the possible outcomes ($\Omega$) and the events
2. Functions of a random variable are also random variables themselves
3. A function continuous random variable is continuous (discrete is discrete)
4. Moments of a random variable can always be calculated (even for discrete random variables)
5. A necessary (not sufficient) condition for $X, Y$ to be independent is to have no instances with a probability of 0 in the joint domain
6. When the degrees of freedom are $+ \infty$ for the $\mathcal T$-distribution, $\mathcal T(d) = \mathcal N(0,1)$
7. Two random variables with the same expectation and variance are not necessarily from the same distribution. The Fisher random variable allows us to confirm if they are or not
8. However, two random variables with the same expectation, variance, and distribution may not always be equal (e.g., $X \sim \mathcal U(-1, 1)$ and $Y = -X$)

# Definitions
- Random Variable: A function that maps from a [[Probability Theory|sample space]] $\Omega$ to a numeric value $\mathbb R$
- Support $(\mathcal B)$: The smallest closed set $R_X \in \mathcal B$ such that the probability is one
	- The height of humans cannot be negative, so even though the random variable can exist in $\mathbb R$, the support would be $\mathbb R^+$.
- [[Random Vectors|Random Vector]]: $\Omega \rightarrow \mathbb R^n$, mapping from a space to a real vector
	- Multidimensional Random Variable

# Additional Resources
- [Markov and Tchebychev Inequalities](https://www.probabilitycourse.com/chapter6/6_2_2_markov_chebyshev_inequalities.php)
- [Chi-Square Distribution Video](https://www.khanacademy.org/math/statistics-probability/inference-categorical-data-chi-square-tests/chi-square-goodness-of-fit-tests/v/chi-square-distribution-introduction)
- [Student's T Distribution Video](https://www.youtube.com/watch?v=0wjK7Ya7lOA)
- [F-distribution](https://www.statlect.com/probability-distributions/F-distribution)
- [Fisher Information](https://www.youtube.com/watch?v=pneluWj-U-o)
- [Linear Combinations of Random Variables](https://www.youtube.com/watch?v=93VgYYOWNio)
- [Calculating Probabilities of Linear Combinations of Random Variables](https://www.youtube.com/watch?v=0Rcc0htSgPU)
- [Ratio of Exponentials Example](https://swnydick.github.io/assets/reports/Ratio_of_Exponentials.pdf)

# Notes
## Random Variables as Functions
- Random variables must be measurable
	- $\forall B \in \mathcal B, X^{-1}(B)\in \mathcal A$
		- For any outcome in the support set, the inverse of the event must be within the [[Probability Theory|sigma algebra]]
## Moments of a Random Variable
- Similar definitions to [[Descriptive Statistics|descriptive statistics moments]], but random variables are based on [[Distributions of Probability and Random Variables|probability distributions]]
	- Raw moments are on raw data, centered moments remove the expected value, and scaled centered moments both remove the expected value and the variance
- Expected Value $E[X]$ (first moment)
	- If $X$ discrete
		- $E[X] = \sum_{x_i} x_i f_X(x_i) = \sum_{x_i} x_i P(X=x_i)$
	- If $X$ is continuous
		- $E[X] = \int_{- \infty}^\infty xf_X(x)dx$
	- Properties (same as the [[Descriptive Statistics|mean]])
		- $E[aX + b] = aE[X] + b$
			- Can also separate sums of functions of random variables
		- $\forall x \rightarrow g(x) \ge 0, E[g(X)] \ge 0$
		- $\forall x \rightarrow g(x) \ge t(x), E[g(X)] \ge E[t(X)]$: If the output of a function of a random variable is always greater than or equal to the output of another function of the same random variable, the expected value of the first function will be greater than or equal to the other function's expected value
		- $\forall x \rightarrow a \le g(x) \le b, a \le E[g(X)] \le b$: If all observations of a random variable are between two values, the expected value is also between those values
- Variance $\mathrm {Var}(X)$ (second moment)
	- $E[(X - E[X])^2]$: Expected value of the squared difference
	- <mark style="background: #FFB86CA6;">Same property exists</mark> as [[Descriptive Statistics|variance]]: $\mathrm{Var}(X) = E[X^2] - E[X]^2$
	- $\mathrm{Var}(aX + b) = a^2\mathrm{Var}(X)$
		- <mark style="background: #FFB86CA6;">Adding a constant DOES NOT change variance</mark>
- Skew (third moment) and kurtosis (fourth moment)
- Generalized moments of degree $k$
	- Raw moments
		- Discrete: $\mu_k = \sum_ix_i^kf(x_i)$
		- Continuous: $\mu_k = \int_{- \infty}^\infty x^kf(x_i)$
	- Standardized Moments
		- $\tilde{\mu_k}= \dfrac{\mu_k}{\sigma_k}$
			- $\mu_k = E[(X - \mu)^k]$
			- $\sigma_k = \mu_2^{k/2}$
## Important Inequalities of Random Variables
- Markov's Inequality
	- If X is positive, then $\forall r > 0, P(X\ge r) \le \dfrac{E[X]}{r}$ 
		- The probability that a random variable is greater than a chosen value is at most the ratio of the expected value of that random variable and the chosen value
- Tchebychev Inequality
	- Let X be a random variable and g(x) be a non-negative function of that random variable
	- $\forall r > 0, P(g(X) \ge r) \le \dfrac{E[g(x)]}{r}$
	- Same as Markov's, but this applies to non-negative functions of the random variable
## Classical Random Variables and Their Properties
- Uniform ($X \sim \mathcal U(a, b)$)
	- Density Function: $f_X(t) = \begin{cases}\dfrac{1}{b - a} \text{ if } t \in [a,b]\\ 0 \text{ otherwise }\end{cases}$
	- $\mathbb E[X] = \dfrac{a+b}{2}$ and $\mathbb V[X] = (b-a)^2/12$
	- Distribution Function: $F_X(t) = \begin{cases}0 \text{ if } t \lt a\\\dfrac{t-a}{b-a} \text{ if } t\in [a,b]\\1 \text{ if }t \gt b\end{cases}$
	- The distribution $X \sim \mathcal U(0,1)$ can be converted to any range
		- $Y = a + (b-a)X \implies Y \sim \mathcal U(a, b)$
	- R Function: `runif(n, min = 0, max = 1)`
- Exponential ($X \sim \epsilon(\lambda)$)
	- Density Function: $f_X(t) = \begin{cases}\lambda e^{-\lambda t} \text{ if } t \ge 0\\0 \text{ otherwise }\end{cases}$
	- $\mathbb E[X] = \dfrac{1}{\lambda}$ and $\mathbb V[X] = \dfrac{1}{\lambda^2}$
		- This is the French version. English version is $\lambda$ and $\lambda^2$
	- $F_X(t)=\begin{cases}1-e^{-\lambda t} \text{ if } t \ge 0\\0 \text{ otherwise }\end{cases}$
	- The distribution $X \sim \epsilon(1)$ can be converted to anything
		- $Y = \dfrac{1}{\lambda}X \implies Y \sim \epsilon(\lambda)$
	- R Function: `rexp(n, rate = 1)`
- [[Distributions of Probability and Random Variables|Gaussian]] ($X \sim \mathcal N(\mu, \sigma^2)$)
	- Due to the complexity of the density function, software like R or precalculated tables are used to estimate
	- $\mathbb E[X] = \mu$ and $\mathbb V[X] = \sigma^2$
	- R Function: `rnorm(n, mean = 0, sd = 1)`
		- Note that this uses standard deviation and not variance
	- We can transform any Gaussian-distributed variable to the standard Gaussian through normalization (centering and scaling)
		- $Y = \dfrac{X - \mu}{\sigma^2} \implies Y \sim \mathcal N(0,1)$
- Chi-Square ($X \sim \chi^2(d)$)
	- The chi-square random variable is a sum of squared gaussian random variables
		- Let $X_1, \dots, X_d$ [[Distributions of Probability and Random Variables|iid]] whose distribution is $\mathcal N(0,1)$, consider $C = \overset{d}{\underset{k=1}{\sum}}X^2_k$
		- $C$ is then a $\chi^2$ random variable with degrees of freedom $d$
	- $\mathbb E[X] = d$ and $\mathbb V[X] = d \mathbb V[X_1^2] = 2d$
	- Like Gaussian random variables, there is also a table for calculation based on the degrees of freedom
	- R Function: `rchisq(n, df, ncp = 0)`
- Student's $T$ Random Variable ($X \sim \mathcal T(d)$)
	- Ratio of a standard Gaussian and normalized $\chi^2$
		- Let $N \sim \mathcal N(0,1)$ and $C \sim \chi^2(d)$, $X = \dfrac{N}{\sqrt{\dfrac{C}{d}}}$
	- Has degrees of freedom $d$
	- $\mathbb E[X] = 0$ if $d \gt 1$ and $\mathbb V[X]  = \dfrac{d}{d - 2}$ if $d \gt 2$
	- This is a <mark style="background: #FFB86CA6;">symmetric distribution</mark>
		- $\forall t \in \mathbb R, f_X(t) = f_x(-t) \text{ and } P(X \le -t) = P(X \ge t)$
	- R Function: `rt(n, df, ncp)`
- Fisher Random Variables $X \sim \mathcal F(d, p)$
	- Ratio of two $\chi^2$ random variables normalized by their degrees of freedom
		- Let $N \sim \chi^2(d)$ and $D \sim \chi^2(p), X = \dfrac{\dfrac{N}{d}}{\dfrac{D}{p}}$
	- Has $d$ and $p$ degrees of freedom
		- $\dfrac{1}{F}$ has $p$ and $d$ degrees of freedom
	- Typically used for comparing datasets
		- Start by comparing variances, then means
		- Then, if above satisfied, turn to Fisher 
	- $\mathbb E[X] = \dfrac{p}{p-2}$ if $p \gt 2$ and $\mathbb V[X] = \dfrac{2p^2(d + p -2)}{d(p-2)^2(p-4)}$ if $p \gt 4$
## Graphical Representation
- Histogram
	- Representation of the density function
	- Divides the random variable into classes on the x-axis and uses the empirical density on the y-axis
	- Acts as a [[Point Estimators|non-parametric estimation]] of the true density function
	- To determine class length
		- Set the number of classes: $k \approx 1 + 3.22 \cdot log_{10}(n)$ with $n$ as number of observations
		- Define the class limits with a margin ($\epsilon$)
			- $a_0 = min(X) - \epsilon; a_k = max(X) + \epsilon; \forall i \in [1, k-1], a_i = a_0 + i\cdot range$
				- $range = \dfrac{a_k-a_0}{k}$
	- The histogram is generated using the [[Descriptive Statistics|continuous frequency table]]
	- In R, the `hist(x)` function creates a histogram
		- Be sure to set the argument `freq = FALSE` to have the empirical density on the y-axis instead of the count
		- We can also redefine the breaks, but by default, R uses the Sturges algorithm (formula above)
	- Example R plot: `hist(rnorm(10000), freq = FALSE, main="Histogram of Normal Distribution", xlab="x", ylab="Empirical Density")`
		 ![[Pasted image 20250503091247.png]]
- Cumulative Empirical Distribution Curve
	- Estimates the distribution function
	- Depends on the number of observations and classes
	- <mark style="background: #FFB86CA6;">Since it uses random variable observations, it is a random object</mark>
	- Calculates an ordered-sum of the empirical densities across classes
	- R Example: `plot(ecdf(rnorm(10000)), main="Empirical CDF of Normal Distribution", xlab="x", ylab="Empirical CDF")`
		 ![[Pasted image 20250503091647.png]]