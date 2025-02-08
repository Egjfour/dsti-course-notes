|         Course Name         |   Topic   |  Professor   |      Date       | Tags |
| :-------------------------: | :-------: | :----------: | :-------------: | :--: |
| **Continuous Optimization** | Convexity | Jacques Blum | 21 janvier 2025 |      |

[Class Video Link 1](https://learn.dsti.institute/mod/url/view.php?id=22609)

# Summary
*Convexity is a critical topic in optimization because convex functions allow for much simpler and exact methods of solving. Convexity of a set means that there are no two points in the set for which the chord between the points goes outside the set. Convexity of a function is different and comes in 3 forms which are in increasing order of strength: convexity, strict convexity, and alpha convexity. We can use the second-order Gâteaux derivative to identify what level (if any) of convexity a given function displays.*

# Key Takeaways
1. Alpha convexity implies strict convexity which implies convexity
2. Convexity means that the graph of the function is above its tangent
3. If the second derivative is 0 at any point, it is not alpha convex
4. The alpha value is the minimum of the [[Eigenvalues and Eigenvectors|eigenvalues]] of $A^TA$
5. If $J: K \to \mathbb R$ is convex, then every [[Optimization Basics & Problem Statement|local minimum]] of $J$ is global as well
6. A convex function MUST be defined on a convex set/subset

# Definitions
- Convex Subset: A set is convex if the chord between two points within the set is also completely within the set
	- Example of a non-convex set: a heart-shaped subset in $\mathbb R^2$
- Convex Function: $J((1 - \theta)u + \theta v) \le (1 - \theta)J(u) + \theta J(v)$
	- The chord between two points of a function is completely above or equal to the function

# Additional Resources
- [Convexity PDF (Stanford)](https://ai.stanford.edu/~gwthomas/notes/convexity.pdf)

# Notes
## Convexity
- Sets
	- A set, $K$, is convex if the chord between any two points within the set is entirely within the set as well
	- There can be no holes, bulging points, or disjointedness
	- ![[Pasted image 20250207092103.png]]
- Functions
	- $J:K\to \mathbb R \textrm{ is convex iff }$ $J((1 - \theta)u + \theta v) \le (1 - \theta)J(u) + \theta J(v)$
		- $\forall \theta \in [0, 1], \forall u, v \in K$
	- In other words, if you pick any two points on the graph of the function and draw a straight line (chord) between them, the graph of the function will lie below or on this line segment
		- $(1 - \theta)u + \theta v$ is a point on the line segment connecting $u$ and $v$
	- The inequality shows that $J$ is convex because it <mark style="background: #FFB86CA6;">ensures that the function's graph does not "bulge" above the chord connecting any two points</mark>
## Strict and Alpha-Convexity
- <mark style="background: #FFB86CA6;">Applies only to functions. Sets cannot be strictly or alpha-convex</mark>
- Strict convexity
	- Implies the same inequality condition as the convex case, but requires that the function be entirely below the chord
	- $J((1 - \theta)u + \theta v) \lt (1 - \theta)J(u) + \theta J(v)$
	- Excludes affine functions
- Alpha convexity
	- We can think of this as stating that there is a "parabola in-between the graph and the chord"
		- Creates a lower bound on how much the function must lie below the chord
	- From the convexity formula, we subtract out the square [[Vectors|norm]] of the difference between points $v \textrm{ and } u$ multiplied by $\frac{\alpha}{2}$ 
		- $J((1 - \theta)u + \theta v) \le (1-\theta)J(u) + \theta J(v) - \frac{\alpha}{2}||u-v||^2$
			- $\forall \theta \in [0,1], \hspace{1.5mm} \forall u.v \in K, \hspace{1.5mm} \alpha \gt 0$
	- This implies strict convexity because the $\frac{\alpha}{2}||u-v||^2$ is always positive, so $J((1 - \theta)u + \theta v)$ must be strictly less than $(1-\theta)J(u) + \theta J(v)$
- Example: strictly convex but not alpha-convex
	- Let $J: \mathbb R \to \mathbb R; \hspace{3mm}J(x) = x^4$
		- In this case, the hessian is $12x^2$ which is $\gt 0$ for all $x \ne 0$ which demonstrates strict convexity
		- However, this curvature has no lower bound... as $x \to 0$, $J''(x) \to 0$, so there is no fixed $\alpha \gt 0$ that satisfies the alpha-convexity condition
## Examples (Functions)
![[Pasted image 20250207090209.png]]
## Convexity Conditions Using the [[Optimization Basics & Problem Statement|Gâteaux Derivative]]
- If $J: V \to \mathbb R$ is Gâteaux derivable on $\mathbb R$, then:
	- $J$ is convex in $V$ $\iff$ $J(v) \ge J(u) + (J'(u), v-u)$
	- $J$ is strictly convex in $V$ $\iff$ $J(v) \gt J(u) + (J'(u), v - u)$
	- $J$ is alpha convex in $V$ $\iff$ $J(v) \ge J(u) + (J'(u), v - u) + \frac{\alpha}{2}||v-u||2$
- We also get the following
	- $J$ is convex$\textrm { iff } J'$ is a <mark style="background: #FFB86CA6;">monotone operator</mark>
		- $(J'(u) - J'(v), u-v) \ge 0, \forall u, v$
		- When $u \gt v, \textrm{ then } J'(u) > J'(v)$
		- Strictly convex $\textrm{iff }(J'(u) - J'(v), u-v) \gt 0, \forall u, v$
			- Strict inequality sign
		- Alpha convex $\textrm{iff }(J'(u) - J'(v), u-v) \ge \alpha ||u - v||^2, \forall v,u \in V$
			- <mark style="background: #FFB86CA6;">The rate of increase is at least (lower bounded) alpha</mark>
- Using second-order Gâteaux derivatives - The Hessian: $J''(u) = \mathcal H$
	- $J$ is convex $\textrm{iff } (J''(u); w, w) \ge 0, \hspace{1.5mm} \forall w \in V$
	- $J$ is alpha convex $\textrm{iff } (J''(u); w, w) \ge \alpha||w||^2, \hspace{1.5mm} \forall w \in V$
		- Second derivative is lower bounded by alpha times the square norm of w
	- $(J''(u); w, w) \gt 0, \hspace{1.5mm} \forall c \in V$ is a sufficient condition for strict convexity but is not necessary