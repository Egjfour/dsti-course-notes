|                      Course Name                       |              Topic              |    Professor    | Date |    Tags     |
| :----------------------------------------------------: | :-----------------------------: | :-------------: | :--: | :---------: |
| **Advanced Statistical Analysis and Machine Learning** | Comparing Qualitative Variables | Christine Malot | N/A  | #Statistics |

[Class Video Link]([URL](https://learn.dsti.institute/mod/resource/view.php?id=29153))

# Summary
*ANOVA is the extension of the [[Simple Linear Model|linear model]] to utilize categorical variables as the predictors. In the ANOVA model, the design matrix is a one-hot encoding of the levels of the factor with the first one suppressed as the reference cell. Two-factor ANOVA models can also be created, but it is essential to check for and possibly integrate relevant cross effects.*

# Key Takeaways
1. Each level of the categorical variable represents its own predictor in the model
2. Since with an [[Simple Linear Model|intercept]], the explanatory variables would be [[Matrix Inverse|nonsingular]], we suppress one column in the feature matrix
3. The predicted response value for a given feature level is [[Descriptive Statistics|mean]] associated to the modality $i$ for that feature: $\hat y_{ik} = \bar y_i$
4. In two-factor ANOVA, we must check the influence of cross-effects first since if they are found, then both factors have influence and should be kept in the model

# Definitions
- Reference Cell: The suppressed column (feature level) which serves as the baseline
- Tukey Test: Comparison of pairs of means via multiple [[Hypothesis Testing|hypothesis tests]]
- Cross Effects: The relationship between a pair of predictors and the outcome across all combinations of feature levels
	- $\underset{j=1}{\overset{J}{\sum}}\underset{k=1}{\overset{K}{\sum}}\gamma_{jk}1_{F_i^{(1)} = a_j}1_{F_i^{(2)} = a_k}$

# Additional Resources
- [ANOVA Explained (IBM)](https://www.ibm.com/docs/en/cognos-analytics/11.2.x?topic=tests-analysis-variance-anova)

# Notes
## The One-Factor ANOVA Model
- Framework
	- Quantitative response variable $Y$
	- Qualitative explanatory variable $F$ with levels $\{a_1, a_2, \dots, a_I\}$
- The model considers each factor its own variable
	- $y_i = \mu + \underset{k=1}{\overset{I}{\sum}}\mu_k \cdot 1_{F_i = a_k} + \epsilon_i$ with
		- $\mu$ the common effect
		- $\epsilon_i$ having the same [[Simple Linear Model|assumptions as the linear model]]
	- This model creates a [[Multiple Linear Model|multiple regression]] framework
		- We write the $y_{ik}$ is the $k$th observation for group $i$ among $I$ total groups
	- <mark style="background: #FFB86CA6;">Each observation is the combination of a common effect</mark>, $\mu$, <mark style="background: #FFB86CA6;">and a specific effect</mark>, $\mu_i$
		- $\forall i \in [1, I], \hspace{1.5mm} \forall k \in [1, n_i],\hspace{3mm} y_{ik} = \mu + \mu_i + \epsilon_i$
	- This creates a feature matrix $\mathbb X$ with dimension $I + 1$
		- But this is not full-rank since the sum of the last $I$ columns equals the first
		- Thus we suppress one column (usually the second) which creates the reference cell
- Estimating $\hat\beta$ in this model is simple since $\mathbb X$ is orthogonal, $\mathbb X^T\mathbb X$ is diagonal
	- So, $(\mathbb X^T\mathbb X)^{-1}$ is just the reciprocal inverse of the elements of $\mathbb X$
		- $\begin{pmatrix}\frac{1}{n_1} & & & \\ & \frac{1}{n_2} & & \\ & & \ddots & \\ & & & \frac{1}{n_k}\end{pmatrix}$
	- And $\mathbb X^T Y$ is $\begin{pmatrix}\underset{k=1}{\overset{n_1}{\sum}y_{ik}}\\\underset{k=1}{\overset{n_2}{\sum}y_{ik}}\\ \vdots\end{pmatrix}$
		- Essentially, the mean over all responses associated to modality $i$ for the factor
- The variance is then estimated ([[Point Estimators|unbiased]]) as $\hat\sigma^2 = \dfrac{\underset{i=1}{\overset{I}{\sum}}\underset{j=1}{\overset{n_i}{\sum}}(y_{ij} - \bar y_i)^2}{n - I}$
- Evaluation
	- For model quality, we can leverage the [[Evaluation and Metrics of Simple Linear Models|R-squared]] coefficient
		- <mark style="background: #FFB86CA6;">Do not need to use the adjusted R-squared</mark>
	- Can also use the Fisher test
		- But this requires the Gaussian assumption
		- This test operates under the null hypothesis that all the groups share the same mean
	- The Tukey test allows for comparisons among specific groups
## Two-Factor ANOVA
- The framework is largely the same, but now we consider two qualitative factors $F^{(1)}$ and $F^{(2)}$ with modalities $F$ and $J$
- In this model both <mark style="background: #FFB86CA6;">individual and cross-effects are considered</mark>
	- This creates $I + J + IJ$ new variables/parameters
	- To make $\mathbb X$ full-rank, we need to suppress $1 + I + J$  total columns
- Since the combinatorial effect could introduce a lot of parameters, we should first check if cross effects are truly needed
	- In R, this can be seen looking at  the `interaction.plot`
		- If the trajectories are parallel in the plot, no cross effect is needed
- Constructing this model in R is done using the `lm` function like for regression
	- Cross effects are applied using multiplication
		- Example: `lm(Y ~ F1 + F2 + F1*F2, data = df)`
	- We can then see the significance of the entire model by calling function `anova` on the fitted `lm` object