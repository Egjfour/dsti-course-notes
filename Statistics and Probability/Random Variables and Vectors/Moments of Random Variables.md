|                             Course Name                             |      Topic       |    Professor    |     Date      |    Tags     |
| :-----------------------------------------------------------------: | :--------------: | :-------------: | :-----------: | :---------: |
| **Foundations of Statistical Analysis and Machine Learning Part 2** | Random Variables | Christine Malot | 28 avril 2025 | #Statistics |

[Class Video Link](URL)

# Summary
*A 3-4 sentence description of what was learned in italics*

# Key Takeaways
1. The [[Descriptive Statistics|statistical mean/variance]] $\ne$ the expectation/variance
2. The variance is ALWAYS a positive value
3. Moments of random variables are not themselves random variables, they are constants
4. Estimating the density function of a transformation involves finding the distribution function and taking the derivative of the distribution function
# Definitions
- Expectation ($\mathbb E[X]$): Let $x$ be a [[Random Variables|random variable]] with [[Distributions of Probability and Random Variables|density function]] $f$, if $\int_{\mathbb R} |x|f(x)dx \lt + \infty$, then $x$ is an integrable variable (denoted $x \in \mathscr L^1$), and in this case, $\mathbb E[X]$ exists and is given by $\mathbb E[X] = \int_{\mathbb R}xf(x)dx$ 
	- The expectation is the integral of the density function times the observations across the entire [[Random Variables|support]]
- Variance ($\mathbb V[X]$): Let $x$ be a random variable with density function $f$. If $\int_{\mathbb R^2}x^2f(x)dx \lt + \infty$, then $x$ is <mark style="background: #FFB86CA6;">square integrable</mark> (denoted $x \in \mathscr L^2$), and in this case, the variance of $x$ exists and is given by $\mathbb V[X] = \mathbb E[(X - \mathbb E[X])^2]$
- Moment: Let $x$ be a random variable and $k$ an integer $\ge 1$. The moment of order $k$ for $X$ is $\mathbb E[X^k]$ when this quantity exists
# Additional Resources
- [Fundamentals of Moments](https://www.statlect.com/fundamentals-of-probability/moments)

# Notes
## Properties of Expectation and Variance
- Expectation
	- Linearity: $\mathbb E[aX + bY] = a\mathbb E[X] + b\mathbb E[Y]$
	- Constant: $\mathbb E[a] = a$
- Variance
	- Constant: $\mathbb V[a] = 0$
	- Scalar Multiple: $\mathbb V[aX] = a^2\mathbb V[X]$
		- <mark style="background: #FFB86CA6;">MUST square the scalar</mark>
	- NOT LINEAR: $\mathbb V[X + Y] \ne \mathbb V[X] + \mathbb V[Y]$
- Practical formula for variance calculation
	- $\mathbb V[X] = \mathbb E[X^2] - (\mathbb E[X])^2$
		- Implies that $\mathbb E[X^2] \ge \mathbb (E[X])^2$
	- Same formula as with [[Descriptive Statistics|statistical variance]], but uses expectation instead of the mean
## Transfer Formula (Expectation of Transformation of R.V.)
- Let $X$ a random variable with density function $f$ and $h$ a [[Real Functions of a Real Variable|real function]] ($h: \mathbb R \to \mathbb R$)
	- consider $Y = h(X)$
- If $\mathbb E[Y]$ exists, then
	- $\mathbb E[Y] = \int_{\mathbb R} h(x) \cdot f(x)dx$
- $Y$ <mark style="background: #FFB86CA6;">may not necessarily have the same distribution</mark> as $X$, but we can use the distribution of $X$ to calculate $\mathbb E[Y]$
- Without this, we would have to solve for the distribution of $Y$ directly
	- To do this, we need to estimate the [[Distributions of Probability and Random Variables|distribution function]] of the transformed random variable
	- Then, calculate the derivative of the distribution function where it exists
### Transfer Formula Example and Comparison
- Let $X$ a random variable with dens. fxn. $f_X(x) = \begin{cases}cx^2 \text{ if } x \in [-2,2]\\0 \text{ otherwise }\end{cases}$
	- Solve for $c$
	- Consider $Y = x^2$, compute $\mathbb E[Y]$
- Solve for $c$
	- Due to the positivity constraint, $c \ge 0$
	- $\int_{\mathbb R}cx^2dx = c\int_{-2}^2x^2dx$
	- Thanks to symmetry, $c\int_{-2}^2x^2dx=2c\int_{0}^2x^2dx$
	- Solving, we get $\frac{2c}{3}\cdot(2^3 - 0^3) = \frac{16}{3}$
	- Setting the integral equal to one gives, $c = \frac{3}{16}$
- Solve $\mathbb E[Y]$ with the transfer formula
	- Formula states $\mathbb E[Y] = \int_{\mathbb R}y\cdot f(x)dx = \int_{\mathbb R}x^2\cdot \frac{3}{16}x^2dx$
	- Focusing in on the support we get $\frac{3}{16}\int_{-2}^2 x^4 dx = \frac{3}{8}\int_{0}^2 x^4dx$
	- The primitive of which is $\frac{3}{40}[x^5]_0^2$
	- Evaluating gives $\frac{3}{40} \cdot (2^5 - 0^5) = \frac{3}{40} * 32 = \frac{12}{5}$
- Solve $\mathbb E[Y]$ by finding the density function for $Y$
	- First, we need to find the distribution function: $F_Y(t) = P(Y \le t) = P(x^2 \le t)$
		- First case: $t \lt 0$
			- $\{x^2 \le t \} = \emptyset \implies P(\emptyset)=0$
		- Second Case: $t \ge 0$
			- $F_Y(t) = P(x^2 \le t) = P(-\sqrt t \le x \sqrt t) = P(x \le \sqrt t) - P(x \le -\sqrt t)$
			- $F_X(\sqrt t) - F_X(-\sqrt t)$
			- Can immediately compute $f_Y$ since $f_Y(t) = F_Y'(t) = \frac{1}{2\sqrt t} \cdot f_X(\sqrt t)$
				- But this is difficult, so instead we calculate $F_X(t)$
			- $F_X(t) = P(X \le t) = \begin{cases}0 \text{ if } t \lt -2\\ \int_{-2}^tf(x)dx \text{ if } t \in [-2, 2]\\ 1 \text{ if } t \gt 2 \end{cases}$