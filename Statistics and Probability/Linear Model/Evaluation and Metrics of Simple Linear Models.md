|                        Course Name                        |          Topic          |    Professor    |       Date       |    Tags     |
| :-------------------------------------------------------: | :---------------------: | :-------------: | :--------------: | :---------: |
| **Foundations of Statistics and Machine Learning Part 2** | Linear Model Evaluation | Christine Malot | 07 & 09 mai 2025 | #Statistics |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/blaise_pascal_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fblaise%5Fpascal%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FA24%20%2D%20Common%20Link%20DS%5FDE%5FDA%2D20250507%5F084913%2DMeeting%20Recording%201%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E9745aef7%2D0aa1%2D46f7%2Dafb3%2D6170b9eff77d)

# Summary
*[[Simple Linear Model|Linear models]] have many mechanisms which allow us to determine how reliable the results are. Some of these rely heavily on the underlying assumptions of the linear model (in particular [[Simple Linear Model|H4]]) like the t-value and standard error calculations. Others, however, are less restrictive and are useful when these assumptions are not guaranteed like R-squared. There are many methodologies to determine if the Gaussian assumption is upheld such as the Q-Q plot and K-S test.*

# Key Takeaways
1. A histogram of the residuals is not an appropriate evaluation because the residuals are not identically distributed
2. The t-value is the ability, under Gaussian settings, to [[Hypothesis Testing|test]] if $b=0$ or $b\ne0$
3. $R^2$ is what is used when we are not operating in a Gaussian setting to see if there is a linear connection between the dependent and independent variables
4. $R^2$ can be defined as $1 -$ the ratio of the residual sum of squares to the total sum of squares $SSR/SST$ or as the sum of explained residuals over the sum of total residuals $SSE/SST$

# Definitions
- Estimate Standard Error: Square root of the variance of the estimated parameters
- Residual Standard Error: Square root of the variance of the entire model
	- $\sigma = \sqrt{\frac{1}{n-2}\underset{k=1}{\overset{n}{\sum}}(y_k - (\hat a_n - \hat b_n x_k))^2}$
- Regression t-value: The ratio between a parameter estimate and its standard error
- R-squared value: The ratio between the square [[Vectors|norm]] of the difference between the predicted and average values with the square norm of the difference between the actual values and the average
	- $\frac{||\hat Y-\bar Y_n||^2}{||Y-\bar Y_n||^2} = \frac{\sum(\hat Y_k - \bar Y_n)^2}{\sum(Y - \bar Y_n)^2} = 1 - \frac{\sum(Y_k - \hat Y_k)^2}{\sum(Y_k - \bar Y_n)^2}$
- Total Variance ($SST$): $||Y - \bar Y_n||^2$
- Residual Variance ($SSR$): $||Y-\hat Y||^2$
- Explained Variance ($SSE$): $||\hat Y - \bar Y_n||^2$
	- Variance of the $Y_k$

# Additional Resources
- 

# Notes
## Regression Metrics
- Regression metrics allow us to evaluate the quality of the model and make certain statements about the inferential results via [[Hypothesis Testing|hypothesis testing]]
- The output for a linear model in R contains many metrics about the parameter estimations as well as the model as a whole
	- ![[Pasted image 20250608141318.png]]
- This output (from the `summary` function on the fitted model object in R) includes the standard errors for the estimates and residuals, the t-values, and the R-squared value
- The column `Pr(>|t|)` represents the [[Hypothesis Testing|p-value]] for the <mark style="background: #FFB86CA6;">test on the given parameter to be different from 0</mark>
## Verification of Gaussian Assumptions (Q-Q Plots)
- We want to verify the [[Simple Linear Model|homoscedasticity]] of the residuals
	- The residuals plot should not exhibit any fanning or other patterns
	- A quantile-quantile (Q-Q plot) also demonstrates how Gaussian the noise is
	- The Kolmogorov-Smirnov test (a [[Hypothesis Testing|Goodness of Fit test]]) tests the Gaussian assumption
		- `ks.test()` in R
- Q-Q Plots
	- Assume we want to see if our observations which are associated to [[Distributions of Probability and Random Variables|identically distributed]] random variables $Z_1, \dots, Z_n$ which are associated to a Gaussian distribution
		- We should use [[Simple Linear Model|standardized/studentized residuals]] for this
	- We sort the $Z_k$ in increasing order
	- $z_i$ is the empirical quantile associated to order $\frac{i}{n}$
		- Since this is not a [[Applications and Compositions of Sets|bijection]], there is no inverse, however there is a generalized inverse: $\forall p \in [0,1], F_n^{-1}(p) = inf\{t \in \mathbb R/F_n(t) \ge p\}$
	- Theoretical quantiles are calculated $t(i) = F^{-1}(\frac{1}{n})$ with $F$ the distribution function of the Gaussian distribution
	- The plot is simply the cloud of points $(t_i, z_i)$
		- <mark style="background: #FFB86CA6;">If the Gaussian assumption is correct, the points are close to the line</mark> $(x,x)$