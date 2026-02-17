|                          Course Name                          |         Topic         |     Professor     |       Date       |    Tags     |
| :-----------------------------------------------------------: | :-------------------: | :---------------: | :--------------: | :---------: |
| **Statistical Analysis of Massive and High Dimensional Data** | High-Dimensional Data | Charles Bouveyron | 15 décembre 2025 | #Statistics |

[Class Video Link](https://dstisas.sharepoint.com/sites/RecordingsArchive/_layouts/15/stream.aspx?id=%2Fsites%2FRecordingsArchive%2FShared%20Documents%2FA24%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20251215%5F084914%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E000bb16a%2Dff7d%2D4654%2D8dfa%2D10116de5d45e)

# Summary
*Many computation and estimation problems arise when working in high-dimensional spaces which are becoming more and more present as data volumes increase as the world becomes connected. However, not all is lost. Since such spaces are mostly empty, many techniques leverage the emptiness and concentration of data in these spaces to effectively perform classification and clustering. It is important to note, though, that we should always seek to find models which simultaneously perform the clustering and dimensionality reduction. Else, we risk losing the valuable discriminative information.*

# Key Takeaways
1. High dimensional data introduces both numeric and [[Constructing Estimators|estimation]] problems
2. The ratio to consider when identifying if a space is high-dimensional is $\dfrac{p^2}{n}$
3. Generally, Fisher EM should be preferred, but it has a longer compute time

# Definitions
- Curse of Dimensionality: The difficulty to find an optimum in a high-dimensional space due to their emptiness
- Empty Space Phenomenon: High-dimensional spaces are mostly empty, so the data live in low-dimensional spaces
- Parsimonious Models: Making assumptions to reduce the number of parameters which must be estimated in a model
	- [[Unsupervised Learning - Clustering|K-means]] as a parsimonious version of [[Unsupervised Learning - Clustering|GMM]]
- Subspace Clustering: Explaining th phenomenon by assuming the data live in a low-dimensional and cluster-specific subspace of the original high-dimensional data
- Scree Test of Cattel: The difference between the eigenvalues of $\Sigma_k$ with a chosen value, $\tau$, such that $d_k$ is the difference greater than $\tau$

# Additional Resources
- [Curse of Dimensionality Article](https://medium.com/data-science/the-math-behind-the-curse-of-dimensionality-cf8780307d74)
- [Adjusted Rand Index for Cluster Comparison](https://www.geeksforgeeks.org/machine-learning/rand-index-in-machine-learning/)
- [HDDC R Documentation](https://www.rdocumentation.org/packages/HDclassif/versions/2.2.2/topics/hddc)
- [Fisher EM R Documentation](https://www.rdocumentation.org/packages/FisherEM/versions/1.3.2/topics/fem)
- [Sparse Fisher EM R Documentation](https://www.rdocumentation.org/packages/FisherEM/versions/1.6/topics/sfem)

# Notes
## High-Dimensional Spaces
- Example: IoT devices (sensors) with very high precision
- The curse of dimensionality introduces computational and estimation problems
	- For a full [[Unsupervised Learning - Clustering|GMM]], $\Sigma_k$ must be inverted which has the num. of parameters proportional to $p$
		- If $n$ is small relative to $p^2$, the estimates of $\Sigma_k$ are ill-conditioned (or singular) and it is difficult or impossible to invert $\Sigma_k$
	- Estimation issues can turn normally [[Point Estimators|unbiased estimators]] into biased ones
- <mark style="background: #FFB86CA6;">Distances between points are relatively smaller</mark> in HD spaces
	- This is also true for volumes. For example, the volume of the unit sphere converges to 0 as $p \to \infty$
	 ![[Pasted image 20260217091818.png]]
- Uniformity also no longer exists as a notion because the space is too large and too empty
	- Thus, the actual data largely live in a lower-dimensional subspace
- Because the data live in a smaller subspace, clustering and classification models can leverage this to easily locate and separate the data
	- This is the main principle behind what [[Support Vector Machine|SVMs]] leverage
## Avoiding the Curse of Dimensionality
- Dimension Reduction: solves having $p$ too large
	- Unfortunately, this inherently <mark style="background: #FFB86CA6;">implies loss of information</mark> making the classifications worse
- [[Variable Selection - Linear Model|Regularization]]: solves unstable [[Constructing Estimators|parameter estimation]]
- Parsimonious Models: solves number of parameters which much be estimated
	- Imposes restrictions by making assumptions on the model
- None of these solutions actually solve the problem though
## High-Dimensional Clustering
- Ideally, we would <mark style="background: #FFB86CA6;">simultaneously reduce dimension, regularize, and create a sub-model</mark> at the same time
	- Thus, we look to perform subspace clustering
- Mixture PPCA (MPPCA)
	- Assume the mixture includes an internal and group-specific dimension reduction through [[Unsupervised Learning - Dimensionality Reduction|PPCA]]
		- Essentially just PPCA conditioned on a cluster variable $Y$
	- Model specification
		- $y \sim M(1; \pi) \implies P(y=k) = \pi_k$
		- $Z | y = k \sim \mathcal N(z; \mu_k, I_d)$
		- $\epsilon|y=k \sim \mathcal N(\epsilon; 0, \sigma_k^2 I_p)$
		- $X = U_k^T Z + \epsilon$ if $y=k$
			- $U_k^T$ is the projection matrix of size $p,d$
			- $Z$ is the latent representation of the data in $\mathbb R^d$
			- $\epsilon$ is additive noise in $\mathbb R^p$
	- This model allows for the recovery of the marginal distribution of $X$
		- $p(X) = \underset{k=1}{\overset{K}{\sum}}\pi_k \mathcal N(x ; U_k\mu_k, U_k^TU_k+\sigma^2_kI_p)$
		- This is a [[Unsupervised Learning - Clustering|GMM]] with a specific covariance: $\Sigma_K = U_k^TU_k+\sigma^2_kI_p$
	- Model assumes that all components (elements of $Y$) share the same dimensionality with $d << p$
	- So, $k$ and $d$ is chosen using typical model selection with [[Variable Selection - Linear Model|BIC]]
		- $BIC = \log \mathcal L(x; \hat\theta) - \dfrac{V(M)}{2}\log n$
		- $V(M) = K-1 + K_d + K(\dfrac{p(d+1)}{2} + 1)$
	- This is considered a parsimonious model of the full GMM
		- A full GMM is recovered if $d=p-1$
- High-Dimensional Data Clustering (HDDC)
	- A generalization of MPPCA by relaxing the constraint on $d$ and allowing constraints on other parameters
	- Model specification
		- $y \sim M(1; \pi) \implies P(y=k) = \pi_k$
		- $Z | y = k \sim \mathcal N(z; \mu_k, I_{dk})$
			- with $\mu_k \in \mathbb R^{d_k}$
		- $\epsilon|y=k \sim \mathcal N(\epsilon; 0, \sigma_k^2 I_p)$
		- $X = U_k^T Z + \epsilon$ if $y=k$
	- There are <mark style="background: #FFB86CA6;">28 total possible models in this family</mark>
		- $[a_{kj}; b_k, Q_k, d_k]$ is the most general (MPPCA with a free $d_k$)
		- $[a_{kj}; b_k, Q_k, d_k]$ is MPPCA
		- $[a_{j}; b, Q, d]$ is [[Unsupervised Learning - Clustering|k-means]] + [[Unsupervised Learning - Dimensionality Reduction|PCA]]
	- To choose the dimension, we avoid combinatorial explosion by applying the scree-test of Cattel
	- BIC is used to select
		- One of the sub-models of the family
		- The value $K$ (number of clusters)
		- $\tau$ for choosing the dimension reduction
- Implementation in R
	- Package `HDclassif` implements both since MPPCA is a specification of HDDC
	- `hddc(X,K = 3,model="AkjBkQkDk",threshold = 0.05, criterion = "bic")`
	 ![[Pasted image 20260217102208.png]]
## The Fisher-EM Algorithm
- Combines the idea of a low-dimensional subspace with [[Linear Discriminant Analysis (LDA)|discriminative subspaces]]
	- The original supervised case is Fisher Discriminative Analysis (FDA) which seeks to find the dimension which best separates the clusters/classes
- Fisher EM extends this to the unsupervised case
	- $X = U^Ty + \epsilon$
		- $U \in M_{p,d}$
			- Assumed to generate a discriminative subspace
		- $\epsilon \sim \mathcal N(0, \psi)$
		- $y | Z = k \sim \mathcal N(\mu_k, \Sigma_k)$
			- $\mu_k \in \mathbb R^d$
			- $\Sigma_k \in M_{d,x}$
	- Alternates between the E and F steps at step $k$
		- The E-step produces $t^{(k)}_{ik}$ as in a classical [[Unsupervised Learning - Clustering|EM algorithm]]
		- The F-step estimates $U$ such that it <mark style="background: #FFB86CA6;">maximizes the ratio of between to total variance</mark>
			- $t_k(\dfrac{U^TB^{(k)U}}{U^TSU})$
			- with $B^{(k)} = \dfrac{1}{\mu}\underset{k=1}{\overset{K}{\sum}}\mu^{(k)}_k(\mu^{(k)}_k - \mu)^T(\mu^{(k)}_k - \mu)$
				- with $\mu^{(k)}_k = t_{ik}^{(k)}\dfrac{x_i}{n}$
	- The M-step estimates other parameters
		- $\hat\pi_k^{(k)}, \hat\mu_k^{(k)}, \hat\Sigma_k^{(k)}$
		- Maximizes the expectation of the complete log-likelihood at step $k$
- A sparse version of this algorithm exists as well
	- Can add sparsity step to the F-step, add an L1 penalty to the F-step, or use sparse SVD (significant computation time reduction with sparse SVD)
- Implemented in R using the `FisherEM` package
	- Regular: `fem(X,K=3,method = "svd",model = 'all')`
	- Sparse: `sfem(X,K = 3,obj = out.fem,l1 = 0.1)`
		- Needs to be initialized with a previously learned Fisher-EM model