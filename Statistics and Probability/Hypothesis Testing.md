|                        Course Name                        |  Topic  |    Professor    |    Date     |    Tags     |
| :-------------------------------------------------------: | :-----: | :-------------: | :---------: | :---------: |
| **Foundations of Statistics and Machine Learning Part 2** | Testing | Christine Malot | 09 mai 2025 | #Statistics |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/blaise_pascal_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fblaise%5Fpascal%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FA24%20%2D%20Common%20Link%20DS%5FDE%5FDA%2D20250509%5F084930%2DMeeting%20Recording%201%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E31582eee%2D85e9%2D4aa6%2D84e8%2D5141d6ffa3aa)

# Summary
*Hypothesis testing is the statistical framework which allows us to make claims about the values of estimated values (e.g., the parameters estimated in a linear regression). These tests have us establish a null (baseline) hypothesis and an alternative (target) hypothesis. The rejection region of a hypothesis test is directly related to the region of the [[Distributions of Probability and Random Variables|distribution function]] calculated in a [[Confidence Intervals of Estimators|confidence interval]]. Tests can also be performed on entire distributions to establish whether they are "too far" away from a theoretical distribution. Such tests are called Goodness-of-Fit tests.*

# Key Takeaways
1. Tests on [[Simple Linear Model|regression models]] operate under the assumption of Gaussian noise
2. To choose the null, $H_0$, versus alternative, $H_1$, hypotheses, we need to choose the error which has the worse consequences
3. The goal of a hypothesis test is to create a rejection region
4. We can say that we accept the alternative hypothesis but not the null
5. Just because a test does not find a linear relationship does not mean that the two variables are [[Conditional Probability and Independence|independent]]
6. For the [[Evaluation and Metrics of Simple Linear Models|regression parameter tests]], accepting the alternative hypothesis means that 0 does not belong to the confidence interval for the estimator of the regression parameter
7. The distribution function for the K-S test should be a continuous function

# Definitions
- Power of a test: The probability that we will decide $H_1$ when it is true
	- $1 - P(\textrm{other error})$
- Rejection Region: The set of all datasets composed of the observations such that we decided $H_1$
- p-value: The critical probability for choosing to accept the alternative hypothesis or failing to reject the null hypothesis. It is the probability that the estimator is greater than the estimation given the data
	- $P_{H_0}(|\hat b_n| \gt |\hat b_{n, obs}|)$ OR $P_{H_0}(|\mathcal T(n-2)| \gt \hat b_{n,obs}/(\hat \sigma_n / \sqrt{\sum (x_i - \bar x_n)^2})|)$

# Additional Resources
- [KS Test (IBM)](https://www.ibm.com/docs/en/spss-statistics/cd?topic=tests-one-sample-kolmogorov-smirnov-test)

# Notes
## Statistical Tests Overview
- Three types of tests
	- Tests on one parameter
	- Goodness of fit (tests on distribution)
	- Independence
- General test elements
	- Take a decision with respect to a dataset between two hypotheses, the null ($H_0$) and alternative ($H_1$)
		- The null and alternative hypotheses <mark style="background: #FFB86CA6;">need not be collectively exhaustive</mark> (e.g., not required that $P(H_0) + P(H_1) = 1$)
	- Always performing a test of the null versus the alternative
- Tests contain some error since they are based on [[Descriptive Statistics|sample statistics]] of [[Random Variables|random variables]]
	 ![[Pasted image 20250609102048.png]]
	- We want to control the Type I error (false positive rate)
		- This type I error is ultimately what we choose $\alpha$ to be
		- The probability under the null to accept the alternative should be less than or equal to this alpha level: $P_{H_0}(\textrm{decide }H_1) \le \alpha$
			- The complement of this is the [[power of the test]]
	- We cannot simultaneously minimize both sources of error
## Creating Statistical Tests
- We must always precise the null and alternative hypotheses
	- In the context of a simple linear model, $H_0: b=0$ and $H_1: b \ne 0$ under the framework $\forall i, y_i = a + bX_i + \epsilon_i$ with [[Simple Linear Model|assumption H4]]
- We need [[Point Estimators|estimators]] of the unknown parameters and calculate estimations using observations
	- In the linear model $\hat b_n = \dfrac{\sum(x_i - \bar x_n)(y_i - \bar y_n)}{\sum(x_i - \bar x_n)^2}$ which is unbiased and distributed $\mathcal N(b, \sigma^2/\sum(x_i - \bar x_n)^2$
- Idea: We want to find a value $s$ such that the probability under the null that the absolute value of our estimation is greater than $s$ is less than or equal to our pre-determined $\alpha$
	- Linear Model: $P_{H_0}(|\hat b_n| \gt s) \le \alpha \Leftrightarrow P_{H_0}(|\hat b_n|/(\sigma^2/\sqrt{\sum(x_i - \bar x_n)^2}) \gt s/\sqrt{\sum(x_i - \bar x_n)^2}) \le \alpha$
		- We know that $\dfrac{\hat b_n - b}{\sigma^2/\sqrt{\sum(x_i - \bar x_n)^2})} \sim \mathcal T(n-2)$ and since $H_0: b=0$, our case is $|\mathcal T(n-2)|$
- We take $s$ as the worst case scenario (equal to $\alpha$)
	- $P(|\mathcal T(n-2)| > s/(\hat \sigma_n/\sqrt{\sum(x_i- \bar x_n)^2})) = \alpha$
- Now, to calculate this probability, we want to compare to the distribution function
	- Since the [[Random Variables|Student distribution]] is symmetric, we can simply use $P(\mathcal T(n-2) \le s/(\hat \sigma_n/\sqrt{(x_i - \bar x_n)^2})) = 1 - \dfrac{\alpha}{2}$
	- This is equal to $F_t(s/(\hat \sigma_n/\sqrt{(x_i - \bar x_n)^2})))$ which means $s/(\hat \sigma_n/\sqrt{(x_i - \bar x_n)^2})) = t_{1-\alpha/2;\hspace{1mm}n-2}$
- And using the distribution, we generate the rejection region
	- $\{(X_1, \dots, X_n) \in \mathbb R^n/|\hat b_n| \gt \dfrac{\hat \sigma_n \hspace{1mm} \cdot \hspace{1mm} t_{1-\alpha/2;\hspace{1mm}n-2}}{\sqrt{\sum(x_i - \bar x_n)^2}} \}$
- Using the <mark style="background: #FFB86CA6;">p-value lets us not have to worry about the selection of</mark> $\alpha$ for the impacts on the theoretical threshold
	- Linear Model: $P_{H_0}(\mathcal |T(n-2)| > |\hat b_{n, \hspace{1mm} obs}/(\hat \sigma_n/\sqrt{(x_i - \bar x_n)^2})|)$ - The probability that our estimator is larger than the estimation based on the data
## Connection to [[Confidence Intervals of Estimators|Confidence Intervals]]
- Context: Linear model with $H_0: b=0, H_1: b\ne0$
- The rejection region is $\{|\hat b_n| > \dfrac{\hat\sigma_n}{\sqrt{\sum(x_i - \bar x_n)^2}} \cdot t_{1-\alpha/2;\hspace{1mm}n-2}\}$
- A confidence interval for $b$ with confidence level $100(1-\alpha)\%$ is
	- $\hat b_n$ is an estimator for $b$ with $\hat b_n \sim \mathcal N(b, \dfrac{\hat\sigma_n}{\sqrt{\sum(x_i - \bar x_n)^2}})$
	- So we get that $\dfrac{\hat b_n - b}{\hat\sigma_n / \sqrt{\sum(x_i - \bar x_n)^2}} \sim \mathcal T(n-2)$
	- With $A_n = \hat b_n - S_n$ and $B_n = \hat b_n + P_n$ with $P(\hat b_n - S_n \le b \le \hat b_n + P_n) = 1-\alpha$
		- This can be translated to $P(-P_n \le \hat b_n - b \le S_n)$
	- Since we have a known distribution, we can also state this as $P(\dfrac{-P_n}{\hat\sigma_n / \sqrt{\sum(x_i - \bar x_n)^2}} \le \mathcal T(n-2) \le \dfrac{S_n}{\hat\sigma_n / \sqrt{\sum(x_i - \bar x_n)^2}}) = 1-\alpha$
	- By taking the complementary event, we get
		- $P(\mathcal T(n-2) \le \dfrac{-P_n}{\hat\sigma_n / \sqrt{\sum(x_i - \bar x_n)^2}}) = \alpha_1 \implies P_n = \hat\sigma_n / \sqrt{\sum(x_i - \bar x_n)^2} \cdot -t_{\alpha_1; n-2}$
		- $P(\mathcal T(n-2) \le \dfrac{S_n}{\hat\sigma_n / \sqrt{\sum(x_i - \bar x_n)^2}}) = \alpha_2 \implies S_n = \hat\sigma_n / \sqrt{\sum(x_i - \bar x_n)^2} \cdot t_{\alpha_2; n-2}$
	- This produces the confidence interval: $[\hat b_n - (\hat\sigma_n / \sqrt{\sum(x_i - \bar x_n)^2}) \cdot -t_{\alpha_1;\hspace{1.5mm} n-2}; \hspace{1.5mm}\hat b_n + (\hat\sigma_n / \sqrt{\sum(x_i - \bar x_n)^2})\cdot t_{1-\alpha_2;\hspace{1.5mm} n-2}]$
- When $\alpha_1 = \alpha_2$, we have the union of both sides of the distribution
	- If 0 is not in this interval, then we can state that $b \ne 0$ which is the alternative hypothesis
## Goodness of Fit Testing (Continuous - KS Test)
- Calculates a distance on the differences between two distributions
- The null hypothesis is that the target dataset is the same as the one proposed and the alternative is that it is different than proposed
- K-S Test Theory
	- Given a dataset associated to identically distributed random variables, we want to compare an estimated distribution function with a theoretical distribution function
	- We will reject the null if the distance is "too big"
- The distance between the distributions is the supremum of the differences between the theoretical quantile and the observed quantile
	- $\underset{t \in \mathbb R}{sup}|F(t) - F_n(t)|$ with $F_n(t) = \dfrac{1}{n}\sum \mathbb I_{Z_k \le t}$
	- $F(t)$ is a continuous increasing function and $F_n(t)$ is a stair increasing function
		- Means that we <mark style="background: #FFB86CA6;">only need to calculate the supremum for each interval</mark>