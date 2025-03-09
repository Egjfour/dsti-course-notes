|         Course Name         |                      Topic                      |  Professor   |      Date       |   Tags    |
| :-------------------------: | :---------------------------------------------: | :----------: | :-------------: | :-------: |
| **Continuous Optimization** | Constraints, Saddle Points, and Problem Solving | Jacques Blum | 24 janvier 2025 | #Calculus |

[Class Video Link](URL)

# Summary
*When optimizing a function with constraints, the Kuhn-Tucker theorem is essential for identifying the candidate points for a minimum. With this theorem, we can write the Lagrange equation which combines the constraints and cost function. The solution will always be where the derivative of this function is equal to 0. The additional conditions of the KKT are based on whether we have equality or inequality constraints. In the convex case, the KKT conditions are both necessary and sufficient. This minimum point is also, in many cases, a saddle point where we have a maximum with respect to the Lagrange multipliers and a minimum with respect to the input variables.*

# Key Takeaways
1. The constraints must be linearly independent. Otherwise, they are proportional and represent the same constraint
2. For minimization, positive constraint conditions (greater than) must be converted to negative
3. If all constraints are affine, then they are all qualified
4. For a saddle point, the location of the saddle point is the location of the solution
5. Maxima and Minima will be found at solutions to $\nabla J(u) = \lambda \nabla g(u)$

# Definitions
- Regularity of Constraints: The gradient vectors of the constraint functions are [[Vectors|linearly independent]]
- Qualified Constraint: There exists a direction from the boundary of the constraint which goes back inside the constraint (a re-entrant condition)
- Saddle Point: A saddle point is a point in the domain of a function where the gradient is zero, but it is not a local minimum or maximum. Instead, it is a point where the function has a minimum in one direction and a maximum in another.

# Additional Resources
- [Lagrange Multipliers | Geometric Meaning & Full Example Video](https://www.youtube.com/watch?v=8mjcnxGMwFo)
- [Constrained Optimization with Lagrange Multipliers Video](https://www.youtube.com/watch?v=nUfYR5FBGZc)
- [Saddle Points Video](https://www.youtube.com/watch?v=8aAU4r_pUUU)
- [KKT Conditions and Interior Point Method for Convex Optimization Video](https://www.youtube.com/watch?v=uh1Dk68cfWs)

# Notes
## Equality Constraints
- Given a problem, $\mathscr P$ with a minimum at $J(u)$, $\textrm{inf } \underset{v\in K}{J(v)}$ where $K = \{v \in V \textrm{ s.t. }F(v) = 0\}$
	- Produced $m$ equality constraints
- If both $J$ and $F_i$ are derivable at point $u$ and $J'$ and $F_i'$ are continuous and the $m$ vectors $\{F_i'(u), ..., F_m'(u)\}$ are [[Vectors|linearly independent]],
- Then $\exists \hspace{1.5mm} m$ Lagrange multipliers $(\lambda_1, ..., \lambda_m)$ such that $J'(u) + \underset{i=1}{\overset{m}{\sum}}\lambda_iF'_i(u) = 0$
	- <mark style="background: #FFB86CA6;">This implies that the lambda values are all unique</mark>
- We can express all of this as the Lagrangian function
	- $\mathcal L(v,\mu) = J(v) + \overset{m}{\underset{i=1}{\sum}}\mu_iF_i(v) - J(v) + <\mu, F(v)>$
	- Thus
		- $\frac{\partial \mathcal L}{\partial \mu} = F(v)$
		- $\frac{\partial \mathcal L}{\partial v} = J'(v) + <\mu, F'(v)>$
	- Taken at the point $u$ with the Lagrange multipliers
		- $\frac{\partial \mathcal L}{\partial v}(u, \lambda) = J'(u) + \overset{m}{\underset{i=1}{\sum}}\lambda_iF_i'(u) = 0$
		- AND $\frac{\partial \mathcal L}{\partial \mu}(u, \lambda) = F(u) = 0$
	- Therefore, $(u, \lambda)$ is a critical point of $\mathcal L$
- Use Lagrange multipliers to convert constrained problems into unconstrained ones by forming the Lagrangian. <mark style="background: #FFB86CA6;">The gradients of the constraints must be linearly independent (regular).</mark>
- CONDITION: If the constraints are regular, then the candidate points are where $\mathcal L' = 0$ which also satisfies the constraints
- If the gradient of the cost function and the constraints are all affine, then <mark style="background: #FFB86CA6;">the solution is a system of linear equations aka linear programming</mark>
## Inequality Constraints
- $K = \{v \in V \textrm{ s.t. }F_i(v) \le 0, 1 \le i \le m\}$ with $J$ and $F_i$ derivable at point $u$ which is a point as a solution of $\mathscr P$: $\underset{v \in K}{\textrm{inf}}J(v)$
	- $I(u)$ is defined as the set of active constraints at point $u; u\in K$
- Theorem: If $K = \{v = \in V \textrm{ s.t. } F(v) \le 0\}$ and if $J$ and $F_i$ are derivable at point $u$ and the constraints are qualified, then if $u$ is a local minimum at point $u$, there exists $m$ Lagrange multipliers (positive or zero), $p_1, ..., p_m$ such that
	- $J'(u) + \underset{i=1}{\overset{m}{\sum}}p_iF_i'(u) = 0$
	- AND $p_i \ge 0$
	- AND $p_i = 0$ if $F_i(u) = 0; \forall i \in \{1,...,m\}$
- We can rewrite this as $p_i \ge 0; i = 1,...,m$ and $<p, F(u)> = 0$
	- Because $<p, F(u)> = \overset{m}{\underset{i=m}{\sum}}p_iF_i(u)$
- Use KKT Conditions, which include non-negativity of the multipliers and complementary slackness. These conditions generalize the method of Lagrange multipliers to handle inequality constraints
## Saddle Points
- Definition
	- Let $V = \mathbb R^n$ and $Q = \mathbb R^m$, we say that $(u, p) \in V*Q$ is a saddle point of $\mathcal L$ on $u*p$ where $u$ is a subset of $V$ and $p$ is a subset of $Q$ **IF**
		- $\mathcal L(\mu, q) \le \mathcal L(u,p) \le \mathcal L(v,q)$
		- $\mathcal L(u, p) = \underset{v\in U}{\textrm{inf}}\mathcal L(v,p) = \underset{q \in P}{\textrm{sup}}\mathcal L(\mu, q)$
- Theorem: Min-Max Property
	- If $(u,p)$ is a saddle point of $\mathcal L$ on $U * P$, then $\mathcal L(u,p)$ is the $\underset{v\in U}{\textrm{inf}}\hspace{1.5mm}\underset{q\in P}{\textrm{sup}}\hspace{1mm}\mathcal L(v,q)$ and $\underset{q\in P}{\textrm{sup}}\hspace{1.5mm}\underset{v\in U}{\textrm{inf}}\hspace{1mm}\mathcal L(v,q)$
	- <mark style="background: #FFB86CA6;">Minimize the cost function and simultaneously maximize the constraint with respect to the Lagrange multipliers</mark>
- In unconstrained optimization, saddle points are generally not solutions to minimization problems because they do not represent local minima. However, in constrained optimization, saddle points of the Lagrangian function can indeed correspond to solutions of the original constrained problem.
### Understanding Saddle Points in Optimization (Mistral AI)

6. **Constrained Optimization**:
    
    - In optimization, you often want to minimize (or maximize) a function subject to certain constraints. For example, you might want to minimize a cost function $J(v)$ while ensuring that some conditions $Fi(v)=0$ or $Fi(v)\le0$ are met.
7. **Lagrange Multipliers**:
    
    - To handle these constraints, we introduce Lagrange multipliers. These are additional variables that help incorporate the constraints into the optimization problem. We form a new function called the Lagrangian, which combines the original function $J(v)$ with the constraints $F_i(v)$.
8. **Lagrangian Function**:
    
    - The Lagrangian function $\mathcal L(v,\mu)$ is defined as: $\mathcal L(v,\mu)=J(v)+\underset{i=1}{\overset{m}{\sum}}\mu_iF_i(v)$
    - Here, $\mu_i$​ are the Lagrange multipliers, and $F_i(v)$ are the constraint functions.
9. **Saddle Points**:
    
    - A saddle point of the Lagrangian is a point $(u,\lambda)$ where the Lagrangian has special properties:
        - It is a minimum with respect to the original variables $v$.
        - It is a maximum with respect to the Lagrange multipliers $\mu$.
    - This means that at the saddle point, small changes in $v$ increase the Lagrangian, while small changes in $\mu$ decrease it.
10. **Why Saddle Points Matter**:
    
    - The saddle point of the Lagrangian is important because it provides a solution to the original constrained optimization problem. At this point, the original function $J(v)$ is minimized, and all the constraints $F_i(v)$ are satisfied.
    - The apparent contradiction (that moving in one direction increases the Lagrangian while in another it decreases) arises because the Lagrangian incorporates both the objective function and the constraints. The saddle point balances these two aspects.
#### Intuitive Explanation

- **Balancing Act**: Think of the saddle point as a balancing act between minimizing the objective function and satisfying the constraints. The Lagrange multipliers act as "penalties" that ensure the constraints are met.
- **Optimality**: At the saddle point, you've found the best possible value of the objective function while respecting all the constraints. It's like finding the lowest point in a valley (minimizing the objective function) while making sure you stay within certain boundaries (satisfying the constraints).

In summary, the saddle point of the Lagrangian is crucial because it signifies that you've optimized your objective function as much as possible given the constraints. The concept of moving in different directions (minimizing and maximizing) relates to how the Lagrangian balances the objective function and the constraints.
## Convex Case for Inequality Constraints (KKT)
- Kuhn-Tucker Theorem
	- Suppose $J$ and $F_i$ are convex and $K = \{v \in V \textrm{ s.t. } F(v) \le 0\}$
		- If $J = \infty$ at $\infty$, then $\exists u \in K$ as a solution of $(\mathscr P)$
	- Also suppose that $J$ and $F_i$ are convex continuous on $V$ and differentiable on $K$
	- and that $\exists \hspace{1.5mm} \bar v \in V \textrm{ s.t. } \forall i \in \{1, ..., m\}$ either $F_i(\bar v) < 0 \textrm{ or } F_i(\bar v) = 0$ with $F_i$ affine
	- Then, $u$ is a solution of $(\mathscr P)$ if and only if $\exists \hspace{1.5mm} u \in K \textrm{ s.t. } (u,p)$ is a saddle point of $\mathcal L$ on $V \textrm{x} \mathbb R_m^+$
		- $F(u) \le 0$ <mark style="background: #FFB86CA6;">OR</mark> $p \ge 0$: Either the Lagrange multipliers or the constraints are 0
		- $<p, F(u)> = 0$: The product of the Lagrange multipliers and the constraints is 0
		- $J'(u) + \underset{i=1}{\overset{m}{\sum}}p_iF_i'(u)=0$: The derivative of the Lagrangian $(\mathcal L)$ is 0
- When a function is [[Convexity|strictly convex]] on a [[Convexity|closed, convex set]], this relation becomes necessary AND sufficient
## Equality and Inequality Constraints
- Need to combine the hypotheses for the equality and inequality constraints
	- $\exists \bar w \in V \textrm{ s.t. } <h_i'(u), \bar w> = 0, \forall i \in \{1,...,m\}$
		- There is a location, $\bar w$, where the gradient of the equality constraints is zero
	- $\exists \bar w \in V \textrm{ s.t. } <g_j'(u), \bar w> \hspace{1mm} \lt 0, \forall j \in \{1,...,p\}$ <mark style="background: #FFB86CA6;">OR</mark> $<g_j'(u), \bar w> = 0$ with $g_j$ affine
		- The gradient of the inequality constraints is either negative at point $\bar w$ (<mark style="background: #FFB86CA6;">or 0 if the constraint is affine</mark>)
- If the hypotheses are met, then there exists Lagrange multipliers ($p$ and $\lambda$) such that
	- $\mathcal L'(u) = J'(u) + \underset{i=1}{\overset{m}{\sum}}\lambda_ih_i'(u) + \underset{j=1}{\overset{p}{\sum}}p_jg_j'(u) = 0$
	- Inequality
		- $<p, g(u)> = 0$
		- $p_j \ge 0$, $g_j(u) \le 0, \forall j \in \{1,...,q\}$
	- Equality
		- $h_i(u) = 0, \forall i \in \{1,...,m\}$
- If $J$ and $g_j$ are convex and $h_i$ are affine, the  the KKT conditions are necessary and sufficient conditions for which $u$ is a minimum of $J$ on $K$
## Example
- Given the following problem in $\mathbb R^2$: $\underset{x-y \ge -1}{\textrm{min }}x^2 + 2x + xy + y^2 - 4y + 3$
	- The set $K = \{(x,y)/x-y \ge -1\}$ is convex because it is affine and closed because the inequality includes the constraint
	- To determine convexity of the cost function, we need the eigenvalues of the Hessian matrix
		- $J(x,y) = x^2 + 2x + xy + y^2 - 4y + 3$
		- $\nabla J = \begin{pmatrix}2x + y + 2\\2y+x-4 \end{pmatrix}$
		- $\nabla^2 J = \begin{pmatrix}2,1\\1,2 \end{pmatrix}$
		- Since it is a 2x2 matrix the characteristic equation can be defined with the trace and [[Matrix Determinant|determinant]]
			- $|\nabla^2 J| = 2*2 - 1*1 = 3$
			- $tr(\nabla^2 J) = 2+2 = 4$
			- Characteristic Equation: $\lambda^2 - 4\lambda + 3 = 0$
		- Solving for the eigenvalues we get
			- $\frac{-b \pm \sqrt{b^2 - 4ac}}{2a} = \frac{4 \pm \sqrt{16-12}}{2}$
			- $\lambda_1 = 3$ and $\lambda_2 = 1$
		- Since none of the eigenvalues are $<0$, we have convexity. Specifically, we have alpha convexity with $\alpha = 1$ based off the minimum eigenvalue
	- To prove the existence and uniqueness of a minimum we can say that we will have a unique minimum because $J$ is strictly convex and $K$ is closed and convex
	- The KKT conditions for this problem are as follows
		- $\mathcal L'(u) = 0$
			- $\nabla J(u) + \lambda \nabla g(u) = \begin{pmatrix}2x+y+2\\2y+x-4 \end{pmatrix} + p \begin{pmatrix}-1\\1 \end{pmatrix} = \begin{pmatrix}0\\0\end{pmatrix}$
		- $<p, g(u)> \hspace{1mm}= p(-x+y-1) = 0$
		- $p \ge 0$
		- $g(u) \le 0 \implies -x + y - 1 \le 0$
	- <mark style="background: #FFB86CA6;">Solve for the different possible cases</mark> ($p = 0$ and $p \gt 0$)
		- If $p = 0$, then we solve the gradient condition
			- $\begin{pmatrix}2x+y+2\\2y+x-4 \end{pmatrix} = \begin{pmatrix}0\\0\end{pmatrix}$
			- $\left(\begin{array}{cc|c}2 & 1 & -2\\1 & 2 & 4\end{array}\right) = \left(\begin{array}{cc|c}1 & 2 & 4\\2 & 1 & -2\end{array}\right) = \left(\begin{array}{cc|c}1 & 2 & 4\\0 & -3 & -10\end{array}\right)=\left(\begin{array}{cc|c}1 & 2 & 4\\0 & 1 & \frac{10}{3}\end{array}\right) =$
			- $\left(\begin{array}{cc|c}1 & 0 & -\frac{8}{3}\\0 & 1 & \frac{10}{3}\end{array}\right)$, so $x = -\frac{8}{3}$ and $y = \frac{10}{3}$
			- We need to test these values of $x$ and $y$ to ensure they adhere to the constraints
				- $g(-\frac{8}{3}, \frac{10}{3}) = \frac{8}{3} + \frac{10}{3} - 1 = \frac{15}{3} \not \le 0$
				- <mark style="background: #FFB86CA6;">This solution is NOT in the domain</mark>
		- If $p \ne 0$, then we get a 3x3 system of equations because $g(u) = 0$
			- $\begin{pmatrix}2x+y+2-p\\2y+x-4+p\\-x+y-1 \end{pmatrix} = \begin{pmatrix}0\\0\\0\end{pmatrix}$
			- $\left(\begin{array}{ccc|c}2 & 1 & -1 & -2\\1 & 2 & 1 & 4\\-1 & 1 & 0 & 1\end{array}\right) = \left(\begin{array}{ccc|c}2 & 1 & -1 & -2\\-1 & 1 & 0 & 1\\1 & 2 & 1 & 4\end{array}\right) = \left(\begin{array}{ccc|c}1 & \frac{1}{2} & -\frac{1}{2} & -1\\0 & \frac{3}{2} & -\frac{1}{2} & 0\\0 & \frac{3}{2} & \frac{3}{2} & 5\end{array}\right) =$
			- $\left(\begin{array}{ccc|c}1 & \frac{1}{2} & -\frac{1}{2} & -1\\0 & 1 & -\frac{1}{3} & 0\\0 & \frac{3}{2} & \frac{3}{2} & 5\end{array}\right) = \left(\begin{array}{ccc|c}1 & \frac{1}{2} & -\frac{1}{2} & -1\\0 & 1 & -\frac{1}{3} & 0\\0 & 0 & 1 & \frac{5}{2}\end{array}\right) = \left(\begin{array}{ccc|c}1 & \frac{1}{2} & 0 & \frac{1}{4}\\0 & 1 & 0 & \frac{5}{6}\\0 & 0 & 1 & \frac{5}{2}\end{array}\right) =$
			- $\left(\begin{array}{ccc|c}1 & 0 & 0 & -\frac{1}{6}\\0 & 1 & 0 & \frac{5}{6}\\0 & 0 & 1 & \frac{5}{2}\end{array}\right)$, so $x = -\frac{1}{6}, y = \frac{5}{6}$, and $p = \frac{5}{2}$
			- We again need to check the constraint:
				- $g(-\frac{1}{6}, \frac{5}{6}) = \frac{1}{6} + \frac{5}{6} - 1 = 0 \le 0$, so the constraint is satisfied and this is the unique solution
	- Given our solution $(-\frac{1}{6}, \frac{5}{6})$, the minimum value of the cost function $J$ subject to the constraints is $-\frac{1}{12}$