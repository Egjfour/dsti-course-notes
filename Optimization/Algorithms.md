|         Course Name         |      Topic       |   Professor   |      Date       |          Tags          |
| :-------------------------: | :--------------: | :-----------: | :-------------: | :--------------------: |
| **Continuous Optimization** | Gradient Methods | Didier Auroux | 23 janvier 2025 | #Programming #Calculus |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/johnny_najjar_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fjohnny%5Fnajjar%5Fdsti%5Finstitute%2FDocuments%2FRecordings%281%29%2FA24%20%2D%20Common%20Link%20%2D%20DS%2DDE%2DDA%2D20250123%5F095328%2DMeeting%20Recording%201%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E068de554%2Df521%2D47b5%2Db281%2D8261cacb238a)

# Summary
*Gradient methods are the mechanism through which function optimization is conducted using code. These methods analyze a [[Optimization Basics & Problem Statement|cost function]] and utilize the negative gradient to determine what direction to move in. Additional enhancements to this algorithm include performing a line search to optimize the step size at each iteration as well as combining information from the previous gradient in a linear combination to take a more optimal step (the conjugate gradient method).*

# Key Takeaways
1. The direction of the step $d_u$ in gradient descent should be the opposite of the gradient to ensure that $<\nabla J(J_k), d_k>$ is negative
2. The Lipschitz constant, $M$, is always the max of the [[Eigenvalues and Eigenvectors|eigenvalues]] of the Hessian matrix
3. The gradient descent with optimal step changes the step size at each iteration to find the step that minimizes cost
4. The conjugate gradient method finds the best linear combination of the directions and rho values
5. The conjugate gradient converges in $n+1$ steps

# Definitions
- Lipschitz Continuous: Lipschitz continuity is a condition where a function's rate of change is bounded by a constant, ensuring that the function does not change too quickly.
	- If your function is differentiable, Lipschitz continuity just says that the function has bounded derivative
	- "If $x$ and $y$ are close in value, then $f(x)$ and $f(y)$ must also be close in value"
- Conjugate: $<\mathcal H d_k, d_{k+1}>$

# Additional Resources
- [Understanding Lipschitz Continuity](https://math.stackexchange.com/questions/2374289/understanding-lipschitz-continuity)
- [Wolfe Stopping Conditions](https://scicomp.stackexchange.com/questions/3271/understanding-the-wolfe-conditions-for-an-inexact-line-search)
- [Gradient Descent (Video - StatQuest)](https://www.youtube.com/watch?v=sDv4f4s2SB8)
- [Gradient Descent with Optimal Step (Video)](https://www.youtube.com/watch?v=nqYDAmmtkk4)
- [Conjugate Gradient Method (Video)](https://www.youtube.com/watch?v=eAYohMUpPMA)
- [Gradient Descent Methods Article](https://towardsdatascience.com/improve-your-gradient-descent-the-epic-quest-for-the-optimal-stride-4711dc6f5dba/)

# Notes
## Gradient Descent
- Algorithms are <mark style="background: #FFB86CA6;">iterative building of a sequence of points</mark> $\{v_0, ... v_k\}, k \in \mathbb N$ where $v_k \underset{k\to \infty}{\to} u$ with $u$ as the minimum of the cost function, $J$
- Goal in each sequence is to take a step closer and closer to $u$: $J(v_{k + 1}) < J(v_k)$
	- $v_{k+1} + d_k$ with $d_k$ as the update term that we are trying to find such that $d_k = (v_{k+1} - v_k)$
- The [[Taylor Series|Taylor expansion]] of degree 1 determines the update $d_k$
	- $J(v_{k+1}) = J(v_k + d_k) = J(v_k) + (J'(v_k), d_k)$
	- We take the current value plus the [[Optimization Basics & Problem Statement|Gâteaux derivative]] in direction $d_k$
- We want $d_k$ to be as negative as possible
	- <mark style="background: #FFB86CA6;">So, we should use the opposite of the gradient as it will be the MOST negative direction</mark>
- And we want to add a scalar step $(\rho > 0, \rho \in \mathbb R)$ to this direction thus giving
	- $d_k = \rho \nabla J(v_k)$ with $\rho$ as the step
- Ultimately, $v_{k+1} = v_k - \rho \nabla J(v_k), \rho > 0$ for gradient descent
- This scalar step must be small otherwise the ignored terms in the Taylor series could be positive
	- The step size given that $J$ is differentiable, alpha-convex with $\nabla J$ Lipschitz-continuous (w/ a Lipschitz constant, $M$), then the algorithm will converge if the step size is $0 < \rho < \frac{2\alpha}{M^2}$ and will find the unique minimum of $J$
- Example in R
	- Cost Function: $J(X) = \frac{1}{2}||X\beta-y||^2$ - <mark style="background: #FFB86CA6;">This is the linear model</mark>
	- Gradient: $\nabla J(X) =X^T(X\beta-y)$
	- Hessian: $H(\beta) = \nabla^2 J(\beta) = X^TX$
```r
# Cost Function - Assumes X and y are the inputs as a matrix and vector in globals
J <- function(beta) {
  cost <- 0.5*t(X%*%beta-y)%*%(X%*%beta-y)
  return(cost)
}

# gradient function
gradJ <- function(beta){
  grad <- t(X)%*%(X%*%beta-y)
  return(grad)
}

# Hessian function
grad2J <- function(beta){
  H <- t(X)%*%X
  return(H)
}
```

```r
# --------- Gradient Algorithm with Fixed Step ---------
# step
rho <- 0.01
# number of iterations
niter <- 500
# store iterates and the corresponding cost
solution <- matrix(,ncol=m,nrow=(niter+1))
cost <- matrix(,ncol=1,nrow=(niter+1))
# initialize
solution[1,] <- rep(0,m)
cost[1] <- J(solution[1,])
# iteration loop
for (k in 1:niter) {
  solution[k+1,] <- solution[k,]-rho*gradJ(solution[k,])
  cost[k+1] <- J(solution[k+1,])
}
```
## Stopping Criteria (Wolfe Conditions)
- Max number of iterations
- $\frac{J(v_k)}{J(v_0)} < \epsilon$: The cost function has been reduced by at least a set amount from the starting value
- $\frac{||\nabla J(v_k)||}{||\nabla J(v_0)||} \lt \epsilon$ OR $\frac{||v_{k+1} - v_k||}{||v_k||} \lt \epsilon$
	- small enough gradient relative to the start OR small enough step size
## Gradient Descent with Optimal Step
- Same as gradient descent algorithm but with an upgrade. The step $\rho$ changes at each iteration
	- $\beta_{k+1} = \beta_k - \rho_{k}\nabla J(\beta_k)$
- This algorithm performs an <mark style="background: #FFB86CA6;">inner optimization</mark> which finds the best $\rho \in \mathbb R$ to minimize along a half-line: $J(\beta_k - \rho \nabla J(\beta_k))$ with respect to $\rho$
	- This inner optimization occurs in dimension 1
	- It also occurs on an open set and therefore can find the solution using [[Optimality Conditions|Euler's equation]]
		- The best step $\rho_k$ is such that $f'(\rho_k) = 0$ for $f: \mathbb R \to \mathbb R$ as $\rho \to J(\beta_k - \rho \nabla J(\beta_k))$
		- 
- The optimal step algorithm performs a line search which <mark style="background: #FFB86CA6;">always converges</mark> with no conditions on $\rho$
- In the quadratic case,
	- $\rho_k = \frac{||\nabla J(\beta_k)||^2}{<(H\nabla J(\beta_k)), \nabla J(\beta_k)>}$
- Example in R (same example as above)
	- Solve: $\beta_{k+1}$
```r
# number of iterations
niter <- 200
# store iterates and the corresponding cost
solution2 <- matrix(,ncol=m,nrow=(niter+1))
cost2 <- matrix(,ncol=1,nrow=(niter+1))
# initialize
solution2[1,] <- rep(0,m)
cost2[1] <- J(solution2[1,])
# "H" matrix, which is actually the Hessian matrix
H <- grad2J(solution2[1,])
# iteration loop
for (k in 1:niter) {
  # gradient
  wk <- gradJ(solution2[k,])
  # optimal step - 
  rho_k <- (t(wk)%*%wk)/(t(H%*%wk)%*%wk)
  # note that the output could be a 1x1 matrix but not a number...
  # update
  solution2[k+1,] <- solution2[k,]-rho_k[1,1]*wk
  cost2[k+1] <- J(solution2[k+1,])
}
```
## Conjugate Gradient Method
- Store previous gradients to find a better direction to go
	- $\beta_0$
	- $\beta_1 = \beta_0 - \rho_0 \nabla J(\beta_0)$
	- $\beta_2 = \beta_1 - \rho_{1,1}\nabla J(\beta_1)-\rho_{1,0}\nabla J(\beta_0)$
	- We have two weights ($\rho_{1,1}, \rho_{1,0}$) and we want to find the <mark style="background: #FFB86CA6;">best linear combination of these two weights</mark>
	- This best linear combination does not change from iteration to iteration
	 ![[Pasted image 20250209122845.png]]
- New residuals are [[Vectors|orthogonal]] to all previous residuals/search directions
	- This helps us avoid redundancy
	- $\nabla J(\beta_{k+1}) \perp \nabla J(\beta_k)$ AND all previous gradients
- Once you get to the $n+1$ vector, you already have a basis, so the next vector must be the 0 vector, and thus you have to have the minimum
- In the quadratic case
	- $\beta_{k+1} = \beta_k - \rho_kd_k$ with $\rho_k = \frac{<w_k, d_k>}{<A d_k, d_k>}$
	- $d_{k+1} = w_{k+1} - \sigma_k d_k$ with $\sigma_k = \frac{<w_{k+1}, Ad_k>}{<Ad_k, d_k>}$
	- These formulas are the same as the [[Vectors|Gram-Schmidt process]]
- Example in R
```R
niter <- 15
# store iterates and the corresponding cost
solution3 <- matrix(,ncol=m,nrow=(niter+1))
cost3 <- matrix(,ncol=1,nrow=(niter+1))
# store direction
direction3 <- matrix(,ncol=m,nrow=(niter+1))
# initialize
solution3[1,] <- rep(0,m)
cost3[1] <- J(solution3[1,])
direction3[1,] <- gradJ(solution3[1,])
# 1st gradient
wk <- direction3[1,]
# 1st direction
dk <- wk
# "A" matrix, which is actually the Hessian matrix
A <- grad2J(beta0)
# iteration loop
for (k in 1:niter) {
  # optimal step
  rhok <- (t(wk)%*%dk)/(t(A%*%dk)%*%dk) # issue: 1x1 matrix but not a number...
  # update the solution and cost
  solution3[k+1,] <- solution3[k,]-rhok[1,1]*dk
  cost3[k+1] <- J(solution3[k+1,])
  # update the gradient
  wk <- gradJ(solution3[k+1,])
  # optimal step for the direction
  sigmak <- (t(wk)%*%(A%*%dk))/(t(A%*%dk)%*%dk)
  # update the direction
  direction3[k+1,] <- wk-sigmak[1,1]*dk
  dk = direction3[k+1,]
}
```
## The Constrained Case - Gradient Descent with Projection
- Need to make the projection at each step of the iteration
	- Take the point that is not allowed and project it onto the set which is allowed
		- Permissible so long as $K$ is [[Convexity and Convex Optimization|closed and convex]]
	- This projection is applied to each condition independently
- Example in R: all beta values should be positive
```R
# step
rho <- 0.01
# number of iterations
niter <- 500
# store iterates and the corresponding cost
solution4 <- matrix(,ncol=m,nrow=(niter+1))
cost4 <- matrix(,ncol=1,nrow=(niter+1))
# initialize
solution4[1,] <- rep(0,m)
cost4[1] <- J(solution4[1,])
# iteration loop
for (k in 1:niter) {
  solution4[k+1,] <- pmax(solution4[k,]-rho*gradJ(solution4[k,]),0)
  cost4[k+1] <- J(solution4[k+1,])
}
```