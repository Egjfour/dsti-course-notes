|                          Course Name                          |          Topic           |     Professor     |       Date       |    Tags     |
| :-----------------------------------------------------------: | :----------------------: | :---------------: | :--------------: | :---------: |
| **Statistical Analysis of Massive and High Dimensional Data** | Dimensionality Reduction | Charles Bouveyron | 05 décembre 2025 | #Statistics |

[Class Video Link](https://dstisas.sharepoint.com/sites/RecordingsArchive/_layouts/15/stream.aspx?id=%2Fsites%2FRecordingsArchive%2FShared%20Documents%2FA24%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20251205%5F083404%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Ee208a0bc%2Dc4aa%2D47b8%2Dafe8%2D4e104de8d0d4)

# Summary
*Dimensionality reduction is the set of algorithms which allow for reducing the number of predictors for a model such that the maximal information is preserved. The model famous of these methods is the principal component analysis which using [[Matrix Diagonalization|eigen decomposition]] on the [[Random Vectors|variance-covariance matrix]], but other methods exist as well to force greater reduction of the feature space or to handle [[Modeling in High-Dimensional Spaces|high-dimensional cases]].*

# Key Takeaways
1. Feature extraction methods preserve information better but [[Variable Selection - Linear Model|variable selection]] is better for interpretability
2. Probabilistic PCA reformulates PCA to a statistical analysis and produces the same solution as PCA
3. The "Rule of 90%" is often used to determine how many dimensions should be kept ($\underset{d}{argmin}\dfrac{\sum^d \lambda_i}{\sum^p \lambda_i}\ge 0.9$) or we can use a scree plot on the [[Eigenvalues and Eigenvectors|eigenvalues]]

# Definitions
- Feature Extraction: Create $d$ new variables which are combinations of the $p$ original features 
- Principle Components Analysis (PCA): Create a set of $d$ variables by [[Vectors|linear combination]] such that we have maximal variance in the projection

# Additional Resources
- [PCA Step-by-Step - StatQuest (Video)](https://www.youtube.com/watch?v=FgakZw6K1QQ)

# Notes
## Feature Extraction vs [[Variable Selection - Linear Model|Variable Selection]]
- Both techniques are dimensionality reduction
	- Feature extraction creates a mixture of variables
	- Variable selection performs a deletion of variables
- Feature extraction tends to be faster and preserves information better
## Principle Components Analysis (PCA)
- Create a model $Y = \mathbb X U^*$ such that $U^* = \underset{U}{argmax}\hspace{1.5mm}var(y)$
	- Finding the maximal variance in the projection
	- There is <mark style="background: #FFB86CA6;">no statistical assumption on this model</mark>
- Take the [[Eigenvalues and Eigenvectors|eigenvectors]] of the [[Random Vectors|empirical covariance matrix]]
	- $\Sigma = \mathbb X^T\mathbb X$ with $\mathbb X$ data after centering
	- We perform eigenvalue decomposition on $\Sigma$ and keep the vectors associated with the largest values
- In R, we use function `princomp`
- We can analyze the importance of different variables on the PCA axes using the correlation circle plot
	- The angle between vectors on this plot shows the correlation between those variables
	- `biplot` function in R which takes a result from `princomp`
	 ![[Pasted image 20260102221601.png]]
- Probabilistic PCA (PPCA) provides a <mark style="background: #FFB86CA6;">statistical model and justification for PCA</mark> by adding an error term
	- $\underset{\in \mathbb R^p}{\mathbb X} = yU^T + \epsilon$ with
		- $\epsilon \sim \mathcal N(0, \sigma^2I_p)$
		- $y \sim \mathcal N(o, I_d)$
	- Parameters $U$ and $\sigma^2$ are estimated using [[Constructing Estimators|maximum likelihood]]
	- The marginal distribution of $\mathbb X$ is $\mathcal N(0, U^TU + \sigma^2 I_p)$
- Comparing PCA methods
	- Thanks to PPCA, [[Variable Selection - Linear Model|AIC and BIC]] can be used
	- Likelihood cannot be used directly since it increases wrt dimensionality
## Sparse PCA (SPCA)
- More appropriate for high-dimensional data
	- Regular PCA may be unstable when considering many features especially if $n$ is low
- Overview: zero-out small eigenvector values by reformulating PCA to include an [[Variable Selection - Linear Model|L1 penalty]]
	- $U^* = \underset{U}{argmax}\hspace{1.5mm}\{var(\mathbb X U) - \delta||U||_1\}$
	- PCA is then optimized to the lasso penalty, though the [[Variable Selection - Linear Model|ridge (L2) penalty]] can also be used
	 ![[Pasted image 20260102224150.png]]
- In R, package `Bessel` provides options for Sparse PCA
	- `spca(x = X, K = 2, para=rep(1, ncol(X)), sparse = 'penalty')`
	- `para` should be a vector of the lambdas used for the L1/L2 penalties
- SPCA is still unlikely to completely suppress a variable (entire row of zeros in the projection)
	- Globally sparse PPCA is used to identify relevant original variables
	- $\mathbb X = VWy + \bar V\epsilon_1 + V\epsilon_2$
		- $V = diag(V)$ and $v_i \in \{0, 1\}\hspace{2mm} \forall i = 1 \dots p$
		- $W$ is the equivalent of $U$: $w_{ij} \sim \mathcal N(0, \alpha^{-2})$
		- $\epsilon_1 \sim \mathcal N(0, \sigma^2I_p)$
		- $\epsilon_2 \sim \mathcal N(0, \sigma^2I_p)$
		- $y \sim \mathcal(0, I_d)$
	- The $V$ matrix is what <mark style="background: #FFB86CA6;">indicates which variables are relevant</mark>
	- $w_{ij}$ are the weights of the relevant variables
	- $\bar V$ is the opposite (e.g., the inactive variables)
	- GSPPCA is not available on CRAN in R
	 `source('https://raw.githubusercontent.com/pamattei/GSPPCA/master/GSPPCA.R')`