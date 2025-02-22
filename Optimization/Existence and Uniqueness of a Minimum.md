|         Course Name         |     Topic      |  Professor   |      Date       | Tags |
| :-------------------------: | :------------: | :----------: | :-------------: | :--: |
| **Continuous Optimization** | Proving Minima | Jacques Blum | 21 janvier 2025 |      |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/johnny_najjar_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fjohnny%5Fnajjar%5Fdsti%5Finstitute%2FDocuments%2FRecordings%281%29%2FA24%20%2D%20Common%20Link%20%2D%20DS%2DDE%2DDA%2D20250121%5F095012%2DMeeting%20Recording%201%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E659d14cc%2Dda79%2D4441%2D8a42%2D86d3d4673ba0)

# Summary
*The Weierstrass Theorem and its corollary are what define the existence of a minimum. Ultimately, the key condition is that the cost function must go to infinity as the absolute value of the inputs goes to infinity. Uniqueness can be determined simply by looking at the domain of the function (closed and convex) and the [[Convexity|convexity]] of the cost function (strictly convex and continuous).*

# Key Takeaways
1. The corollary of the Weierstrass Theorem allows us to prove the existence of a minimum
2. Convexity is the condition which allows us to demonstrate the uniqueness of a minimum
3. Existence of a minimum requires a continuous function $J$ on a closed, non-empty set with either $J(v) \to \infty \textrm{ as } ||v|| \to \infty$ or $K \subset V$ bounded or $J$ is alpha convex

# Definitions
- Closed Set: A set which includes its boundary
	- Constraints that are defined with a large inequality ($\le,\ge$)
- Bounded Set: A set which does not go to infinity

# Additional Resources
- [Weierstrass Theorem](https://www.sciencedirect.com/topics/mathematics/weierstrass-theorem)

# Notes
## Weierstrass Theorem - Existence
- Any continuous function on a closed, bounded set of $\mathbb R^n$ is upper and lower bounded and reaches its bounds
	- Therefore, there is a value, $A$, such that, $f(A) = inf\hspace{1mm}f(x), x\in K$ and there is a value, $B$ such that $f(A) = max\hspace{1mm}f(x), x\in K$
- Corollary
	- Let $K$ be a closed, non-empty set of $\mathbb R^n$ and $J$ be a continuous function on $K$ such that $J(v) \to \infty$ when $||v|| \to \infty$
	- If true, then $\exists$ at least 1 point of $K$ where $J$ reaches its minimum on $K$
	- In other words, so long as the [[Optimization Basics & Problem Statement|cost function]] goes to infinity as the inputs go to infinity, then there is at least one point within the subset where we reach the minimum
## Uniqueness
- If $V = \mathbb R^n$ and $K$ is a [[Convexity|convex subset]] of $V$
- If $J$ is <mark style="background: #FFB86CA6;">strictly convex, then there exists at most 1 minimum</mark>
- So, given a strictly convex function, if $J'(u) = 0$, then $u$ is a global minimum of $J$ on $K$
	- If the [[Optimality Conditions|first-order condition]] is met, then we have the global minimum of the function
