|         Course Name         |         Topic          |  Professor   |      Date       |   Tags    |
| :-------------------------: | :--------------------: | :----------: | :-------------: | :-------: |
| **Continuous Optimization** | Goals and Introduction | Jacques Blum | 20 janvier 2025 | #Calculus |

[Class Video Link](URL)

# Summary
*Optimization is the process of minimizing or maximizing a cost function which maps a multidimensional input to a one-dimensional output in the real number space. This process can also be subject to constraints of which there can be domain, equality, inequality, and functional constraints. A critical aspect to determining if a candidate point is a minimum is to identify and examine the Gâteaux derivative which represents the derivative of the cost function in a specific direction.*

# Key Takeaways
1. The cost function maps from an input vector ($V$) in space $\mathbb R^m$ to the real number space $\mathbb R$
2. As soon as we leave the domain of the constraint, we [[Algorithms|project onto the constraint]]
3. A maximization problem is equal to the minimization of a negative cost function
4. A global minimum is also local, but the reverse is generally false except in the convex case 
5. Any linear form can be represented with a gradient according to the Reisz Theorem
6. If a Fréchet Derivative exists, at point $u$, then the Gâteaux derivative $J'(u)$ also exists and is identical
7. When $v = e_i$ (the canonical basis), the directional derivative is simply the [[Functions and Derivatives of Functions|partial derivative]] at a given point $u$
 
# Definitions
- Cost Function $((J): V \to \mathbb{R})$: The domain in which the variable we want to optimize moves
	- Squared error - we want to minimize the error function
- Active/Saturated Constraint: When the constraint is binding such that for a constraint $G(v), G_j(v) = 0$ meaning that <mark style="background: #FFB86CA6;">we are at the limit of the constraint</mark>
- Inactive Constraint: A constraint that is not relevant because the solution is not at the domain of the constraint $G_j(v) < 0$
	- A non-binding price ceiling
- Local Optimum: A point $u$ is an optimum if there is a neighborhood of points around $u, \mathcal N(u)$ such that $J(u) \le J(v), \forall v \in \mathcal N(u)$

# Additional Resources
- [What is Mathematical Optimization Video](https://www.youtube.com/watch?v=AM6BY4btj-M)
- [Gâteaux Derivative Video](https://www.youtube.com/watch?v=w1Vzjbd5g8g)
- [Geometrical Interpretation of Gateaux and Directional Derivatives]([https://youtu.be/NomUbVmmyro?si=3hIH0aRawodE_RcA](https://youtu.be/NomUbVmmyro?si=3hIH0aRawodE_RcA "https://youtu.be/nomubvmmyro?si=3hih0arawode_rca"))

# Notes
## Explanation/Goal of General Optimization
- Problem ($\mathscr P$) Statement
	- Need either a criterion (economy), a function (math), or a cost function (optimization goal)
	- Example: Minimize costs subject to a minimum level of output
- Cost Function
	- $J: V \to \mathbb R$
	- A cost function maps a vector input space to a single output in the [[Real Numbers, Real Sequences, and Limits|real number]] space
	- Example: Squared error which in vector form is $y = ||Av - b||^2$
- Our goal is to find a point $u$ in $U$ such that $J(u) \le J(v), \forall u \in U$
## Constraints
- Domain Constraints
	- The solution can only exist in a subset ($K$) of the domain of $V$
	- Example: All variables $v$ must be positive (in quadrant I in $\mathbb R^2$)
	- As soon as we leave this domain, we project onto it
- Equality Type Constraints
	- $F(v) = 0$: Our constraint function must take on a specific value (typically rewritten to be zero)
	- $F: V \to \mathbb R^m$
		- i.e., all $v = 0, \textrm{ for } v \in V$
		- This means that there are m constraints
- Inequality Type Constraints
	- $G(v) <= 0 \textrm { with } G: V \to \mathbb R^p$
		- Results in p constraints
	- Does NOT result in an [[Relations of Sets|order relation]] since this is in $\mathbb R^p$
- Functional Equation Constraints (ODE - Ordinary Differential Equation)
	- Solving for the original function given a function for the derivative and other conditions
	- Example: $\frac{dy}{dt} = ay \textrm{ and } y(0) = y_0 \textrm{ so } \underset{a \in \mathbb R}{y(t)} = e^{at}y_0$
	- <mark style="background: #FFB86CA6;">These are frequently used to enforce dynamic constraints such as time- or space-dependent behaviors</mark>
- Active vs Inactive Constraints
	- Active constraints are ones that are actually being used by the problem. For example, if we specify that a certain input must be positive, but the true solution would be negative, then the constraint is active
- Constraint types can be mixed and multiple constraints can be applied to the same problem
## Gâteaux Derivative
- The Gâteaux derivative is a special type of directional derivative that gives an answer at a specific point, $u$ for $J'(u)$, and works for functions that aren't necessarily continuous
- Defined as $\underset{\theta \to 0^+}{lim}\frac{J(u + \theta v) - J(u)}{\theta}$
	- The difference in the cost function as we go from point $u$ in direction $v$ as we scale direction $v$ smaller and smaller
- Conditions for Gâteaux Derivability
	- $(J'(u),v) \textrm{ exists } \forall v \in V$
	- $V \to (J'(u), v)$ is linear continuous
		- $J'(u) = \mathscr L(v, \mathbb R)$
		- <mark style="background: #FFB86CA6;">The derivative is a linear application with respect to V</mark>
- The Gâteux derivative is an expression of [[Functions and Derivatives of Functions|partial derivatives]]
	- If a partial derivative exists a point $u$, then $(J'(u), v) = \overset{n}{\underset{i=1}{\sum}}\frac{\partial J}{\partial v_i}(u)v_i$
	- This means that the Gâteaux derivative is simply a [[Vectors|dot product]] of the [[Function Optimization|gradient vector]], $\nabla J(u)$, and the direction $v$: $<\nabla J(u), v>$
		- The gradient is the transpose of the Gâteaux Derivative: $\nabla J(u) = [J'(u)]^T$
- Second-Order Gâteux Derivative
	- Looks at two points, $v \textrm{ and } w$ to calculate $(J''(u); v, w)$ which represents the second-order directional derivative at point $u$ in the directions $v$ and $w$
	- Defined by $\underset{\theta \to 0^+}{lim}\frac{J'(u + \theta v; w) - (J'(u), w)}{\theta}$
	- If this second-order derivative is bilinear continuous, it is called the [[Function Optimization|hessian]]
## Mean Value Theorem and [[Taylor Series|Taylor's Approximation]]
- Proposition 1:
	- If $J: V \to \mathbb R$ is Gâteaux derivable $\forall u + \theta v \textrm{ for } \theta \in [0, 1], \exists \hspace{1mm} \theta_0 \in ]0, 1[$ such that $J(u + v) = J(u) + (J'(u + \theta_0 v), v)$
	- The first order Taylor Series Approximation holds and the value from a point u in direction v equals the value of the point plus the direction
- Proposition 2:
	- If $J: V \to \mathbb R$ is twice Gâteaux derivable $\forall u + \theta v, \hspace{1.5mm} \theta \in [0, 1], \hspace{1.5mm} \exists \hspace{1.5mm} \theta_0 \in ]0,1[$ such that $J(u + v) = J(u) + (J'(u), v) + \frac{1}{2}(J''(u + \theta_0 v); v, w)$
	- The second order Taylor Series Approximation also holds

