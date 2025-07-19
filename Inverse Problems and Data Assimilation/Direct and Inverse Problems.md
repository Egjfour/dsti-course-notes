|                Course Name                 |       Topic       |   Professor   |      Date       |   Tags    |
| :----------------------------------------: | :---------------: | :-----------: | :-------------: | :-------: |
| **Inverse Problems and Data Assimilation** | Types of Problems | Didier Auroux | 11 juillet 2025 | #Calculus |

[Class Video Link 1](https://dstisas-my.sharepoint.com/personal/blaise_pascal_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fblaise%5Fpascal%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20250711%5F095245%2DMeeting%20Recording%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E0fc78b60%2D4000%2D48d5%2Da6ad%2D709c82b7286f)
[Class Video Link 2](https://dstisas-my.sharepoint.com/personal/blaise_pascal_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fblaise%5Fpascal%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20250711%5F132853%2DMeeting%20Recording%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E85156350%2D79dc%2D43a1%2D9ae9%2D672b9c5a2c5a)

# Summary
*Inverse problems arise when we have observations of a phenomenon which can be describe by a model that takes states and parameters as input. We use these observations and our knowledge of the model to try and recover either the parameters or states. Problems are either well-posed or ill-posed, and ill-posed problems are very difficult to solve, so we often apply regularization to make them well-posed. Solving such problems is typically formulated as an optimization of a given cost function.*

# Key Takeaways
1. Typically, well-posed direct problems have ill-posed inverse problems
2. The normal equation always has a solution
3. Problems with large condition numbers are ill-posed. With a small condition number, the step size can be 1/condition number since it is smooth
4. To find the solution of the inverse problem, the normal equation will be used
5. We can add multiple norms with multiple epsilons to the normal equation, but the model will be more difficult to tune
6. There is a tradeoff between generalizability of the model versus the need for apriori information

# Definitions
- Direct Problem: Developing the model to determine the [[Simple Linear Model|forecast]] given the state and the parameters
- Inverse Problem: Given observations of $y$, recover $x$ and/or $p$ still having knowledge of the model, $M$
- Well-Posed Problem: Any problem which has a unique solution which depends continuously on the data
- Condition Number: The stability of the matrix
	- $\dfrac{\lambda_{max}}{\lambda_{min}}$
- Total Variation (TV) Norm: The sum of all the perturbations which allows for sharp edges and tries to flatten small variations to create more homogenous regions

# Additional Resources
- [Tikhonov Regularization (Ridge Regression)](https://en.wikipedia.org/wiki/Ridge_regression)
- [Condition Numbers and Preconditioned Conjugate Gradient Descent](https://www.youtube.com/watch?v=zjzOYL4fhrQ)
- [Preconditioning](https://www.youtube.com/watch?v=i-83HdtrI1M)

# Notes
## Overview and Examples of Inverse Problems
- Framework: We have a physical, sociological, economic phenomenon wherein we have a model which takes parameters and states as input to produce forecasts as an output
- For inverse functions we have the observations and the data-independent model, our goal is to recover $x$ and/or $p$
	- Typically observations are noisy, partial, and/or indirect
	- Normally we only try to recover $x$ or $p$ but not both. Model calibration is the 
- Example - Heat Equation (how does temperature evolve in some domain)
	- Need to consider natural convection, fans, etc and how heat moves within the system
	- Temperature, $u$, is a function of $x$ and possibly of time
		- $(a(x)\cdot u'(x))' = f(x)$ where $a(x)$ is the thermal conductivity
		- Change in the thermal conductivity times the change in temperature
	- The <mark style="background: #FFB86CA6;">inverse problem takes the source and noisy observations of temperature and attempts to recover the thermal conductivity</mark>
		- To solve, we take the [[Integration|anti-derivative]] of the source term: $a(x)\cdot u'(x) = \int_0^xf(t)dt$
- Especially when there is noise, calculating integrals and derivatives directly is often not feasible and will greatly amplify the noise
	- So, instead we use numerical approximations like $\dfrac{f(x+\epsilon) - f(x)}{\epsilon}$ for the derivative
		- Take $\epsilon > \textrm{ frequency of the noise}$
## Well-Posed and Ill-Posed Problems
- Direct problems are usually fairly easy to solve and thus are well-posed
	- However, the inverse problem of a well-posed problem is generally ill-posed
- Regularization of Ill-Posed Problems
	- Tikhonov regularization multiplies a linear model by its transpose, the L2 norm
		- $y = Mx \implies M^Ty=M^TMx$
		- This is known as the normal equation which guarantees existence of a solution but not necessarily uniqueness
	- To <mark style="background: #FFB86CA6;">ensure a unique solution, we slightly perturb the model</mark> by adding $\epsilon I$ so that the matrix is invertible ($M^TM + \epsilon I$ is positive symmetric definite but $M^TM$ is only positive symmetric)
	- We assume the solution of the perturbed problem is close to the solution of the original which is also fair since there is always error in the model itself
	- This updates the condition number to $\dfrac{\lambda_{max} + \epsilon}{\lambda_{min} + \epsilon}$
## Solving Inverse Problems
- Typically, this is done by [[Function Optimization|minimizing a function]]
	- e.g., $Mx=y \to \underset{x}{min}||Mx-y||^2$
- And we apply Tikhonov regularization
	- $\underset{x}{min}(||Mx-y||^2 + \epsilon||x||^2)$
	- Different regularization techniques require different levels of noise, so we need to be able to [[Constructing Estimators|construct an estimator]] for this noise
		- This is done by changing the other terms in the [[Optimization Basics & Problem Statement|cost function]]
		- We could use the TV norm instead for example
		- Or we could say we want small variations with respect to time: $\epsilon||x(t)||^2$
- More-stable (lower condition number) problems will converge faster and thus require less iterations of [[Algorithms - Gradient-Based Optimization|optimization algorithms]]
	- We can use the preconditioned [[Algorithms - Gradient-Based Optimization|conjugate gradient]] which is extremely efficient to solve. This process uses the inverse of the 