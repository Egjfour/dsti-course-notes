|         Course Name         |               Topic               |  Professor   |      Date       |   Tags    |
| :-------------------------: | :-------------------------------: | :----------: | :-------------: | :-------: |
| **Continuous Optimization** | First and Second-Order Conditions | Jacques Blum | 22 janvier 2025 | #Calculus |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/johnny_najjar_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fjohnny%5Fnajjar%5Fdsti%5Finstitute%2FDocuments%2FRecordings%281%29%2FA24%20%2D%20Common%20Link%20%2D%20DS%2DDE%2DDA%2D20250122%5F095201%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Ef8ed1370%2Dac7e%2D44da%2D9bb4%2D57dfec1549a3)

# Summary
*The first and second order conditions are what prove that a given point is a minimum of a function. These conditions rely on Euler's equation (unconstrained case) and inequality (constrained case) and then look at the first and second-order Gâteaux derivative to identify a minimum point. In the convex case, the first-order condition becomes sufficient and with a strictly convex function, we also know the solution is unique and is therefore a global minimum as well.*

# Key Takeaways
1. When $\Omega$ is the full domain ($\Omega = \mathbb R^2$), we are finding the optimum with no constraints
2. Euler's equation is used when we are operating on an open subset (or no constraints) and Euler's inequality is used when we are operating on a closed, convex subset
3. Euler's equation states that the gradient must be the zero vector if we are at a local extremum
4. Euler's equation/inequality are necessary conditions in the general case and are necessary and sufficient conditions in the [[Convexity and Convex Optimization|convex]] case
5. It is necessary that the hessian matrix is positive at a local minimum
# Definitions
- First-Order Condition: A condition which involves the gradient of a function
- Vectorial Subspace: Any subset $V$ of $\mathbb R^n$ which is non-empty and is closed under addition and scalar multiplication
	- This means that the origin must be within this subspace
- Critical Point: Any point in the domain of the cost function where the gradient is the zero vector
- Strict Local Minimum: $J$ has a strict local minimum at point $u$ if there exists a neighborhood, $\mathcal N(u)$ such that $J(u) < J(v), \forall v \in \mathcal N(u) - \{u\}$
	- This is the same condition that existed for a [[Optimization Basics & Problem Statement|local minimum]] with the inequality no longer including the equality case
- Coercive: All the eigenvalues of the Hessian matrix are strictly positive (> 0)
	- $\exists \alpha \gt 0 \textrm{ s.t. } (J''(u); w,w) \ge \alpha||w||^2$

# Additional Resources
- [Subspaces](https://textbooks.math.gatech.edu/ila/subspaces.html)

# Notes
## First-Order Conditions (Necessary but not Sufficient)
- Proposition 1
	- Applies to unconstrained optimization problems where the function is differentiable
	- Let $V \in \mathbb R^n \textrm{ and } J: \Omega \to \mathbb R$ an <mark style="background: #FFB86CA6;">open subset</mark> of $V$ and assume that $J$ has a local extremum at point $u \in \Omega$ and that $J$ is [[Optimization Basics & Problem Statement|Gâteaux derivable]] at point $u$
		- Then $J'(u) = 0$ which is known as Euler's equation
		- The gradient must be the zero vector
	- It is essential that $\Omega$ is an open subset. This means that it can be the full domain $(\mathbb R^n)$
		- Full domain = no constraints
	- Proof is that there is a bowl centered on $u$ in $\Omega$ which represents a neighborhood around $u$ and all points in that neighborhood have $J(u + \theta v) \ge J(u)$
- Proposition 2
	- Applies to constrained optimization problems where the feasible set is convex
	- Let $V = \mathbb R^n$ and $K$ be a [[Convexity and Convex Optimization|convex subset]] of $V$
	- If $J$ has a local minimum on $K$ at point $u$, the $(J'(u), v-u) \ge 0, \forall v\in k$
		- Known as Euler's Inequality
		- Ensures that moving from point $u$ to another point $v \in K$ does not decrease the value of $J$
	- This does NOT require that the subset be open like proposition 1
## The Convex Case (First-Order Conditions)
- Given that $V = \mathbb R^n$ and $K$ is a convex subset of $V$
- If $J: K \to \mathbb R$ is convex, any local minimum is also global
- If $J:K\to \mathbb R$ is strictly convex, there exists at most 1 minimum
	- This proves [[Existence and Uniqueness of a Minimum|uniqueness of a solution]]
- Let $J$ be convex and Gâteaux derivable on $K$, If $J'(u) = 0$, then $u$ is a <mark style="background: #FFB86CA6;">global minimum</mark>
	- Unbounded situation (Euler's Equation)
- If $J: K \to \mathbb R$ is convex, Gâteaux derivable, and if $(J'(u), v-u) \ge 0, \forall v \in K$,
	- then $u$ is a global minimum on $K$
	- Euler's inequality
## Second-Order Conditions
- Proposition 3 (<mark style="background: #FFB86CA6;">necessary for a local minimum</mark>)
	- Let $\Omega$ be an open subset of $V$ and $J: \Omega \to \mathbb R$ be a function derivable on $\Omega$ and twice derivable at point $u \in \Omega$
	- If $J$ has a local minimum at point $u \in \Omega$, then $(J''(u); w, w)\ge 0, \forall w \in V$
		- <mark style="background: #FFB86CA6;">All the eigenvalues of the Hessian are positive</mark>
- Proposition 4 (sufficient condition for a strict local minimum)
	- Let $\Omega$ be an open subset of $V$ and $J$, a derivable function such that $J'(u) = 0$
		- *Euler's equation is satisfied*
	- If $J$ is twice Gâteaux derivable and if $\mathcal H$ is coercive (all eigenvalues are *strictly positive*)
	- Then $J$ has a strict local minimum at point $u$
- If the trace and [[Matrix Determinant|determinant]] of the Hessian Matrix are both positive, then all [[Eigenvalues and Eigenvectors|eigenvalues]] are positive
	- Applies only to 2x2 matrices
- Proposition 5 (<mark style="background: #FFB86CA6;">sufficient for a local minimum</mark>)
	- Let $\Omega$ be an open subset of $V$ and $J: \Omega \to \mathbb R$ be a function twice derivable on $\Omega$ with $J'(u) = 0$
	- and if there exists a neighborhood around $u$, $\mathcal N(u)$ such that $(J''(v); w,w) \ge 0, \forall v \in \mathcal N(u), \forall w \in V$
	- Then, $J$ has a local minimum at $u$
	- Difference from proposition 3 is that this does not assume $u$ to be a minimum already