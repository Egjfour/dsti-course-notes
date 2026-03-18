|                      Course Name                       |             Topic             |    Professor    | Date |       Tags       |
| :----------------------------------------------------: | :---------------------------: | :-------------: | :--: | :--------------: |
| **Advanced Statistical Analysis and Machine Learning** | Nonlinear Models - Tree-based | Christine Malot | N/A  | #MachineLearning |

[CART Video](https://learn.dsti.institute/mod/resource/view.php?id=29154)
[Random Forest Video](https://learn.dsti.institute/mod/resource/view.php?id=29155)


# Summary
*The CART algorithm is a tree-based methodology for both regression and classification tasks that partitions the feature space in a nonlinear fashion. The base algorithm has a tendency to overfit the data (even with pruning) and has high variance, so we often look to use random forests instead. Random forests combine hundreds of individual trees using bootstrapped sampling and feature subsampling to force the model to generalize more effectively.*

# Key Takeaways
1. The criterion for classification tasks is the GINI index based on posterior probabilities
2. The criterion for regression tasks is the largest [[Clustering|between-group variance]] on the proposed split
3. The error of the maximal tree is zero unless all explanatory variables are the same
4. With random forests, there is no pruning step or final selection on the individual trees

# Definitions
- Tree: The process of making partitions of the feature space such that each element of the partition is a region of $\mathbb R$ on which the prediction of the response variable will be consistent
- Pruning Step: Construct the sequence of nested trees to suppress the [[Evaluation of ML Models & Improving Results|overfitting]] caused by the maximal tree
- Split: A binary question involving one explanatory variable
	- $\begin{cases}X^{(i)} \lt a_i \textrm{ or } X^{(i)} \ge a_i \textrm{ if quantitative} \\ X^{(i)} \in A_i \textrm{ otherwise}\end{cases}$
- GINI Impurity: The index on posterior probabilities which serves as the [[Goodness of Fit Testing for Multiple Regression|goodness-of-fit criterion]] for classification tasks
	- $i(t) = \underset{k=1}{\overset{K}{\sum}}p(k|t) \cdot (1 - p(k|t))$
- Surrogate Split: A split which involves another explanatory variable than the one used for the best split
	- Used for determining [[Variable Selection Using Random Forest (VSURF)|variable selection]] and variable importance
- Bootstrap Sample: Subsets of individuals from the learning sample sampled uniformly with replacement
- Out-of-Bag Error: The mean prediction error on each training sample $x_i$ using only the trees which did not have $x_i$ in their bootstrap sample
- Variable Importance (Random Forests): A permutation-based methodology which shuffles the considered variable and recreates the forest algorithm. Then, the error and out-of-bag error are compared. Larger differences are considered to be more important

# Additional Resources
- [CART Description](https://www.geeksforgeeks.org/machine-learning/cart-classification-and-regression-tree-in-machine-learning/)
- [Permutation Variable Importance (sklearn)](https://scikit-learn.org/stable/modules/permutation_importance.html)

# Notes
## Decision Trees - The CART Algorithm
- Framework
	- No restriction on the explanatory variables
		- Can be quantitative or qualitative
		- <mark style="background: #FFB86CA6;">Can have missing values</mark>
	- Goal is either classification or regression
	- Algorithm Overview: 3 Main Steps
		- Construction of the maximal tree
		- Pruning step (using a [[Variable Selection - Linear Model|penalized criterion]])
		- Selection step
			- Determine best tree in the previous collection of pruned trees using [[Variable Selection - Linear Model|cross-validation error]]
- Algorithm Step 1: Constructing the Maximal Tree
	- We use a tree to divide the variable space with $p$ features into partitions that are the most similar as they can be along a single explanatory variable $y$
		- Nodes of the tree are split (indexed) such that parent node $t_k$ produces child nodes $t_{2k}$ and $t_{2k+1}
			- These splits are binary questions involving one of the variables
	- The splits are created using either the GINI index for classification or the between variance for regression
		- Classification: $\dfrac{1}{n}\sum 1 y_i \ne y_{i, T}$ (misclassification rate)
		- Regression: $\dfrac{1}{n}\sum(y_i - \hat y_{i, T})^2$
	- To determine if a node should be split, we continue to split until either
		- The node has only one individual of the learning sample
		- All the individuals in the node have the same value for the response variable
	- In the maximal tree, the error will be zero unless ALL explanatory variables are the same
- Algorithm Steps 2 & 3: Pruning and Selection
	- Given a maximal tree $T_{max}$, the penalized criterion is
		- $\gamma(T) + \alpha \dfrac{|\tilde T|}{n}$ where $\alpha \ge 0$
			- $\gamma(T)$ is the goodness of fit criterion for the current tree
			- $|\tilde T|$ is the total number of leaves
	- As $\alpha$ increases, we create a sequence of nested trees and <mark style="background: #FFB86CA6;">prefer trees with less leaves</mark>
	- In R, we can use `printcp` to compare all models and then apply either the [[Variable Selection - Linear Model|min or 1se rule]]
## Variable Importance and Variable Selection
- The variable importance is a "grade" which is given to each explanatory variable such that the higher the score, the more influential that variable is on the response
	- These scores leverage the information gained at each split
	- $VI(X^{(m)}) = \begin{cases}\underset{t\in T-\tilde T}{\sum}(R(t) - R(t_L) - R(t_R)) \textrm{ for regression}\\\underset{t\in T-\tilde T}{\sum}(i(t) - P_L i(t_L) - P_R i(t_R)) \textrm{ for classification}\end{cases}$
		- $t \in T - \tilde T$ meaning $t$, an intermediate node
		- $R$ being the between-group variance
		- $i$ being the GINI index (or Shannon entropy)
		- $P_L$ and $P_R$ being the posterior probabilities of the left and right split
	- Variable importance is <mark style="background: #FFB86CA6;">often rescaled to be between 0 and 1</mark>
- Surrogate splits are also an important concept building models and considering features
	- These consider the <mark style="background: #FFB86CA6;">next-best variable to use for a given split</mark> based on the overlap in how individuals are partitioned between the actual split and the surrogate
	- These are a method which allows us to determine what should happen if an individual is missing the observation for the explanatory variable associated with the actual split
- Variable selection traditionally would consider all possible subsets of explanatory variables
	- But this creates $2^{p} - 1$ subsets which is computationally intractable
	- Instead, we often perform variable selection by considering the variable importance and choose the most important variables until either reaching a threshold of importance or a chosen number of predictors
## Random Forests
- CART, as a method, has extremely high [[Evaluation of ML Models & Improving Results|variance]] with respect to the training data
	- Random forests solve this issue
- Individual trees are built using <mark style="background: #FFB86CA6;">bootstrapped samples</mark>
	- Each tree is a maximal tree
	- But for each split, we <mark style="background: #FFB86CA6;">randomly select</mark> `mtry` <mark style="background: #FFB86CA6;">explanatory variables and only consider splits among those variables</mark>
		- `mtry` is resampled for each split
	- No pruning or final selection is performed on these trees
- The final predictions are an aggregation of all the trees
	- $\hat f = \begin{cases}\dfrac{1}{K}\underset{k=1}{\overset{ntree}{\sum}}\hat f_{Tk} \textrm{ for regression: The average prediction of all trees}\\ \underset{j}{argmax}\{N(j)\} \textrm{ for classification: The majority vote of all trees}\end{cases}$
- In R (using package `randomForest`),
	- We define models like the `lm` function
	- The default `ntree` is 500 and `mtry` is $\dfrac{p}{3}$
	- The variable importance plot can be created using `varImpPlot({rf})`