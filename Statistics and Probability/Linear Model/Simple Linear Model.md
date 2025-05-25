|                        Course Name                        |   Topic    |    Professor    |    Date     |    Tags     |
| :-------------------------------------------------------: | :--------: | :-------------: | :---------: | :---------: |
| **Foundations of Statistics and Machine Learning Part 2** | Regression | Christine Malot | 09 mai 2025 | #Statistics |

[Class Video Link](URL)

# Summary
*A 3-4 sentence description of what was learned in italics*

# Key Takeaways
1. It is essential that the error is Gaussian distributed
2. Mathematical notation: $\forall i \in [1,n], y_i = a + bX_i + \epsilon_i$
3. The individual $y_i$ are not identically distributed
4. With assumption four (the errors are a [[Random Vectors|Gaussian Random Vector]]), we can assume that our parameter vector $\begin{pmatrix}\hat a_n \\ \hat b_n \end{pmatrix}$ is a Gaussian random vector
5. $\hat Y$ is the orthogonal projection of $Y$ on $X$ and the error $\hat \epsilon \perp X$ with $X$ a vectorial subspace of dimension $n-2$
6. A confidence interval for forecasted values is $[\hat y_{new} \pm \hat\sigma_n \sqrt{1 + \frac{1}{n}\frac{(X_{new} - \bar X_n)^2}{\underset{k}{\sum}(X_k - \bar X_n)^2}}\cdot t_{1-\alpha/2;\hspace{1mm} n-2}]$
7. The further we are from $\bar X_n$, the less confident we are in the prediction

# Definitions
- Least Squares Estimation: Minimize the squared differences between actual and predicted values for all parameters
- $argmin f(x)$: Find the value of $x$ which produces the min value for $f(x)$
- Forecasting: Producing model outputs on new data with unknown actual response

# Additional Resources
- Name the hyperlink in brackets then outside the brackets put the URL in parens

# Notes
## Section 1
- Bullets on the actual content in question