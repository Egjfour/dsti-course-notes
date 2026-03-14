|                      Course Name                       |            Topic             | Professor | Date |       Tags       |
| :----------------------------------------------------: | :--------------------------: | :-------: | :--: | :--------------: |
| **Advanced Statistical Analysis and Machine Learning** | Nonlinear Variable Selection |    N/A    | N/A  | #MachineLearning |

[Reference](https://inria.hal.science/hal-01096233v1)

# Summary
*VSURF is a method which employs random forests in a multi-step procedure to identify the most useful variables among many predictors. It consists of finding the most important predictors with redundancy and then reducing the set to the minimum number of predictors required to have a good-enough model. This serves as a nonlinear version of [[Variable Selection - Linear Model|variable selection under the linear model]]*

# Key Takeaways
1. VSURF does not use [[CART Algorithm & Random Forests|normalized importance scores]] but instead creates a data-driven solution
2. The variance of variable importance for true variables is greater than that of useless ones

# Definitions
- Interpretation: Find important variables highly related to the response variable even if they are redundant
- Prediction: Find a smaller number of variables with low redundancy which are sufficient for good-enough prediction of the response variable

# Additional Resources
- [R Package Docs](https://www.rdocumentation.org/packages/VSURF/versions/1.2.1/topics/VSURF)

# Notes
## Explanation of Methodology for Random Forest Variable Selection (VSURF)
The VSURF methodology performs two variable selection objectives, interpretation and prediction, by <mark style="background: #FFB86CA6;">using the prediction performance</mark>.

The algorithm generally works according to the following
1. Rank the variables by their variable importance
2. Create two subsets of potential variables
    1. A collection of nested random forest models. The variables selected then correspond to the most accurate model (using OOB error)
    2. A forward stepwise procedure which sequentially adds the sorted variables in decreasing order of importance

<i>Note that the <mark style="background: #FFB86CA6;">variable importance used here is based on feature permutation</mark> and importantly is not normalized so as to create a data-driven solution</i>

The detail of the VSURF algorithm is outlined below.
- All random forests use <mark style="background: #FFB86CA6;">2000 trees by default</mark>
- Step 1: Elimination and Ranking (keeps $m$ predictors of $p$ initial)
    - Sort variables by variable importance (averaged over 50 random forest runs)
    - Eliminate variables with little importance
        - A threshold is determined to identify these variables using the standard deviation of the VI calculations across the 50 runs
        - The standard deviation is used since more important features have a higher standard deviation in variable importance relative to useless ones according to the author
- Step 2: Interpretation (keeps $m'$ predictors of $m$ initial)
    - Construct nested RF models from $k = 1$ to $m$ and choose the set with the smallest out-of-bag error
        - Instead of the smallest, `VSURF` uses the 1se trick on 25 random forest runs
- Step 3: Prediction (determines final set of predictors of $m'$ initial)
    - Add variables in a stepwise way based on decreasing importance based on step 1
    - A variable is added only if the OOB error decrease is larger than a threshold
        - The threshold is the average absolute variation decrease for adding noisy variables (all variables $m' \notin m$)
            
            $\dfrac{1}{m - m'}\underset{j=m'}{\overset{m-1}{\sum}}|errOOB(j+1) - errOOB(j)|$

        - Essentially, we consider the variables that we already know are noisy and have deselected in step 2 and use those to create the threshold for error reduction in step 3