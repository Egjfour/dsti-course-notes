|                          Course Name                          |   Topic    |     Professor     |       Date       |       Tags       |
| :-----------------------------------------------------------: | :--------: | :---------------: | :--------------: | :--------------: |
| **Statistical Analysis of Massive and High Dimensional Data** | Clustering | Charles Bouveyron | 05 décembre 2025 | #MachineLearning |

[Class Video Link]([URL](https://dstisas.sharepoint.com/sites/RecordingsArchive/_layouts/15/stream.aspx?id=%2Fsites%2FRecordingsArchive%2FShared%20Documents%2FA24%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20251205%5F083404%2DMeeting%20Recording1%2Emp4&ga=1)

# Summary
*Clustering is the process of creating groups from a given unlabeled dataset which have members that are as similar as possible to each other and dissimilar to the members of other groups. A variety of algorithms exist for creating clusters including k-means and hierarchical. Among the most flexible, however, are the mixture models which leverage the EM algorithm to generate posterior probabilities for class membership.*

# Key Takeaways
1. K-means is a general, restricted form of the gaussian mixture model
2. In general, we seek to maximize the ratio of the between-group variance to the within group variance
3. The EM algorithm converges only towards a [[Optimization Basics & Problem Statement|local minimum]], not necessarily global
4. When clustering in [[Modeling in High-Dimensional Spaces|high dimensions]], subspace clustering is essential

# Definitions
- Clustering: Given a set of data of dimension, $D$, assign each group to a single group $X\in X^D \to y \in \{1, \dots, k\}$ such that individuals in the same group behave similarly to each other and differently from individuals in other groups
- Mixture Model: A statistical model where the [[Distributions of Probability and Random Variables|probability density function]] can be written as
	- $P(x) = \underset{k=1}{\overset{K}{\sum}}\prod_kP_k(x)$ with $\prod_k \in [0,1],\hspace{1.5mm} \sum \prod_k = 1,$ and $P_k(x)$ is a pdf
	- $P_k(x)$ can be any distribution (even discrete) but cannot be mixed

# Additional Resources
- [Clustering Overview](https://www.geeksforgeeks.org/machine-learning/clustering-in-machine-learning/)
- [Model-Based Clustering and Classification Book](https://math.univ-cotedazur.fr/~cbouveyr/MBCbook/)
- [Video - The EM Algorithm](https://www.youtube.com/watch?v=3zbAsgCf1Sw)

# Notes
## Unsupervised Overview
- Unsupervised learning covers two main categories: [[Unsupervised Learning - Dimensionality Reduction|dimensionality reduction]] and clustering
- Unsupervised methods are the largest open category of problems in data science
- These algorithms are often very sensitive to high dimensionality and variable scales
## K-Means Clustering
- Algorithm which iteratively <mark style="background: #FFB86CA6;">segments</mark> data into groups
	- Requires that we <mark style="background: #FFB86CA6;">specify the desired number of groups</mark>
	- First, initialize the $K$ centroid values and compute each point to each centroid and assign each point to its closest one
	- Then, update the centroids to be the mean of the assigned points
	- Continue this process until stable
- Evaluated by considering the within to between group variance of the groups created
	- $\textrm{Total Variance}: S = \dfrac{1}{\mu}\sum(x_i - \mu)^2 = B+W$
	- $\textrm{Within Variance}: W = \dfrac{1}{\mu}\underset{k=1}{\overset{K}{\sum}}\mu_k S_k$
	- $\textrm{Between Variance}: B = \dfrac{1}{\mu}\underset{k=1}{\overset{K}{\sum}} \mu_k(\mu_k-\mu)^2$
- The criterion to maximize then becomes $\mathcal L(K) = \dfrac{B(K)}{S}$
	- We consider this as an elbow curve
## Hierarchical Clustering
- Algorithm which iteratively <mark style="background: #FFB86CA6;">merges</mark> data into groups based on smallest distance than with respect to data distance
	- Unlike K-means, we can display all the data as a tree (dendrogram)
		- Can use this to "cut" the tree where we see the largest gap
		 ![[Pasted image 20260216122223.png]]
- Since there are many choices for the distance calculation, this actually creates a family of possible models
	- Complete: max distance between any two points of existing groups
		- Tends to form tight spherical clusters
	- Simple: min distance between any two points of existing groups
		- Tends to form long chains
	- Centroid: distance between averages of existing groups
	- Ward: Normalized centroid distance
		- Produces groups of different sizes
		- $\textrm{distance}=\dfrac{d(\bar a, \bar b)}{\frac{1}{n_a} + \frac{1}{n_b}}$
- Tends to be very difficult to use in practice due to high complexity: $O(n^2\log n$)
## Gaussian Mixture Models
- These models have deep theoretical assumptions with a lot of flexibility and options
- The mixture model here introduces a latent (unobserved) variable, $y$, which represents cluster membership
	- This is established such that $P(y=k) = \pi_k$
- The Gaussian Mixture Model is a mixture model which strictly uses the [[Distributions of Probability and Random Variables|Gaussian distribution]]
	- $p(x) = \underset{k=1}{\overset{K}{\sum}}\pi_k \mathcal N(x ; \mu_k, \Sigma_k)$
		- $\mu_k$ the mean of the $k$th component
		- $\Sigma_k$ the variance of the $k$th component
	- $y \sim M(\pi_k)$: $y$ is a <mark style="background: #FFB86CA6;">mixture of the probabilities of group memberhip</mark>
	- $x | y=k \sim \mathcal N(\mu_k, \Sigma_k)$
- Since the latent variable $y$ is unobserved, this is very difficult to estimate directly with [[Constructing Estimators|maximum likelihood]], so we use the EM algorithm
- The output of the EM algorithm gives posterior probabilities for each cluster
	- $y_i = \textrm{argmax} P(y=k | x = x_i) \overset{\textrm{Bayes}}{\propto} \hat \pi_k \mathcal N(x_i ; \hat \mu _k, \hat \Sigma_k)$
- By choosing which parameters are fixed and free, GMMs represent a family of models
	- K-means is a GMM where
		- $\pi_k = \dfrac{1}{K}$
		- $\mu_k$ is free
		- $\Sigma_k = I_p$
## The EM Algorithm
- General
	- First, suppose that $y$ is known and estimate parameter values
		- Typically start with random initialization
	- Then given values of $\theta$, deduce values for $y$
- The E-step (Expectation)
	- $\mathbb E[y | \theta^*, x]$
	- Calculate the expected values of the latent classes given the current set of parameters
- The M-step (Maximization)
	- $\theta^* = \underset{\theta}{\textrm{argmax}} \hspace{2mm}\mathbb E[\log P(x, y | \theta; \theta^*, x)]$
	- Reset the parameters by maximizing the conditional expected complete likelihood
- This algorithm converges towards a local maximum
	- So we perform <mark style="background: #FFB86CA6;">several random initializations</mark> to hopefully find a better local max
	 ![[Pasted image 20260216133527.png]]