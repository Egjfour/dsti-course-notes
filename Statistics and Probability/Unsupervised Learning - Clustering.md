|                          Course Name                          |   Topic    |     Professor     |       Date       |       Tags       |
| :-----------------------------------------------------------: | :--------: | :---------------: | :--------------: | :--------------: |
| **Statistical Analysis of Massive and High Dimensional Data** | Clustering | Charles Bouveyron | 05 décembre 2025 | #MachineLearning |

[Class Video Link](URL)

# Summary
*A 3-4 sentence description of what was learned in italics*

# Key Takeaways
1. K-means is a general, restricted form of the gaussian mixture model
2. In general, we seek to maximize the ratio of the between-group variance to the within group variance
3. The EM algorithm converges only towards a [[Optimization Basics & Problem Statement|local minimum]], not necessarily global
4. When clustering in [[Modeling in High-Dimensional Spaces|high dimensions]], subspace clustering is essential

# Definitions
- Clustering: Given a set of data of dimension, $D$, assign each group to a single group $X\in X^D \to y \in \{1, \dots, k\}$ such that individuals in the same group behave similarly to each other and differently from individuals in other groups
- Mixture Model: A statistical model where the [[Distributions of Probability and Random Variables|probability density function]] can be written as
	- $P(x) = \underset{k=1}{\overset{K}{\sum}}\prod_kP_k(x)$ with $\prod_k \in [0,1],\hspace{1.5mm} \sum \prod_k = 1,$ and $P_k(x)$ is a pdf
- Subspace Clustering: Explaining th phenomenon by assuming the data live in a low-dimensional and cluster-specific subspace of the original high-dimensional data
- Scree Test of Cattel: The difference between the eigenvalues of $\Sigma x$ with a chosen value, $\tau$, such that $d_k$ is the difference greater than $\tau$

# Additional Resources
- [Clustering Overview](https://www.geeksforgeeks.org/machine-learning/clustering-in-machine-learning/)
- [Model-Based Clustering and Classification Book](https://math.univ-cotedazur.fr/~cbouveyr/MBCbook/)

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
