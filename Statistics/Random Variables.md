|                         Course Name                          |           Topic            |     Professor      |        Date        |    Tags     |
| :----------------------------------------------------------: | :------------------------: | :----------------: | :----------------: | :---------: |
| **Foundations of Statistical Analysis and Maching Learning** | Distributions of Variables | Christophe Bécavin | 15-16 janvier 2025 | #Statistics |

[Class Video Link](URL)

# Summary
*A 3-4 sentence description of what was learned in italics*

# Key Takeaways
1. Random variables are the link between the possible outcomes ($\Omega$) and the events
2. Functions of a random variable are also random variables themselves
3. A function continuous random variable is continuous (discrete is discrete)
4. Moments of a random variable can always be calculated (even for discrete random variables)
5. The moments of a random vector create a vector of moments: $E[X, Y] = \begin{pmatrix}E[X]\\E[Y]\end{pmatrix}$
6. The random variables of a random vector are independent if and only if their [[Distributions of Probability and Random Variables|joint distribution]] is equal to the product of their marginal distributions
7. A necessary (not sufficient) condition for $X, Y$ to be independent is to have no instances with a probability of 0 in the joint domain

# Definitions
- Random Variable: A function that maps from a [[Probability Theory|sample space]] $\Omega$ to a numeric value $\mathbb R$
- Support $(\mathcal B)$: The smallest closed set $R_X \in \mathcal B$ such that the probability is one
	- The height of humans cannot be negative, so even though the random variable can exist in $\mathbb R$, the support would be $\mathbb R^+$.
- Random Vector: $\Omega \rightarrow \mathbb R^n$, mapping from a space to a real vector
	- Multidimensional Random Variable

# Additional Resources
- [Markov and Tchebychev Inequalities](https://www.probabilitycourse.com/chapter6/6_2_2_markov_chebyshev_inequalities.php)

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
		- $\tilde{\mu_k}= \frac{\mu_k}{\sigma_k}$
			- $\mu_k = E[(X - \mu)^k]$
			- $\sigma_k = \mu_2^{k/2}$

## Inequalities of Random Variables
- Markov's Inequality
	- If X is positive, then $\forall r > 0, P(X\ge r) \le \frac{E[X]}{r}$ 
		- The probability that a random variable is greater than a chosen value is at most the ratio of the expected value of that random variable and the chosen value
- Tchebychev Inequality
	- Let X be a random variable and g(x) be a non-negative function of that random variable
	- $\forall r > 0, P(g(X) \ge r) \le \frac{E[g(x)]}{r}$
	- Same as Markov's, but this applies to non-negative functions of the random variable