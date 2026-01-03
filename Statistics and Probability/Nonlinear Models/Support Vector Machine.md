|                          Course Name                          |     Topic      |     Professor     |       Date       |       Tags       |
| :-----------------------------------------------------------: | :------------: | :---------------: | :--------------: | :--------------: |
| **Statistical Analysis of Massive and High Dimensional Data** | Classification | Charles Bouveryon | 05 décembre 2025 | #MachineLearning |

[Class Video Link](https://dstisas.sharepoint.com/sites/RecordingsArchive/_layouts/15/stream.aspx?id=%2Fsites%2FRecordingsArchive%2FShared%20Documents%2FA24%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20251205%5F083404%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Ec75f3828%2D61f5%2D4bb4%2D8a0f%2D9ac72730c8ba)

# Summary
*Support vector machines find a nonlinear projection to identify the best linear separator. Since optimization of the nonlinear function would be computationally expensive, the kernel trick allows for easier computation.*

# Key Takeaways
1. Main goal: Find a nonlinear projection operator, $\phi$, such that the classification problem can be solved linearly
2. The kernel trick is what allows is to perform the optimization directly on the raw data

# Definitions
- Support Vector: The data points which are closest to the classification boundary
- Kernel: a function that implicitly maps input data into a higher-dimensional feature space so that the classes become linearly separable, without explicitly computing that mapping. It does this by computing inner products in the feature space directly, enabling efficient learning of nonlinear decision boundaries

# Additional Resources
- [Intuitive SVM Explanation](https://medium.com/low-code-for-advanced-data-science/support-vector-machines-svm-an-intuitive-explanation-b084d6238106)
- [SVM Function - R Documentation](https://www.rdocumentation.org/packages/e1071/versions/1.7-16/topics/svm)

# Notes
## SVM Algorithm
- An SVM is a machine learning model which projects data into a higher dimensional space to simplify (linearize) the classification problem
- Once in the projected feature space, $F$, the classification boundary is the hyperplane which is furthest away from all data
	- We find this by <mark style="background: #FFB86CA6;">maximizing the distance between the support vectors' margin</mark>
- To avoid expensive nonlinear computation, we use the kernel trick
	- The kernel trick involves taking the [[Vectors|dot product]] of the projected individual data points
	- $K(x, y) = <\phi(x), \phi(y)>$
- The optimization can this be written as
	- $\underset{H}{argmax}||\phi(x_1) - \phi(x_2)||^2 = K(x_1, x_1) - 2K(x_1, x_2) + K(x_2, x_2)$
	- This rewrite transforms finding $\phi$ to finding the kernel function
## Common Kernel Functions
- Linear: $K(x, x') = <x, x'>$
- Polynomial: $K_d(x, x') = <x, x'>^d$ with $d$ a tuning parameter
- RBF: $K_{\gamma}(x, x') = exp(-\frac{1}{2\gamma}<x,x'>^2)$ with $\gamma$ a tuning parameter
	- This is the Gaussian kernel
## Implementation in R
- Package `e1071` is used
	- Function `svm` lets us fit a support vector machine model
	- `svm(X, y, kernel = "linear", cost = 1)`
- Example: Function to find best gamma value
	 ```R
 find_SVM_best_gamma <- function(X, Y){
    gamma_values <- 10^seq(-5, 1, by = .75)

    folds <- sample(1:5, nrow(X), replace = TRUE)

    folds %>% map(~{
        learn = which(folds != .)
        errors <- sapply(gamma_values, function(gamma) {
            model <- svm(X[learn, ], Y[learn], kernel = "radial", gamma = gamma)
            predictions <- predict(model, X[-learn, ])
            mean(predictions != Y[-learn])
        })
        return(errors)
    }) %>% reduce(`+`) / 5 -> avg_errors

    best_gamma <- gamma_values[which.min(avg_errors)]
    return(best_gamma)
	}
	  ```