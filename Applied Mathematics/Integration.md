|   Course Name    |    Topic    |   Professor   |       Date       |   Tags    |
| :--------------: | :---------: | :-----------: | :--------------: | :-------: |
| **Applied Math** | Integration | Didier Auroux | 05 Novembre 2024 | #Calculus |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/johnny_najjar_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fjohnny%5Fnajjar%5Fdsti%5Finstitute%2FDocuments%2FRecordings%281%29%2FA24%20%2D%20Common%20Link%20%2D%20DS%2DDE%2DDA%2D20241105%5F095116%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E011ca560%2De26e%2D4ec7%2D83dc%2D7837199dd94f)

# Summary
*Integration is the opposite operation to derivation, but it is more difficult since there is no explicit formula and multiple solutions (constant of integration). It represents the area under a curve. Like with derivation, there are rules that can assist with calculating the integral. In statistics, the integral of a probability distribution is the cumulative distribution function which sums to exactly 1 over the domain of the function.*

# Key Takeaways
1. In differential calculus we are concerned with the tangent problem and resolve it by taking derivatives. <mark style="background: #FFB86CA6;">In integral calculus the problem is calculating an area under a curve</mark>
2. The anti-derivative is not unique (it is defined up to a constant $+ C$)
3. The cumulative distribution function is the anti-derivative of the probability density function

# Definitions
- Integration ($\int$): Inverse process of differentiation
	- An anti-derivative $F(x)$ is defined for $f(x)$ such that $F'(x) = f(x)$
- Primitive: The function that is differentiated to $f(x)$
	- The result of an indefinite integral

# Additional Resources
- [Integration by Parts](https://www.youtube.com/watch?v=2I-_SV8cwsw)
- [U-Substitution](https://www.youtube.com/watch?v=8B31SAk1nD8)

# Notes
## Basic Integration 
- We use the inverse operation of the [[Functions and Derivatives of Functions|derivative]] (the anti-derivative) to calculate the integral
- Basic anti-derivative/integral rules
	- Linear
		- $\int f(x) + g(x) \to F(x) + G(x) + C$
			- The integral of the sum of functions equals the sum of their anti-derivatives
		-  $\int af(x) \to aF(x) + C$
			- The integral of a constant multiplied by a function is equal to the constant multiplied by the integral
	- Power Rule
		- $\int f(x^n) = \frac{x^{n+1}}{n + 1} + C ; n \ne 1$
	- Inverse Rule
		- $\int \frac{1}{x} = ln(x) + C ; x > 0$
		- There is no direct log rule defined like for derivatives
	- Exponent Rule
		- $\int e^x = e^x + C$
	- Cosine Rule
		- $\int cos(x) = sin(x) + C$
	- Sine Rule
		- $\int sin(x) = -cos(x) + C$
- A definite integral seeks to find the area under the curve within a specific region of a continuous function
	- Evaluated on the evaluation bracket
	- $\int ^b_a = [F(x) + C]^b_a = F(b) - F(a)$
		- The integral from a to b is the anti-derivative at b less the anti-derivative at a
## Special Integral Rules (Inverse of Product and Chain Rules)
- Anti-derivative of the chain rule <mark style="background: #FFB86CA6;">(u-substitution)</mark>
	- Need to find a situation where the derivative of the inside is multiplied by the function
	- $f(g(x)) * g'(x) \to F(g(x)) + C$
	- Example:
		- $\int e^{5x} dx = \frac{1}{5} \int e^u du = \frac{1}{5} e^u + C = \frac{1}{5} e^{5x} + C$
- Anti-derivative of the product rule <mark style="background: #FFB86CA6;">(integration by parts)</mark>
	- $\int udv = uv − \int vdu$
	- Choose u to be differentiated, the rest of the expression is dv
	- Then take the anti-derivative of dv
	- Looking for the product of a function and it's derivative