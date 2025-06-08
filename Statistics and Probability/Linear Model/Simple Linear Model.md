|                        Course Name                        |   Topic    |    Professor    |       Date       |    Tags     |
| :-------------------------------------------------------: | :--------: | :-------------: | :--------------: | :---------: |
| **Foundations of Statistics and Machine Learning Part 2** | Regression | Christine Malot | 07 & 09 mai 2025 | #Statistics |

[Class Video Link](URL)

# Summary
*A 3-4 sentence description of what was learned in italics*

# Key Takeaways
1. It is essential that the error is Gaussian distributed
2. Mathematical notation: $\forall i \in [1,n], y_i = a + bX_i + \epsilon_i$
3. The individual $y_i$ are not identically distributed because $\mathbb E[Y_i] = a + bX_i$
4. With assumption H4 (the errors form a [[Random Vectors|Gaussian Random Vector]]), we can assume that our parameter vector $\begin{pmatrix}\hat a_n \\ \hat b_n \end{pmatrix}$ is a Gaussian random vector
5. $\hat Y$ is the orthogonal projection of $Y$ on $X$ and the error $\hat \epsilon \perp X$ with $X$ a vectorial subspace of dimension $n-2$
6. A confidence interval for forecasted values is $[\hat y_{new} \pm \hat\sigma_n \sqrt{1 + \frac{1}{n}\frac{(X_{new} - \bar X_n)^2}{\underset{k}{\sum}(X_k - \bar X_n)^2}}\cdot t_{1-\alpha/2;\hspace{1mm} n-2}]$
7. The further we are from $\bar X_n$, the less confident we are in the prediction. Prediction interval is a pair of hyperbolic curves which increase in width as we move away from the mean
8. Any model which can be written as a product of a data matrix with a coefficient matrix plus some error vector is a linear model (ex: $Y = \mathbb X\beta + U$)

# Definitions
- Homoscedasticity: Equivalence in variances across observations
	- Typically used for describing variance of the error
- Least Squares Estimation: Minimize the squared differences between actual and predicted values for all parameters
- $argmin f(x)$: Find the value of $x$ which produces the min value for $f(x)$
- Forecasting: Producing model outputs on new data with unknown actual response

# Additional Resources
- [Confidence vs Prediction Intervals in Regression (DataCamp)](https://www.datacamp.com/blog/confidence-intervals-vs-prediction-intervals)

# Notes
## Overview of the Linear Model
- R Programming Specifics
	- `lm(dependent_variable ~ independent_variable)` to generate a model
	- `predict()` function can also produce intervals for `"confidence"` and `"prediction"` and the <mark style="background: #FFB86CA6;">prediction interval is always larger</mark> 
	- The `predict()` function requires a dataframe object in `newdata` which has the same name
- Mathematical Expression
	- Framework: We have observations $(x_i, y_i)_{i\in [1,n]}$ and assume that $x_i$ is an observation of $X_i$ and $Y_i$ an observation of $Y_i$. Scope is to see if there is a <mark style="background: #FFB86CA6;">linear connection</mark> between the explanatory ($X_i$) and response ($Y_i$) variables
		- $\forall i \in [1,n], \hspace{2mm} y_i = a + bx_i + \epsilon_i$ with $a, b$ unknown parameters and $\epsilon$ an <mark style="background: #FFB86CA6;">unobservable noisy variable</mark>
	- We operate as though only $Y_i$ is a [[Random Variables|random variable]] because to consider $X_i$ a random variable as well requires using the conditional distribution which, in practice, simply means fixing $X_i$
## Assumptions of the Linear Model
- H1: The expectation of the error is 0
	- $\forall i, \mathbb E[\epsilon_i] = 0$
- H2: The variances of the error terms are homoscedastic
	- $\forall i, \mathbb V[\epsilon_i] = \sigma^2$
- H3: The errors for different observations are uncorrelated with each other
	- $\forall i,k; cov(\epsilon_i, \epsilon_k) = 0$ if $i\ne k$
	- NOTE: <mark style="background: #FFB86CA6;">Uncorrelated does not imply independence</mark>
- H4: The errors form a [[Random Vectors|Gaussian Random Vector]]
	- $U = \begin{pmatrix}\epsilon_1\\ \vdots\\ \epsilon_n \end{pmatrix} \sim \mathcal N(0_n, \sigma^2 I_n)$ with $0_n = \begin{pmatrix}0_1\\ \vdots \\ 0_n\end{pmatrix}$ (the "zero vector")
## Estimation of Regression Parameters
- We need to estimate $a, b, \textrm{ and } \sigma^2$
	- Cannot use the [[Constructing Estimators|method of moments]] since there are many parameters to estimate simultaneously. Instead, we use least squares estimation
- Least Squares Estimation for $\hat a_n, \hat b_n$
	- $(\hat a_n, \hat b_n) = \underset{\lambda, \gamma \in \mathbb R}{argmin}\underset{k=1}{\overset{n}{\sum}}(y_k - (\lambda + \gamma x_k))^2$
	- $\hat a_n = \bar Y_n - \hat b_n \bar X_n$
	- $\hat b_n = \frac{\sum(y_k - \bar Y_n)(x_k - \bar X_n)}{\sum(x_k - \bar X_n)^2} = \frac{\sum y_k x_k - n \bar X_n \bar Y_n}{\sum x_k^2 - n\bar X_n^2}$
	- $\hat b_n$ can also be estimated with $\frac{\sum \epsilon_k (x_k - \bar X_n)}{\sum (x_k - \bar X_n)^2} + b$ for theoretical calculations
		- Not practical since it relies on $b$ which is unknown
- Our estimators $\hat a_n, \hat b_n$ are unbiased if we can assume assumptions H1, H2, and H3
- Variance of the estimators $\hat a_n, \hat b_n$ under H1, H2, H3
	- $\mathbb V[\hat a_n] = \sigma^2 \sum x_k^2/\sum(x_k - \bar x_n)^2 n$
	- $\mathbb V[\hat b_n] = \sigma^2/\sum(x_k - \bar x_n)^2$
	- $cov(\hat a_n, \hat b_n) = - \bar X_n \mathbb V[\hat b_n] = \frac{-\sigma^2 \bar x_n}{\sum(x_k - \bar x_n)^2}$
- Since $\mathbb V[\hat a_n] \textrm{ and } \mathbb V[\hat b_n]$ depend on $\sigma^2$, we need an estimator, $\hat \sigma^2_n$
	- Such an estimator is $\frac{1}{n-2}\underset{k}{\sum}\hat \epsilon_k^2 \textrm{ with } \hat\epsilon_k = y_k - \hat y_k$
	- The sum of the squared residuals debiased by dividing by n-2 since $Y \perp X$ and $X$ is a vectorial subspace with dimension n-2
## Forecasting and Prediction Intervals
- Forecasting allows us to have an idea about the response variable when presented with new explanatory variables
	- ex: $\hat y_{new} = \hat a_n + \hat b_n x_{new}$
- Given $Y_{new} = a + b X_{new} + \epsilon_{new} \textrm{ with } \epsilon {\perp \!\!\! \perp} \epsilon_1, \dots, \epsilon_n \textrm { and } \epsilon_{new} \sim \mathcal N(0, \sigma^2)$
	- The length of the prediction interval for $Y_{new}$ interval is $2\cdot\hat\sigma_n \sqrt{a + \frac{1}{n}\frac{(X_{new} - \bar X_n)^2}{\sum(X_k - \bar X_n)^2}}$ which is an increasing function of the distance from the mean $\bar X_n$
	- $Y_{new} - \hat Y_{new} \sim \mathcal N(0, \sigma^2 (1 + \frac{1}{n}((X_{new} - \bar X_n)^2)/\sum(X_k - \bar X_n)^2))$
	- $\mathbb E[Y_{new} - \hat Y_{new}] = 0$
	- $\mathbb V[Y_{new} - \hat Y_{new}] = \mathbb V[a + b X_{new} - \hat a_n - \hat b_n X_{new} + \epsilon_{new}] = \sigma^2(1 + \frac{1}{n}\frac{(X_{new} - \bar X_n)^2}{\sum (X_k - \bar X_n)^2})$
		- Only true if $X_{new}$ not in $\begin{pmatrix}X_1\\ \vdots \\ X_n \end{pmatrix}$. Otherwise $\epsilon_{new}\hspace{1.5mm} {\not\!\perp \!\!\! \perp} \begin{pmatrix}\epsilon_1 \\ \vdots \\ \epsilon_n \end{pmatrix}$ 
## Matrix Notation of the Linear Model
- Objects
	- $\beta$: A vector of coefficients $\begin{pmatrix}a\\ b\end{pmatrix}$
	- $Y$: A vector of response observations $\begin{pmatrix} y_1 \\ \vdots \\ y_n \end{pmatrix}$
	- $U$: A vector of errors $\begin{pmatrix}\epsilon_1 \\ \vdots \\ \epsilon_n \end{pmatrix}$
	- $\mathbb X$: A matrix of explanatory observations $\begin{pmatrix}1, x_1 \\ \vdots, \vdots \\ 1, x_n \end{pmatrix}$
		- [[Matrices|Rank]] of $\mathbb X$ is 2 in the simple linear model
- We can write the linear model as the explanatory variables multiplied with the coefficient vector added with the error term
	- $Y = \mathbb X \beta + U \Leftrightarrow \begin{pmatrix}y_1 = a + bx_1 + \epsilon_1 \\ \vdots \\ y_n = a + bx_n + \epsilon_n \end{pmatrix}$
- $\hat Y$ is the orthogonal projection of $\mathbb X$ on $Y$
	- $\hat Y = P_{\mathbb X} Y = \mathbb X (\mathbb X^T\mathbb X)^{-1}\mathbb X^T Y$
	- $\mathbb X (\mathbb X^T\mathbb X)^{-1}\mathbb X^T$ is the matrix of the orthogonal projection of $Y$ on the linear subspace $\epsilon_{\mathbb X}$
- Residuals ($Y - \hat Y$)
	- $\hat U = Y - \hat Y = Y - \mathbb X (\mathbb X^T\mathbb X)^{-1}\mathbb X^T Y$
	- $= (I - \mathbb X (\mathbb X^T\mathbb X)^{-1}\mathbb X^T) Y$
	- $= (I - \mathbb X (\mathbb X^T\mathbb X)^{-1}\mathbb X^T)(\mathbb X\beta + U)$
		- Define $I - \mathbb X (\mathbb X^T\mathbb X)^{-1}\mathbb X^T$ as $R$
	- $= RU$
	- When we assume Gaussian noise (H4), $U$ is a Gaussian random vector and $\hat U$ is a Gaussian random vector as well since $R$ is deterministic
	- <mark style="background: #FFB86CA6;">Therefore</mark>, $\forall i, y_i - \hat y_i$ <mark style="background: #FFB86CA6;">is a Gaussian random variable</mark>
	- The expectation is the zero vector: $\mathbb E[\hat U] = \mathbb E[RU] = R\mathbb E[U] = 0_n$
		- So, $\forall i,\hspace{1.5mm} \mathbb E[y_i - \hat y_i] = 0$
	- The variance is $\sigma^2$ multiplied with the projection matrix $R$
		- $\mathbb V[\hat U] = \mathbb V[RU] = R\mathbb V[U]R^T = \sigma^2RR^T = \sigma^2R^2 = \sigma^2R$\
			- Since $R$ is a projection matrix, $R^2 = R = R^T$
			- $\mathbb V[U] = \sigma^2 I$
		- Since $R$ is not the identity matrix, the <mark style="background: #FFB86CA6;">residuals do not all have the same variance and are therefore not identically distributed</mark>
	- We can take the standardized residuals however which makes them normally distributed
		- $\hat U^{(sd)}_i = (y_i - \hat y_i)/(\hat \sigma_n \sqrt{R_{ii}}) \sim \mathcal N(0,1)$ with $R_{ii}$ as the term at row and column $i$ of $R$
	- We cannot determine the exact distribution of the standardized residuals, so we use Studentized residuals
		- $\hat U^{(st)}_i = (y_i - \hat y_i)/(\hat \sigma_{n, i} \sqrt{R_{ii}}) \sim \mathcal T(n-3)$
		- $\hat \sigma^2_{n, i}$ is an estimator of $\sigma^2$ when we perform the linear model on learning sample $\{(x_k, y_k), \hspace{1.5mm} k \in [1,n],\hspace{1mm} k\ne i\}$; <mark style="background: #FFB86CA6;">estimate the variance without the current observation in the sample</mark>