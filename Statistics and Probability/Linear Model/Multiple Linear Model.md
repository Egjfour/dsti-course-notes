|                 Course Name                  |       Topic       |    Professor    |      Date       |    Tags     |
| :------------------------------------------: | :---------------: | :-------------: | :-------------: | :---------: |
| **Advanced Statistics and Machine Learning** | Linear Regression | Christine Malot | 27 octobre 2025 | #Statistics |

[Class Video Link](URL)

# Summary
*A 3-4 sentence description of what was learned in italics*

# Key Takeaways
1. We must be sure to use the Adjusted [[Evaluation and Metrics of Simple Linear Models|R-Squared]] for regressions with more than one variable since the R-squared increases as the number of predictors increases
2. If $\mathbb X^t\mathbb X$ is invertible, then the [[Simple Linear Model|least-squares estimator]] is $\hat \beta = (\mathbb X^t\mathbb X)^{-1}\mathbb X^tY$
3. Performing the Fisher test <mark style="background: #FFB86CA6;">requires</mark> the [[Simple Linear Model|Gaussian noise assumption (H4)]] (e.g., $U$ is a [[Random Vectors|Gaussian random vector]])
4. The Fisher test for the multiple linear model tests that ALL parameters are equal to 0: $\hat \beta = 0_p$
5. We need a correction like the Bonferroni correction when applying multiple tests since the true value of $\alpha$ under many tests $\le \alpha$
6. To perform a [[Hypothesis Testing|hypothesis test]] of a single parameter value, we use a [[Random Variables|student random variable]] to calculate the test statistic
7. The hypothesis test for regression parameters is equivalent to saying that 0 is not in the [[Confidence Intervals of Estimators|confidence interval]] for $\hat \beta_k$
8. A confidence interval for $\hat \beta_k$ is $[\hat \beta_k \pm \hat \sigma_n \sqrt{v_k} \cdot \mathcal t_{1 - \alpha/2; n - rk(\mathbb X)}]$ with $v_k = (\mathbb X^T \mathbb X)^{-1}_{k+1, k+1}$

# Definitions
- Multicollinearity: A situation in which one or more combinations of columns of the design matrix is a [[Vectors|linear combination]] of another column
	- This situation often arises in one-hot encoded categorical variables
- Fisher Test Statistic: For the multiple linear model, the Fisher test statistic is calculated as the deviance between the predictions and average scaled by the [[Vectors|rank]] of the design matrix divided by the deviance between the actuals and predictions scaled by both the sample size and rank of the design matrix
	- $F = \dfrac{||\hat Y - \bar Y_n||^2/(rk(\mathbb X) - 1)}{||Y - \hat Y||^2/(n - rk(\mathbb X))}$
	- This is distributed as a [[Random Variables|Fisher random variable]] $\sim \mathcal F(rk(\mathbb X) - 1, n - rk(\mathbb X))$
- Bonferroni Correction: A mechanism to ensure we don't over-increase the Type I error in multiple testing situations by dividing $\alpha$ by the number of tests we intend to execute

# Additional Resources
- [False Discovery Rate and Bonferroni Correction](https://www.youtube.com/watch?v=921IgQ6T6_4)

# Notes
## Overview and Notation
- We employ and extend the matrix notation of the [[Simple Linear Model|simple linear model]]
- $Y = \mathbb X\beta + U$; the model defined with
	- $U =\begin{pmatrix}\epsilon_1 \\ \vdots \\ \epsilon_n\end{pmatrix}$; the vector of error, a [[Random Vectors|random vector]]
	- $Y = \begin{pmatrix}y_1 \\ \vdots \\ y_n\end{pmatrix}$; the vector of responses, a random vector
	- $\beta = \begin{pmatrix}\beta_1 \\ \vdots \\ \beta_p\end{pmatrix}$; the p-length deterministic vector of parameters
	- $\mathbb X = \begin{pmatrix}x_1^{(1)} & x_1^{(2)} & \dots & x_1^{(p)} \\ \vdots & \vdots & \vdots & \vdots \\ x_n^{(1)} & x_n^{(2)} & \dots & x_n^{(p)}\end{pmatrix}$; a deterministic matrix of dimensions $(n, p)$
		- This is <mark style="background: #FFB86CA6;">known as the design matrix</mark>
- Assumptions are same as in the simple case around the independence, expectation, shared variance, and distribution of the error term
- The least-squares estimator for $\beta$, $\hat \beta$
	- Closed-form solution: $\hat \beta = (\mathbb X^T\mathbb X)^{-1}\mathbb X^TY$
	- Properties
		- [[Point Estimators|Unbiased estimator]] for $\beta$
		- $\mathbb V[\hat \beta] = \sigma^2 (\mathbb X^T\mathbb X)^{-1}$
		- If we assume Gaussian noise, $\hat \beta \sim \mathcal N(\beta, \sigma^2 (\mathbb X^T\mathbb X)^{-1})$
			- In particular, $\forall k \in [1,p], \hspace{1mm} \hat \beta_k \sim \mathcal N(\beta_k, \sigma^2 (\mathbb X^T\mathbb X)^{-1}_{k+1, k+1})$
		- For theoretical purposes: $\hat \beta = \beta + (\mathbb X^T\mathbb X)^{-1}\mathbb X^TU$
## Handling Multicollinearity
- If $\mathbb X^t \mathbb X$ is not invertible, we cannot determine $\hat \beta$ using the typical method. We must preprocess the data first
- We can still create a linear model however. We just must first delete the columns which are linearly dependent to create
- There is no unicity in this solution, however, as there are many choices for which column to delete
	- Good news is that <mark style="background: #FFB86CA6;">we will always get the same predictions no matter which subset we decide to keep</mark> since the linear space of the reduced design matrix is the same as the linear space of the original
## Model Evaluation
- For evaluating multiple regression, there are two possibilities: adjusted $R^2$ and a fisher test
- Adjusted $R^2$
	- Since as we add predictors, the linear subspace $\mathbb X$ increases, the numerator for the classic $R^2$ formula monotonically increases
	- We apply a penalty term based on the model complexity to arrive at adjust $R^2$
		- $R^2_{adj} = 1 - \dfrac{n}{n-rk(\mathbb X)}\cdot (1 - R^2)$ in the case where $\beta_0 = 0$
		- $R^2_{adj} = 1 - \dfrac{n - 1}{n-rk(\mathbb X)}\cdot (1 - R^2)$ in the case where $\beta_0 \ne 0$
	- This penalty adjustment means that $R^2$ has no lower bound and <mark style="background: #FFB86CA6;">can be negative</mark>
	- There is no requirement to have Gaussian noise when evaluating models with $R^2$
- Fisher Test
	- Hypotheses
		- $H_0: \beta_1 = \beta_2 = \dots = \beta_p = 0$
		- $H_1:$ at least one $\beta_k \ne 0$
	- The [[Hypothesis Testing|rejection region]] is built by comparing the modeled outputs, $\hat Y$, to a baseline of the average of $Y$, $\bar Y_n$
		- $\{||\hat Y - \bar Y_n||^2 \gt s\} = P(||\hat Y - \bar Y_n||^2 \gt s) \le \alpha$
	- There is a scaling problem in the above so we transform the dependent variable
		- $P(\dfrac{||\hat Y - \bar Y_n||^2}{||Y - \hat Y||^2} \gt s) \le \alpha$
	- We know that the following are true thanks to Cochran's Theorem
		- $\dfrac{||Y - \hat Y||^2}{\sigma^2} \sim \chi^2(n - rk(\mathbb X))$
		- $\dfrac{||\hat Y - \bar Y_n||^2}{\sigma^2} \sim \chi^2(rk(\mathbb X) - 1)$
		- $Y - \hat Y {\perp \!\!\! \perp} \hat Y - \bar Y_n$
	- We consider instead the Fisher random variable which creates the test statistic
		- $F = \dfrac{||\hat Y - \bar Y_n||^2/(rk(\mathbb X) - 1)}{||Y - \hat Y||^2/(n - rk(\mathbb X))}$
	- And we compare this against a quantile of the Fisher distribution
		- $\mathcal f_{1-\alpha; rk(\mathbb X) - 1; n - rk(\mathbb X)}$
	- But in practice, it is much easier to calculate the p-value
		- $P(F \gt F_{observed})$
	- It is essential that the Gaussian noise assumption holds to use the Fisher test