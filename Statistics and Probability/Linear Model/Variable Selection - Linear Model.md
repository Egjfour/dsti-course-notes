|                 Course Name                  |       Topic        |    Professor    |       Date       |    Tags     |
| :------------------------------------------: | :----------------: | :-------------: | :--------------: | :---------: |
| **Advanced Statistics and Machine Learning** | Variable Selection | Christine Malot | 12 novembre 2025 | #Statistics |

[Class Video Link](https://dstisas.sharepoint.com/sites/RecordingsArchive/_layouts/15/stream.aspx?id=%2Fsites%2FRecordingsArchive%2FShared%20Documents%2FA24%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20251112%5F085249%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E47c34ebd%2D0600%2D4518%2Dbd4f%2D40e1ad31c0a2)
[Class Video Link 2](https://dstisas.sharepoint.com/sites/RecordingsArchive/_layouts/15/stream.aspx?id=%2Fsites%2FRecordingsArchive%2FShared%20Documents%2FA24%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20251112%5F085249%2DMeeting%20Recording1%2Emp4&ga=1)

# Summary
*A 3-4 sentence description of what was learned in italics*

# Key Takeaways
1. The Lasso regression does not produce an interpretable expressional form (e.g., cannot use the coefficients for inference)
2. We cannot determine which variables to suppress simply by looking at the p-values on the estimations of $\beta$
3. With Lasso, coefficients go all the way to 0 and with ridge, they only go to zero as $\lambda$ goes to $\infty$
4. We cannot evaluate models of different sizes using only the [[Simple Linear Model|least-squares criterion]] since this will always be lower as $rk(\mathbb X)$ increases, so we use the [[Multiple Linear Model|Fisher Test]] instead
5. With Lasso and Ridge methods, there are as many estimators for $\hat\beta$ as there are values for $\lambda$, so we must use cross-validation to compare and select the estimator
6. There is no variable selection in Ridge, but there is an analytic expression for $\hat\beta_{Ridge}: \hat\beta_{Ridge,\lambda} = (\mathbb X^T\mathbb X + \lambda I_{p+1})^{-1}\mathbb X^T Y$
7. The ridge method allows us to find a solution for $\hat\beta$ even under [[Multiple Linear Model|perfect multicollinearity]] when OLS would be otherwise undefined
# Definitions
- Sparsity: The notion that there are many predictors and not all of them are necessarily relevant
- Penalized Methods: Instead of minimizing the [[Simple Linear Model|least squares criterion]], we minimize it [[Constrained Optimization - Lagrangian|under constraint]]
- Cross-Validation: The process of taking the learning sample and dividing it into disjoint subsets and iteratively build models holding out one subset at a time for evaluation 
- 1se Method: Select the [[Gradient Descent and Optimizers|hyperparameter]] value which is the largest such that its cross-validation error is less than the minimum cv error + 1 standard deviation
- Nested Models: Models wherein the next evaluated option is based on the current model
	- Stepwise regression but not exhaustive search
- Bagging: Split the data many times (hundreds) and average the error to get more comprehensive comparisons between models
- L1 Norm: $||X||_1 = \sum|X_k|$
	- Sum of the absolute values
- L2 Norm (Euclidean): $||X||_2^2 = \sum x_k^2$

# Additional Resources
- [Ridge Regression (StatQuest)](https://www.youtube.com/watch?v=Q81RR3yKn30)
- [Lasso Regression (StatQuest)](https://www.youtube.com/watch?v=NGf0voTMlcs)

# Notes
## Overview
- Scope: Starting with $p$ explanatory variables, we construct a linear model. Do we really need all $p$ exp. vars to explain or can we reduce the subset and eliminate sparsity
- 3 Main Methods
	- Exhaustive Search: Consider all possible subsets of variables and compare
		- Creates $2^p - 1$ models to compare so intractable if $p$ too large
		- `leaps` package in R
	- Step-by-Step: Either forward (addition) or backward (deletion) of variables to the model one-by-one via a recursive strategy
		- Creates $\dfrac{p(p+1)}{2}$ models to compare
		- `MASS` package in R
	- Penalized Methods: Lasso and ridge techniques
		- Only one model to build but introduces a tunable hyperparameter
		- `glmnet` package in R
- Determining Relevance/Need for Variable Selection
	- Correlation between independent variables (strong correlation = likely redundancy)
	- Check [[Multiple Linear Model|adjusted R-squared]]
	- Use the Fisher test
	- Non-significance of some p-values on the coefficient estimation
		- NOTE: <mark style="background: #FFB86CA6;">This does NOT tell us which variables may be suppressed</mark>
## Exhaustive Search
- Theory
	- We consider the criterion the adjusted $R^2$ and examine <mark style="background: #FFB86CA6;">all possible subsets</mark> of predictors
	- For each possible subset, we calculate a linear model and the criterion
	- We keep the subset of explanatory variables associated to the largest adj. $R^2$
	- Problem: These models are not nested, so going from $k$ to $k + 1$ explanatory variables may result in completely different subsets of variables being selected
- Implementation
	- While there are other criterion we can choose, we should select `"adjr2"`
	- Parameter `nbest` determines how many models to display for each possible number of predictors chosen
		- Set to 1 for the final model, but we can create boxplots to understand variability of our criterion with respect to number of predictors by increasing this value
	- Example: `model_exhaustive = leaps(X,Y,method='adjr2',nbest=1)`
## Step-by-Step/Stepwise Regression
