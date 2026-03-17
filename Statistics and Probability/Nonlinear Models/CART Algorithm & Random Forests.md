|                      Course Name                       |             Topic             |    Professor    | Date |       Tags       |
| :----------------------------------------------------: | :---------------------------: | :-------------: | :--: | :--------------: |
| **Advanced Statistical Analysis and Machine Learning** | Nonlinear Models - Tree-based | Christine Malot | N/A  | #MachineLearning |

[CART Video](https://learn.dsti.institute/mod/resource/view.php?id=29154)
[Random Forest Video](https://learn.dsti.institute/mod/resource/view.php?id=29155)


# Summary
*A 3-4 sentence description of what was learned in italics*

# Key Takeaways
1. The criterion for classification tasks is the GINI index based on posterior probabilities
2. The criterion for regression tasks is the largest between-group variance on the proposed split
3. The error of the maximal tree is zero unless all explanatory variables are the same
4. With random forests, there is no pruning step or final selection on the individual trees

# Definitions
- Tree: The process of making partitions of the feature space such that each element of the partition is a region of $\mathbb R$ on which the prediction of the response variable will be consistent
- Pruning Step: Construct the sequence of nested trees to suppress the overfitting caused by the maximal tree
- Split: A binary question involving one explanatory variable
	- $\begin{cases}X^{(i)} \lt a_i \textrm{ or } X^{(i)} \ge a_i \textrm{ if quantitative} \\ X^{(i)} \in A_i \textrm{ otherwise}\end{cases}$
- GINI Impurity: The index on posterior probabilities which serves as the goodness-of-fit criterion for classification tasks
	- $i(t) = \underset{k=1}{\overset{K}{\sum}}p(k|t) \cdot (1 - p(k|t))$
- Surrogate Split: A split which involves another explanatory variable than the one used for the best split
	- Used for determining variable selection and variable importance
- Bootstrap Sample: Subsets of individuals from the learning sample sampled uniformly with replacement
- Out-of-Bag Error: The mean prediction error on each training sample $x_i$ using only the trees which did not have $x_i$ in their bootstrap sample
- Variable Importance: A permutation-based methodology which shuffles the considered variable and recreates the forest algorithm. Then, the error and out-of-bag error are compared. Larger differences are considered to be more important

# Additional Resources
- [CART Description](https://www.geeksforgeeks.org/machine-learning/cart-classification-and-regression-tree-in-machine-learning/)
- [Permutation Variable Importance (sklearn)](https://scikit-learn.org/stable/modules/permutation_importance.html)

# Notes
## Section 1
- Bullets on the actual content in question