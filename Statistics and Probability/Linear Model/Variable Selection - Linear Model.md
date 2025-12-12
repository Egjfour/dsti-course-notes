|                 Course Name                  |       Topic        |    Professor    |       Date       |    Tags     |
| :------------------------------------------: | :----------------: | :-------------: | :--------------: | :---------: |
| **Advanced Statistics and Machine Learning** | Variable Selection | Christine Malot | 12 novembre 2025 | #Statistics |

[Class Video Link](https://dstisas.sharepoint.com/sites/RecordingsArchive/_layouts/15/stream.aspx?id=%2Fsites%2FRecordingsArchive%2FShared%20Documents%2FA24%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20251112%5F085249%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E47c34ebd%2D0600%2D4518%2Dbd4f%2D40e1ad31c0a2)
[Class Video Link 2](https://dstisas.sharepoint.com/sites/RecordingsArchive/_layouts/15/stream.aspx?id=%2Fsites%2FRecordingsArchive%2FShared%20Documents%2FA24%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20251112%5F085249%2DMeeting%20Recording1%2Emp4&ga=1)

# Summary
*As our data grows in width (more predictors) it is important that we reduce the scope of our models and identify what is truly relevant. This process - known as variable selection - has many potential paths for linear models. The most simple is exhaustive search where we try and compare every subset of explanatory variables; this of course is inefficient. Other methods include stepwise regression which adds/deletes predictors iteratively until a stopping condition is met and penalized regression which adds a penalty term to traditional OLS.*

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
- Cross-Validation (CV): The process of taking the learning sample and dividing it into disjoint subsets and iteratively build models holding out one subset at a time for evaluation
- Cross Validation Error (CV Error): The mean of the individual error from each of the folds
- 1se Method: Select the [[Gradient Descent and Optimizers|hyperparameter]] value which is the largest such that its cross-validation error is less than the minimum cv error + 1 standard deviation
- Nested Models: Models wherein the next evaluated option is based on the current model
	- Stepwise regression but not exhaustive search
- Bagging: Split the data many times (hundreds) and average the error to get more comprehensive comparisons between models
- L1 Norm: $||X||_1 = \sum|X_k|$
	- Sum of the absolute values
- L2 Norm (Euclidean): $||X||_2^2 = \sum x_k^2$
- Akaike Information Criterion (AIC): An evaluation of likelihood which penalizes for model complexity and tends to be less conservative than the BIC
	- $AIC = 2k - 2 \cdot log(\hat L)$ with $\hat L$ the likelihood in the Gaussian setting
	- Said otherwise: $2k + \textrm{constant} + \textrm{L.S. criterion}$
	- Frequentist, approximation of the deviance (KL divergence) of the model
- Bayes Information Criterion (BIC): A modification of the AIC which tends to be more punitive to unnecessarily complex models especially for large datasets
	- $BIC = k\cdot log(n) - 2\cdot log(\hat L)$
	- `Imagine AIC as a friend who says, “Add a few details, as long as they help,” while BIC says, “Only add details if they’re absolutely necessary.”`
	- Bayesian, approximation of the integrated likelihood $\int_{\theta}log(\mathcal L(x_1, \dots, x_n; \theta))d\theta$

# Additional Resources
- [AIC and BIC](https://medium.com/@jshaik2452/choosing-the-best-model-a-friendly-guide-to-aic-and-bic-af220b33255f)
- [Ridge Regression (StatQuest)](https://www.youtube.com/watch?v=Q81RR3yKn30)
- [Lasso Regression (StatQuest)](https://www.youtube.com/watch?v=NGf0voTMlcs)
- [Bagging](https://www.datacamp.com/tutorial/what-bagging-in-machine-learning-a-guide-with-examples?utm_cid=19589720821&utm_aid=157156374951&utm_campaign=230119_1-ps-other~dsa~tofu_2-b2c_3-emea_4-prc_5-na_6-na_7-le_8-pdsh-go_9-nb-e_10-na_11-na&utm_loc=9197924-&utm_mtd=-c&utm_kw=&utm_source=google&utm_medium=paid_search&utm_content=ps-other~emea-en~dsa~tofu~tutorial~machine-learning&gad_source=1&gad_campaignid=19589720821&gbraid=0AAAAADQ9WsGRmaMj4HRU1fym4hMX5d1Hm&gclid=CjwKCAiA_orJBhBNEiwABkdmjCZwQnHeBaaATzg6-T61SDW03CJc86KsqXWxYsJYodCVNZeyz_ZnPRoCYhkQAvD_BwE)

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
- Theory (Forward)
	- $\forall k \in [1,p]$, we first consider the Fisher test
		- $H_0:$ Intercept-Only Model
		- $H_1$: Model with Intercept and $X^{(k)}$
	- Note that we have nested Gaussian spaces since $\mathscr E_{0, k} \subset \mathscr E_{1, k}$
		- If we consider least-squares criterion, we will always reject the null
	- We must determine if the benefit of $\hat Y_{1,k}$ is enough to <mark style="background: #FFB86CA6;">justify the complexity</mark>
		- We use $||\hat Y_{0,k} - \hat Y_{1,k}||^2$ to determine if we prefer $H_0^{(k)}$ or $H_1^{(k)}$
	- So, we create a known distribution from this metric
		- $\dfrac{||\hat Y_{0,k} - \hat Y_{1,k}||^2/(1)}{||Y - \hat Y_{1,k}||^2/(n-2)} \sim \mathcal F(1, n-2)$
	- We generally prefer the following however since p-values are more easily compared between models
		- With $\hat Y$ as the largest model we can consider
		- $F^{(k)} = \dfrac{||Y - \hat Y_{0,k}||^2 - ||Y - \hat Y_{1,k}||^2}{||Y - \hat Y||^2/(n - rk(\mathbb X))} \sim \mathcal F(1, n-rk(\mathbb X))$
	- We then sort according to p-value and add the predictor with the smallest p-value
	- We then consider all other predictors and repeat this process with the null including the intercept and any predictors we've added
- Theory (Backward)
	- Can simply use the `lm` function and suppress the largest p-value and recalculate the linear model without it
	- We always keep the <mark style="background: #FFB86CA6;">larger model in the alternative hypothesis</mark>
	- We continue the iterative suppression using the p-values from the same Fisher test as in the forward method until at most step 2
- Stopping Rule (Both)
	- If the smallest/largest p-value at a given step is too large/small, then stop
	- The threshold for this condition should not be equal
		- Since for forward, we prefer $H_1$, we take a larger p-value to be <mark style="background: #FFB86CA6;">less conservative with increasing model complexity</mark>
			- Typical: 0.1
		- For backward, we prefer $H_0$ (deleting independent variables), so we are more conservative with smaller p-values
			- Typical: 0.05
	- The asymmetry between forward and backward stopping conditions is why we <mark style="background: #FFB86CA6;">often do not get the same final model</mark> when implementing both methods on the same data
- Implementation
	- We use the `stepAIC` function from the `MASS` package in R
	- The default is to use the AIC or BIC as the penalty, but we can set `test = 'F'` to have it use the p-values as described in the theory above
	- We first define a minimal and maximal model and pass these into the `scope` parameter
	- Then, we use `stepAIC`
	- The output will show us the p-values at each step and compare it to the stopping condition
	```R
	# Define Maximal Model
	L=lm(Y~.,data=X)
	
	# Define Minimal (Intercept-Only) Model
	L0=lm(Y~1,data=X)
	
	# Perform all 3 variants of Stepwise Regression
	SF=stepAIC(L0,scope=list(upper=L,lower=L0),direction='forward',test='F')
	SB=stepAIC(L,scope=list(upper=L,lower=L0),direction='backward',test='F')
	SS1=stepAIC(L,scope=list(upper=L,lower=L0),direction='both',test='F')
	```
## Penalized Regression
- Theory (Ridge)
	- Initial model is $Y = \mathbb X\beta+U$ with goal to find an estimator for $\beta$
	- The estimator for $\beta$ thanks to ridge is
		- $||Y - \mathbb X\hat\beta_{Ridge}||^2_2 = \underset{a\in\mathbb R^{p+1}}{inf}||Y - \mathbb Xa||^2_2$ with $a = \begin{pmatrix}a_0\\\tilde a\end{pmatrix}$ and $||\tilde a||_2^2 \le \mathscr s$
	- The constraint is on all predictors of $a$ <mark style="background: #FFB86CA6;">except the intercept</mark>
	- We can write this [[Optimization Basics & Problem Statement|minimization problem]] thanks to the [[Constrained Optimization - Lagrangian|LaGrangian]] as
		- $||Y - \mathbb Xa||_2^2 + \lambda||\tilde a||_2^2$ for $a \in \mathbb R^{p+1}$
			- $||Y - \mathbb Xa||_2^2$ is the least squares criterion
			- $\lambda||\tilde a||_2^2$ is the penalty term
			- $\lambda = 1/\mathscr s$
	- Ridge regression offers a <mark style="background: #FFB86CA6;">closed-form solution that can be interpreted expressively</mark>
		- $\hat\beta_{Ridge,\lambda} = (\mathbb X^T\mathbb X + \lambda I_{p+1})^{-1}\mathbb X^T Y$
		- This specification also allows us to always estimate $\hat\beta_{Ridge}$ even if $\mathbb X$ is not full-rank
- Theory (Lasso)
	- The lasso specification is exactly the same except it uses the L1 norm instead of the L2 norm: $||Y - \mathbb Xa||_2^2 + \lambda||\tilde a||_1$ for $a \in \mathbb R^{p+1}$
	- Due to the L1 norm, there is no closed-form solution like with ridge
		- We do however know that $\hat\beta_{Lasso}$ is a [[Point Estimators|biased estimator]] for $\beta$ with $\hat \lambda$ the best value of $\lambda$
		- Thus, <mark style="background: #FFB86CA6;">we can use lasso to identify the subset of explanatory variables to keep then run OLS on that subset</mark> to identify the unbiased estimation of $\beta$
- Selecting $\lambda$
	- In penalized methods, there are infinitely many candidate values because there is a tunable hyperparameter, $\lambda$
	- To select the best model, we use cross validation and compare the CV error for different values of lambda
	- We tend to prefer the 1se method for selecting lambda as it results in a more conservative model and lambda tends to be more stable on different training datasets
- Implementation
	- The `glmnet` function from the `glmnet` package is used in R
	- Parameter `alpha` determines ridge (0) vs lasso (1)
	- We can also tune using cross validation with `cv.glmnet`
	- Remember that for lasso, a final OLS model using `lm` should be created using only the selected variables
	```R
	# Simple example of each model
	Ridge=glmnet(X,Y,alpha=0)
	Lasso=glmnet(X,Y,alpha=1)
	
	# CV for lambda selection with final lasso and final LM model
	Lassocv=cv.glmnet(as.matrix(X),Y,alpha=1)
	Lasso=glmnet(X,Y,alpha=1,lambda=Lassocv$lambda.1se)
	LfinLasso=lm(Y~cyl+hp+wt,data=X)
	```
## Comparing Models/Methods
- To fairly compare models using an error metric, we must compare on an [[Testing|unseen validation/test set]]
	- Data must be split at the beginning before any models are constructed
- Since comparisons are determined by the splits, we split with resampling many (typically at least 500) times and average the errors to get a more comprehensive comparison
	- This is known as bagging
- This also lets us have an estimation of the variability in the validation error of the models we're comparing