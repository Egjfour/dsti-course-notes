|                        Course Name                        |  Topic  |    Professor    |      Date      | Tags |
| :-------------------------------------------------------: | :-----: | :-------------: | :------------: | :--: |
| **Foundations of Statistics and Machine Learning Part 2** | Testing | Christine Malot | Date of course |      |

[Class Video Link](URL)

# Summary
*A 3-4 sentence description of what was learned in italics*

# Key Takeaways
1. Tests on [[Simple Linear Model|regression models]] operate under the assumption of Gaussian noise
2. To choose the null, $H_0$, versus alternative, $H_1$, hypotheses, we need to choose the error which has the worse consequences
3. The goal of a hypothesis test is to create a rejection region
4. We can say that we accept the alternative hypothesis but not the null
5. Just because a test does not find a linear relationship does not mean that the two variables are [[Conditional Probability and Independence|independent]]
6. For the [[Evaluation and Metrics of Simple Linear Models|regression parameter tests]], accepting the alternative hypothesis means that 0 does not belong to the confidence interval for the estimator of the regression parameter

# Definitions
- Power of a test: The probability that we will decide $H_1$ when it is true
	- $1 - P(\textrm{other error})$
- Rejection Region: The set of all datasets composed of the observations such that we decided $H_1$
- p-value: The critical probability for choosing to accept the alternative hypothesis or failing to reject the null hypothesis. It is the probability that the estimator is greater than the estimation given the data
	- $P_{H_0}(|\hat b_n| \gt |\hat b_{n, obs}|)$ OR $P_{H_0}(|\mathcal T(n-2)| \gt \hat b_{n,obs}/(\hat \sigma_n / \sqrt{\sum (x_i - \bar x_n)^2})|)$

# Additional Resources
- Name the hyperlink in brackets then outside the brackets put the URL in parens

# Notes
## Section 1
- Bullets on the actual content in question