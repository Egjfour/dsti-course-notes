|                          Course Name                          |         Topic         |     Professor     |       Date       |    Tags     |
| :-----------------------------------------------------------: | :-------------------: | :---------------: | :--------------: | :---------: |
| **Statistical Analysis of Massive and High Dimensional Data** | Classification Models | Charles Bouveyron | 14 novembre 2025 | #Statistics |
|                     **Survival Analysis**                     |    General Models     |  Anna Sterantino  | 16 décembre 2025 | #Statistics |

[Class Video Link 1](https://dstisas.sharepoint.com/sites/RecordingsArchive/_layouts/15/stream.aspx?id=%2Fsites%2FRecordingsArchive%2FShared%20Documents%2FA24%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20251114%5F085109%2DMeeting%20Recording2%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E3bd9b3df%2Dc164%2D483f%2Dabb4%2D36a6a141d1e9)
[Class Video Link 2](https://dstisas.sharepoint.com/sites/RecordingsArchive/_layouts/15/stream.aspx?id=%2Fsites%2FRecordingsArchive%2FShared%20Documents%2FA24%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20251216%5F085721%2DMeeting%20Recording1%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E8b0a93b1%2D3ad9%2D4547%2D8a46%2Dd4e32b0fdfed)

# Summary
*Logistic regression is an outlier-robust classification model that transforms a classification problem into a regression one using the logistic function. This model looks to understand the difference between logits and the independent variables to create a generative classification based on conditional probability. The interpretation of the model is similar to that of the linear model, but we express the coefficients as log-odds.*

# Key Takeaways
1. Unlike the [[Simple Linear Model|linear model]], there is no closed form solution to logistic regression
2. Tends to be more robust to outliers since no distribution is assumed like in [[Linear Discriminant Analysis (LDA)|LDA]]

# Definitions
- Generative Classification Method: Methods which assume a model for each class ($P(X|Y)$) from which we can determine $P(Y|X)$
- Odds: The ratio of the probability of success to the probability of failure
	- The probability of getting a 4 when throwing a fair 6-sided dice is 1/6 or ~16.7%. On the other hand, the odds of getting a 4 are 1:5

# Additional Resources
- [Logistic Regression Overview](https://www.geeksforgeeks.org/machine-learning/understanding-logistic-regression/)
- [Binary Classification Regression Models](https://daviddalpiaz.github.io/r4sl/logistic-regression.html)
- [Interpreting Logistic Regression Coefficients](https://medium.com/data-science/a-simple-interpretation-of-logistic-regression-coefficients-e3a40a62e8cf)

# Notes
## Logistic Model
- The logistic regression is a binary classification method
	- Often considered a reference method
- Turns classification into regression using the logistic function
	- $logit(P(y= 1 |X; \theta)) = \log(\dfrac{P(y = 1 | X;\theta)}{P(y = 0| X;\theta)})$
	- $=\beta_0 + \beta X + \epsilon$ with $\epsilon \sim \mathcal N(0, \sigma^2)$
- We use [[Constructing Estimators|maximum likelihood]] to estimate $\theta = \{\beta_0, \beta, \sigma^2\}$
	- $\hat f(x^*) = \underset{c}{argmax}P(y = c | X = x^*; \hat \theta)$
	- and $P(y = 1| X) = exp(\hat \beta_0 + \hat \beta X)/(1 + exp(\hat\beta_0 \hat\beta X))$
- This model <mark style="background: #FFB86CA6;">works poorly in high-dimensional spaces</mark>
- In R, we use `glm(data, family = "binomial")` from package `glmnet`
## Interpreting Logistic Model Output
- The coefficients of the logistic regression model are presented as log-odds
	- A one-unit increase in independent variable $x_k$ results in a $\beta_k$ change in the log odds of being in the majority class
- When we exponentiate, we get the odds ratio
	- This ratio is centered at 1, so a <mark style="background: #FFB86CA6;">value of 1 means that there is no effect</mark>
- Example
	 ![[Pasted image 20260102155232.png]]