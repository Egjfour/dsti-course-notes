|                        Course Name                        |               Topic               |    Professor    |     Date      |    Tags     |
| :-------------------------------------------------------: | :-------------------------------: | :-------------: | :-----------: | :---------: |
| **Foundations of Statistics and Machine Learning Part 2** | Multidimensional Random Variables | Christine Malot | 29 avril 2025 | #Statistics |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/blaise_pascal_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fblaise%5Fpascal%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FA24%20%2D%20Common%20Link%20DS%5FDE%5FDA%2D20250429%5F085138%2DMeeting%20Recording%201%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E724f0038%2D6f6d%2D4208%2D89a2%2D0a30759d78de)

# Summary
*Random vectors extend the concept of a random variable into mutli-dimensional space. The vectors are represented as column vectors where each element is a random variable. Random vectors have their own density functions which indicate information about joint probabilities. This information can be used to ascertain information about the density of the individual random variables as well (though the inverse is not true). A special case of random vectors, the Gaussian random vector, also exists which specifies that any linear combination of the Gaussian random variable elements must be a Gaussian random variable itself.*

# Key Takeaways
1. It is impossible to deduce the joint distribution of two random variables simply from the marginal distributions
2. The covariance between $X$ and $Y$ can be computed as $\mathbb E[XY] - \mathbb E[X] \cdot \mathbb E[Y]$
3. $\mathbb V[X + Y] = \mathbb V[X] + \mathbb V[Y] + 2cov(X,Y)$
4. $\mathbb V[X - Y] = \mathbb V[X] + \mathbb V[Y] - 2cov(X,Y)$
5. The variance-covariance matrix is a [[Matrices|square, symmetric]], [[Matrix Diagonalization|positive semi-definte]] matrix
6. The summation of non-independent Gaussian random variables is not always a Gaussian random variable

# Definitions
- [[Conditional Probability and Independence|Independence]] (${\perp \!\!\! \perp}$): The joint probability of two events is equal to the product of their marginal probabilities (i.e., knowing the outcome of one event gives no information about another)
	- Discrete Case: $X {\perp \!\!\! \perp} Y \text{ iff } \forall i \in X(\Omega), \forall k \in Y(\Omega), P(X = i) \cdot P(Y = k) = P(X = i, Y = k)$
	- Continuous Case: $X {\perp \!\!\! \perp} Y \text{ iff } f_{X,Y}(x, y) = f_X(x) \cdot f_Y(y)$
- Total Probability: The probability of an event in one variable across all joint possibilities of another random variable
	- Discrete Case: $\forall i \in X(\Omega), P(X=i) = \underset{k \in Y(\Omega)}{\sum}P(X=i,Y=k)$
- Deterministic: Values which are fixed and not random (i.e., regression coefficients)
- Gaussian Random Vector: A random vector in which all possible linear combinations of the components are also [[Random Variables|Gaussian random variables]]

# Additional Resources
- [Covariance Matrix](https://www.youtube.com/watch?v=152tSYtiQbw)
- [Gaussian Random Vectors Article](https://medium.com/@xiaoshi_4553/gaussian-random-vectors-a-detailed-analysis-9ee47f301e1d)

# Notes
## 2-Dimensional Discrete Random Vectors
- Definition
	- Let $X$ and $Y$ be two discrete random variables. Consider the object $(X, Y)$
	- This is a [[Vectors|row vector]] in dimension 2 but a column vector in higher dimensions
- We precise this vector by its distribution
	- Cartesian Product: $X(\Omega) \times Y(\Omega) = \{(x,y) \text{ for } x \in X(\Omega) \text{ and } y \in Y(\Omega)\}$
	- Probability is joint: $P_{ik}(X=i,Y=k)$
- If we know the joint distribution of $(X, Y)$, we can deduce the marginal distribution of $X$ and of $Y$ using total probabilities
	- The reverse is not true, however, since $X$ and $Y$ are not necessarily independent
## 2-Dimensional Continuous Random Vectors
- Unlike the discrete case, we cannot look at precise points since <mark style="background: #FFB86CA6;">the probability of a continuous random variable taking on a specific value is 0</mark>
- Same definition as the discrete case, but uses continuous random variables
- Distribution is a density function defined on $\mathbb R^2$
	- $f: \mathbb R^2 \to \mathbb R \text{ s.t. } \forall(x,y) \in \mathbb R^2 f(x,y) \gt 0 \text{ and } \iint_{\mathbb R^2}f(x, y)dxdy = 1$
	- Same conditions as the density for a continuous random variable: positive function and area under the curve/surface = 1
		- In the multi-dimensional case, we use double integrals to describe the distribution function
- Just like in the discrete case, the joint density function can be used to derive the marginal density functions.
### Example - Deriving Marginal Densities from Joint Density Function
- Let $f_{X,Y} = \begin{cases}c \text{ if }0 \le x \le y \le 2\\ 0 \text{ otherwise }\end{cases}$
	- Support is a triangle with $x = [0,2]; y=[0,2]$
	- First derive the value of $c$
	- Then determine the marginal densities $f_X$ and $f_Y$
- Derive $c$
	- Recognize that $f_{X,Y}$ is a triangle, so the area is $\frac{2\cdot 2}{2} = 2 = c$
	- Or integrate:
		- $\iint_{\mathbb R^2}f(x,y)dxdy = \iint_Dc\hspace{1mm}dxdy = c\cdot\iint_Ddxdy$
		- $\iint_Ddxdy = \int_{x=0}^2\int{y=0}^{2-x}dydx = \int_0^2[y]_0^{2-x}dx$
		- $=\int_0^2(2-x)dx=[2x - \frac{x^2}{2}]_0^2 = 2\cdot2 - \frac{2^2}{2} = 2 = c$
- Determine $f_X$
	- $f_X(t) = \int_{y \in \mathbb R}f(t,y)dy = \int_0^{2-t}cdy = c[y]_0^{2-t} = 4-2t$
		- Remember: $y = 2-x$
	- If $t \notin [0,2], f_X(t) = 0$
- Determine $f_Y$
	- $f_Y(t) = \int_{x\in \mathbb R}f(x,t)dx = \int_0^{2-t}cdx=c[x]_0^{2-t} = 4-2t$
	- If $t \notin [0,2], f_Y(t) = 0$
## Expectation and Variance for Random Vectors
- Calculations are the same for the discrete and continuous cases
- Expectation
	- The expectation of a random vector is <mark style="background: #FFB86CA6;">simply a vector of the expectation of each random variable</mark> contained within
	- $\mathbb E[(X, Y)] = (\mathbb E[X], \mathbb E[Y])$ where both expectations exist
- Variance
	- The variance of a random vector produces the variance-covariance matrix
		- Variance of each random variable along the diagonal and the covariance of each pair of random variables on the non-diagonal elements
		- Because covariance is symmetric, the variance-covariance matrix is also symmetric
	- Example: The variance of random vector $(X, Y)$ is $\begin{pmatrix}\mathbb V[X], cov(X, Y)\\ cov(Y,X), \mathbb V[Y]\end{pmatrix}$
	- Covariance Properties
		- $cov(X,X) = \mathbb V[X]$
		- $cov(X,Y) = cov(Y,X)$ - symmetry
		- $cov(aX+bZ, Y) = a\cdot cov(X,Y) + b\cdot cov(Z, Y)$
		- Independent random variables have a covariance of 0
			- However, <mark style="background: #FFB86CA6;">covariance of 0, does not imply independence</mark>. It simply implies no linear dependency. There can still be a non-linear dependency
	- Correlation is normalized covariance between 0 and 1
		- $corr(X,Y) = \frac{cov(X,Y)}{\sqrt{\mathbb V[X] \cdot \mathbb V[Y]}}$
## Generalization to Higher Dimensions
- Always expressed as a column vector when dimension ($p$) > 3
- Definitions for expectation and variance as a vector and matrix respectively remain the same
- Properties:
	- Let $M$ be a deterministic matrix and $X$ a random vector
	- $\mathbb E[MX] = M\mathbb E[X]$
		- The expectation retains its linearity property multiplying by a constant matrix
	- $\mathbb V[MX] = M\mathbb V[X] M^T$
- A matrix of random variables is a random matrix
	- The variance-covariance matrix is a random matrix
## Gaussian Random Vectors
- Definition
	- Let $X = \begin{pmatrix}X_1\\ \vdots\\X_d\end{pmatrix}$ a random vector
	- $X$ is a Gaussian random vector if $\forall (\lambda_1, \dots, \lambda_d) \in \mathbb R^d, \underset{k=1}{\overset{d}{\sum}}\lambda_kX_k$ is a Gaussian random variable (i.e., all possible [[Vectors|linear combinations]] of the random vector produce a Gaussian random variable)
### Example - Gaussian Random Vector
- Setup
	- Let $X \sim \mathcal N(0,1)$ and $\epsilon$ a rademaker (symmetric) random variable such that $P(\epsilon = -1) = P(\epsilon = 1) = \frac{1}{2}$
	- Assume $X {\perp \!\!\! \perp} \epsilon$ and introduce $y = \epsilon X$
- Prove that $Y$ is a Gaussian Random Variable
	- Need to determine $f_Y$
	- $f_Y(t) = P(Y \le t) = P(\epsilon X \le t)$
	- Since $\epsilon$ is discrete: $P(\epsilon X \le t) = P(X \ge -t, \epsilon = -1) + P(X \le t, \epsilon = 1)$
	- Since $X {\perp \!\!\! \perp} \epsilon$, we can multiply the marginal probabilities to get the joint probability
		- $P(X \ge -t, \epsilon = -1) = P(X \ge -t) \cdot P(\epsilon = -1)$
		- $P(X \le t, \epsilon = 1) = P(X \le t) \cdot P(\epsilon = 1)$
	- Because the Gaussian is centered
		- $\frac{1}{2}(P(X\le t) + P(X \ge -t))=\frac{1}{2}(P(X\le t) + P(X \le t)) = P(X \le t)$
	- So, we have $\forall t \in \mathbb R f_Y(t) = f_X(t)$
		- This means $X$ and $Y$ come from the same distribution
		- Since $X \sim \mathcal N(0, 1)$, so is $Y$. Thus, $Y$ is a Gaussian random variable
- Compute $cov(X,Y)$
	- $cov(X, Y) = \mathbb E[XY] - \mathbb E[X] \cdot \mathbb E[Y]$
		- $\mathbb E[X] \cdot \mathbb E[Y] = 0$ because they are standard Gaussians
		- $\mathbb E[XY] = \mathbb E[X \cdot \epsilon X]=\mathbb E[X^2 \epsilon]$
		- Since $X {\perp \!\!\! \perp} \epsilon$, $\mathbb E[X^2 \epsilon] = \mathbb E[X^2] \cdot \mathbb E[\epsilon]$
		- Since $\mathbb E[\epsilon] = \frac{1}{2} \cdot -1 + \frac{1}{2} \cdot 1 = 0$, $\mathbb E[XY] =0$
	- Thus, $cov(X,Y) = 0 - 0 = 0$
- Is $X {\perp \!\!\! \perp} Y$?
	- Assume that $X {\perp \!\!\! \perp} Y$
	- This also means $X {\perp \!\!\! \perp} \epsilon X$
		- and thus $X^2 {\perp \!\!\! \perp} (\epsilon X)^2$
		- but $(\epsilon X)^2 = \epsilon^2 \cdot X^2 = X^2$
		- Which would imply $X^2 {\perp \!\!\! \perp} X^2$ which is a contradiction
- Consider $Z = (X, Y)$. Prove that $Z$ is not a Gaussian random vector
	- Take the combination $X + Y$
	- Restate as $X + \epsilon X = X(1 + \epsilon)$
	- Since $\epsilon$ is discrete, we can calculate $P(X + Y = 0) = P(\epsilon = -1) = \frac{1}{2}$
	- Because we have a non-zero probability for a specific outcome, the random variable $X + Y$ is neither Gaussian nor continuous
	- Further, because there is a linear combination of $Z$ which does not produce a Gaussian random variable, $Z$ is not a Gaussian random vector