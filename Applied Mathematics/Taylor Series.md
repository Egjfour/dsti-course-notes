|   Course Name    |     Topic     |   Professor   |       Date       |   Tags    |
| :--------------: | :-----------: | :-----------: | :--------------: | :-------: |
| **Applied Math** | Taylor Series | Didier Auroux | 04 Novembre 2024 | #Calculus |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/johnny_najjar_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fjohnny%5Fnajjar%5Fdsti%5Finstitute%2FDocuments%2FRecordings%281%29%2FA24%20%2D%20Common%20Link%20%2D%20DS%2DDE%2DDA%2D20241104%5F095204%2DMeeting%20Recording%201%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Ef7e71a2a%2D1691%2D457b%2Daa8c%2Dac811a75875a)

# Summary
*Taylor Series are used to approximate functions using a known point by leveraging the derivatives of the function at that point. This allows us to calculate values of functions at points of [[Continuity & Derivability|discontinuity]].*

# Key Takeaways
1. If a function $f(x)$ has the same output and same derivatives as $g(x)$ then $f(x) = g(x)$
2. For some value, c, between a and x, there are essentially equal results between n and n+1
3. Linear regression is a Taylor approximation of order 1 and Newtonian optimization is order 2

# Definitions
- [[Continuity & Derivability|Mean Value Theorem]]: Somewhere between two points a and b, there is a point c which is the slope of the line
	- $\frac{f(b) - f(a)}{b-a} = f'(c)$
	- This is the average slope between points 

# Notes
## Taylor Expansion Series
- If we know a function's value and its derivatives at a specific point, we can approximate that function
	- As we add more and more derivatives, the approximation improves
	- ![[Pasted image 20241109133241.png]]
	- Useful for functions with discontinuities or that are highly unknown
- The general form of this series is:
	- $f(x) = f(a) + f'(a)(x-a) + \frac{1}{2}f''(a)(x-a)^2 + ... + \frac{1}{n}f^{(n)}(a)(x-a)^n$
	- $a$ is a specific reference point where we know the value of the function and its n-order derivatives and $x$ is where we are trying to approximate the function
- A Taylor Series where $a = 0$ is a Maclaurin series
- Application Example (Absolute Value)
	- The absolute value function $|x - 2| + 4$ is not differentiable at 2, so we cannot find the minimum
	- But we can approximate with a Maclaurin series at $a = 0$
		- $f(2) ≈ (|0 − 2| + 4)1 = 2 + 4 = 6$
		- $f(2) ≈ (|0 − 2| + 4) + (−1)(2 − 0) = 6 − 2 = 4$
	- The approximation converged exactly once we reached the second-order derivative
## Taylor Formula
- For practical purposes, often the first few terms of a Taylor series are used to get an approximate value <mark style="background: #FFB86CA6;">leaving the rest of the infinite sum as a remainder</mark>
- This is only defined in the neighborhood of $a$ since it is an approximation
- $f(x) = \sum^{k=0}_{n-1}\frac{f^{(k)}(a)(x-a)^k}{k!} +R_n$ ; $R_n = \frac{f^{(n)}(c)(x-a)^n}{n!}, c\in(a,x)$
	- $\exists c, a < c < b$
	- We can find a value c that ensures that the remainder is within an acceptable range
- This <mark style="background: #FFB86CA6;">lets us set a bound and determine which order we need to get to in order to have a certain accuracy</mark>
	- Let the true value of our function $f(x)$ at x be y, our approximation be p, the lower bound of our estimate be l, the upper bound u, and our approximation error e
	- n is the order of the Taylor series we have gone to
	- $\frac{l}{(n + 1)!} < e < \frac{u}{(n + 1)!}$ , so $p + \frac{l}{(n+1)!} < y < \frac{u}{(n+1)!}$
		- Our error is between the lower bound and upper bound (chosen by us) divided by the order of our series factorial, so the true value lies within the approximation plus the lower and upper error
## Multiple Dimensions
- Need to include all [[Functions and Derivatives of Functions|partial derivatives]] at each order
- $f(x_1, x_2) = f(a_1, a_2) + \frac{d}{dx_1}(a_1, a_2)(x_1 - a_1) + \frac{d}{dx_2}(a_1, a_2)(x_2 - a_2) + \frac{1}{2}${sum of 2nd order terms}