|   Course Name    |       Topic       |   Professor   |         Date          |   Tags    |
| :--------------: | :---------------: | :-----------: | :-------------------: | :-------: |
| **Applied Math** | Minima and Maxima | Didier Auroux | 04 & 08 Novembre 2024 | #Calculus |

[Class Video Link 1](https://dstisas-my.sharepoint.com/personal/johnny_najjar_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fjohnny%5Fnajjar%5Fdsti%5Finstitute%2FDocuments%2FRecordings%281%29%2FA24%20%2D%20Common%20Link%20%2D%20DS%2DDE%2DDA%2D20241104%5F095204%2DMeeting%20Recording%201%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Ef7e71a2a%2D1691%2D457b%2Daa8c%2Dac811a75875a)
[Class Video Link 2](https://dstisas-my.sharepoint.com/personal/johnny_najjar_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fjohnny%5Fnajjar%5Fdsti%5Finstitute%2FDocuments%2FRecordings%281%29%2FA24%20%2D%20Common%20Link%20%2D%20DS%2DDE%2DDA%2D20241108%5F095114%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E0426196a%2Dabe7%2D4da3%2D9084%2D522791403eab)
# Summary
*A function is in a local optima when it is no longer increasing or decreasing at that point. To check for this, we use derivatives. The first order condition (first derivative = 0) lets us know where minima or maxima might be and the second order condition (positive or negative second derivative) lets us know if we've found a minima or maxima (respectively). When working with multiple inputs/variables, we use the gradient vector $\nabla$ for the first derivatives and the hessian matrix for the second derivatives with a key difference being that the second order condition is now calculated on the entire hessian matrix.*

# Key Takeaways
1. A necessary condition for finding a minimum or maximum or a function is that the local derivative of that function MUST be 0
2. If the second derivative is negative, then the point is a candidate for the maximum
	a. For positive values of $f''$, it is a candidate for the minimum
3. When working in multiple dimensions, we want to identify if the [[Matrix Diagonalization|entire hessian matrix is positive or negative]] to determine if we are at a minimum or maximum
4. The hessian matrix is always a [[Matrices|square, symmetric matrix]] thanks to [[Functions and Derivatives of Functions|Young's Theorem]] on the cross partial derivatives

# Definitions
- Gradient Vector: A [[Vectors|vector]] with all first order partial derivative functions
	- Referred to as "nabla" ($\nabla$)
- Hessian Matrix ($\nabla^2$): The matrix of all second-order partial derivatives based on the gradient vector

# Additional Resources
- [Optimization (Includes constraints, but main idea is there)](https://calcworkshop.com/application-derivatives/optimization-calculus/)
- [Partial Derivatives and Gradients](https://www.khanacademy.org/math/multivariable-calculus/multivariable-derivatives/partial-derivative-and-gradient-articles/a/the-gradient)

# Notes
## Optimization in Dimension 1
- Define a minimum $x^*$
	- Goal: Find $min(f(x)) \implies f(x^*)<= f(x) \forall x$
	- Opposite if finding a maximum
- Conditions:
	- Local first-order derivative must be zero
		- Not sufficient since this can be either a min or max
	- [[Functions and Derivatives of Functions|Second derivative]] tells us min or max
		- Min: positive $f''$
		- Max: negative $f''$
	- These conditions no longer hold if there are constraints
		- Instead we need to also check the extrema of the constraints
		- E.g., find the minimum of $f(x)$ s.t. $-5 <= x <= 20$
## Optimization in Multiple Dimensions
- A function of multiple variables has multiple [[Functions and Derivatives of Functions|partial derivatives]]
	- These can be arranged into a vector, the gradient vector ($\nabla$)
		- $\nabla f = \begin{pmatrix}f'_{x_1}(x_1,x_2)\\f'_{x_2}(x_1,x_2)\end{pmatrix}$
	- All the second-order conditions can then be stored in a matrix, the hessian matrix
		- $\nabla^2 f = \begin{pmatrix}\frac{\partial^2 f}{\partial x_i \partial x_j}\end{pmatrix}$
- To find a min/max of $f$,
	- $\nabla f = \textbf 0$ ; <mark style="background: #FFB86CA6;">ALL the first order conditions must be 0</mark>
	- The <mark style="background: #FFB86CA6;">entire hessian matrix must be positive (minimum) or negative (maximum)</mark>
		- Since it is symmetric, we can just check the (*sign of*) eigenvalues