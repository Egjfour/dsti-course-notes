|                          Course Name                          |         Topic         |     Professor     |       Date       |    Tags     |
| :-----------------------------------------------------------: | :-------------------: | :---------------: | :--------------: | :---------: |
| **Statistical Analysis of Massive and High Dimensional Data** | Classification Models | Charles Bouveyron | 14 novembre 2025 | #Statistics |

[Class Video Link](https://dstisas.sharepoint.com/sites/RecordingsArchive/_layouts/15/stream.aspx?id=%2Fsites%2FRecordingsArchive%2FShared%20Documents%2FA24%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20251114%5F085109%2DMeeting%20Recording2%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Eac897b27%2D9a80%2D4846%2D92c6%2D59f82a202e49)

# Summary
*LDA is a reference method that presumes classes can be identified using a linear projection. The output of the model is the posterior probability for a set of continuous inputs to be in a given class. This model is useful as well because it has no hyperparameters to tune.*

# Key Takeaways
1. LDA is an old method which is often used as a reference to compare to other methods
2. It is like [[Dimensionality Reduction|Principle Components Analysis]] but focuses on maximizing the separability of known categories
3. LDA is multiclass by nature (unlike [[Logistic Regression|logistic regression]] which is designed for binary classification)
4. Only works for continuous data with low dimensionality ($p \le 25$)

# Definitions
- Discriminative Classification Method: Methods which directly estimate the function $f(x) = P(Y | X)$

# Additional Resources
- [LDA Overview](https://www.geeksforgeeks.org/machine-learning/ml-linear-discriminant-analysis/)
- [LDA Video - StatQuest](https://www.youtube.com/watch?v=azXCzI57Yfc)

# Notes
## LDA Model
- Theory
	- All classes have an underlying [[Distributions of Probability and Random Variables|probability density function]] which is [[Random Variables|Gaussian]]
	- $X | Y = c \sim \mathcal N(\mu_c, \Sigma); \hspace{2mm} \forall c \in 1, \dots, C$
	- We create a new axis and linearly project the data onto this new axis which maximizes linear separability between classes
- Estimation - [[Constructing Estimators|Maximum Likelihood]]
	- Goal is to estimate the parameters of all classes
		- $\theta = \{\mu_1, \mu_2, \Sigma, \pi_1, \pi_2\}$
		- $\pi_k$ is the prior probability of class $k$ estimated as $\dfrac{n_c}{n}$
	- We consider as the objective function, the ratio between the means of the classes to the sum of the scatters (variances)
		- $\dfrac{(\mu_1 - \mu_2)^2}{s_1^2 + s_2^2}$ where $s_k = \sum(x_i - \mu_k)^2$
		- With more than 2 classes, we <mark style="background: #FFB86CA6;">consider the distance for each class mean to the global mean of the dataset</mark>
	- Or, otherwise stated $\hat \theta = \underset{\theta}{argmax}\prod p(x_i, y_i | \theta)$
- Assumptions
	- The data should be Gaussian
	- All classes should have the same covariance structure
	- The data must be linearly separable