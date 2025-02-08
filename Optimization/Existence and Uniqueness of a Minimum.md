|         Course Name         |     Topic      |  Professor   |      Date       | Tags |
| :-------------------------: | :------------: | :----------: | :-------------: | :--: |
| **Continuous Optimization** | Proving Minima | Jacques Blum | 21 janvier 2025 |      |

[Class Video Link](URL)

# Summary
*A 3-4 sentence description of what was learned in italics*

# Key Takeaways
1. The corollary of the Weierstrass Theorem allows us to prove the existence of a minimum
2. Convexity is the condition which allows us to demonstrate the uniqueness of a minimum

# Definitions
- Closed Set: A set which includes its boundary
	- Constraints that are defined with a large inequality ($\le,\ge$)
- Bounded Set: A set which does not go to infinity

# Additional Resources
- [Weirstrass Theorem](https://www.sciencedirect.com/topics/mathematics/weierstrass-theorem)

# Notes
## Weierstrass Theorem - Existence
- Any continuous function on a closed, bounded set of $\mathbb R^n$ is upper and lower bounded and reaches its bounds
	- Therefore, there is a value, $A$, such that, $f(A) = inf\hspace{1mm}f(x), x\in K$ and there is a value, $B$ such that $f(A) = max\hspace{1mm}f(x), x\in K$
- Corollary
	- Let $K$ be a closed, non-empty set of $\mathbb R^n$ and $J$ be a continuous function on $K$ such that $J(v) \to \infty$ when $||v|| \to \infty$
	- If true, then $\exists$ at least 1 point of $K$ where $J$ reaches its minimum on $K$
	- In other words, so long as the [[Optimization Basics & Problem Statement|cost function]] goes to infinity as the inputs go to infinity, then there is at least one point within the subset where we reach the minimum
## Uniqueness
- If $V = \mathbb R^n$ and $K$ is a [[Convexity and Convex Optimization|convex subset]] of $V$
- If $J$ is <mark style="background: #FFB86CA6;">strictly convex, then there exists at most 1 minimum</mark>
- So, given a strictly convex function, if $J'(u) = 0$, then $u$ is a global minimum of $J$ on $K$
	- If the [[Optimality Conditions|first-order condition]] is met
