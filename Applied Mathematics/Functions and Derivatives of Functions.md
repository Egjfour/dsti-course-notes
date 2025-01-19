|       Course Name       |           Topic           |   Professor   |       Date       |   Tags    |
| :---------------------: | :-----------------------: | :-----------: | :--------------: | :-------: |
| **Applied Mathematics** | Functions and Derivatives | Didier Auroux | 04 Novembre 2024 | #Calculus |

[Class Video Link 1](https://dstisas-my.sharepoint.com/personal/johnny_najjar_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fjohnny%5Fnajjar%5Fdsti%5Finstitute%2FDocuments%2FRecordings%281%29%2FA24%20%2D%20Common%20Link%20%2D%20DS%2DDE%2DDA%2D20241104%5F095204%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Ef5b65f50%2D995a%2D405b%2Da4c8%2D7a3767f3aaf1)
[Class Video Link 2](https://dstisas-my.sharepoint.com/personal/johnny_najjar_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fjohnny%5Fnajjar%5Fdsti%5Finstitute%2FDocuments%2FRecordings%281%29%2FA24%20%2D%20Common%20Link%20%2D%20DS%2DDE%2DDA%2D20241104%5F095204%2DMeeting%20Recording%201%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Ef7e71a2a%2D1691%2D457b%2Daa8c%2Dac811a75875a)

# Summary
*Functions are mappings from an input space to a single value of an output space. Functions can take many forms including linear (multiply each element by a coefficient and sum) or non-linear (power, exponent, log). All these functions use derivatives to understand properties such as rate of change and curvature. When dealing with multiple variables, partial derivatives are used to "zoom-in" on a specific relationship of interest and treat other variables as constant.*

# Key Takeaways
1. A constant slope (derivative of 0) is a slope line
2. In $\mathbb R^1$, the derivative is the local slope at point $x$
3. Computing a derivative is a linear process (has the same properties as a linear function)
4. The second derivative is used to find maximum and minimum values
5. Multiple inputs? Typical derivatives no longer exist. There's a slope for each direction (variable)
6. For each input variable, a multivariable function has a partial derivative

# Definitions
- Function: A function maps an input (or set of inputs) from one space to <mark style="background: #FFB86CA6;">one and only one</mark> element of an output space
- Linear Function: A function of the sum-product of elements with the following properties 
	- $f(x + y) = f(x) + f(y)$ $\forall x, y \in \mathbb R$: Function of sum of inputs = sum of outputs
	- $f(\alpha x) = \alpha f(x)$, $\forall \alpha \in \mathbb R, \forall x$: A function of a constant times x is the same as that constant times the output
- Affine Functions: Linear functions that contain and intercept
- [[Continuity & Derivability|Derivative]]: $f'(x) = \lim_{x \to x_0} \frac{f(x) - f(x_0)}{x - x_0}$
- Partial Derivative: In a multivariable function (e.g., $f(x,y) = Some\hspace{1.5mm}Formula$), the partial derivative is the derivative of the function only considering one of the variables and treating the others as constant terms
- Young's Theorem: Cross partial derivatives are always equal
	- Ex: $\frac{\partial ^2 f(x,y)}{\partial x \partial y}$ = $\frac{\partial ^2f(x,y)}{\partial y \partial x}$

# Additional Resources
- [Chain Rule (StatQuest)](https://www.youtube.com/watch?v=wl1myxrtQHQ&ab_channel=StatQuestwithJoshStarmer)
- [Change of Base Formula (Logarithms)](https://www.youtube.com/watch?v=FFm-zaFW_X4)

# Notes
## Functions
- Functions map an input (or set of inputs) from one space to an output (or set of outputs)
![[Pasted image 20241109085408.png]]
- In dimension 1: $x \in \mathbb R$ and $y \in \mathbb R$
### Linear Functions
- 2 main properties:
	- $f(x + y) = f(x) + f(y)$ $\forall x, y \in \mathbb R$: Function of sum of inputs = sum of outputs
	- $f(\alpha x) = \alpha f(x)$, $\forall \alpha \in \mathbb R, \forall x$: A function of a constant times x is the same as that constant 
- In dimension 1, the only linear functions are a straight line containing the origin
	- Cannot get a vertical line
	- $f(x) = ax, a \in \mathbb R$
- Affine functions are linear functions with an intercept added
	- $f(x) = ax + b, \forall a,b \in \mathbb R$
	- Also called linear despite not meeting the traditional linear definition
### Non-Linear Functions
- All functions that are not linear are nonlinear
- Power functions: $f(x) = x^a, a \in \mathbb R$
	- These can also have a constant being multiplied with x: $f(x) = cx^a$
	- <mark style="background: #FFB86CA6;">Also include the root functions</mark> since $\sqrt{x} = x^\frac{1}{2}$
	- <mark style="background: #FFB86CA6;">Also include inverse functions</mark> since $\frac{1}{x} = x^{-1}$
- Exponential Functions: $f(x) = a^x$
	- These can also include a constant multiplied with a: $f(x) = ca^x$
	- Standard exponential function uses Euler's number $a = e \approx 2.71 \implies e^x = exp(x)$
- Logarithmic functions: $log_a(y) = x$
	- Inverse of the exponential $f^{-1}(x)$
	- Goal: Find $x$ such that $a^x = y$
	- Base $e$ produces the natural log $ln$
## Derivatives
- Derivatives represent the local slope in dimension 1
- In all dimensions, they give the magnitude and direction of a function at a given point
- Defined explicitly by the following:
	- $f'(x) = \lim_{x \to x_0} \frac{f(x) - f(x_0)}{x - x_0}$ **OR** $f'(x) = \frac{f(x + \epsilon) - f(x)}{x - \epsilon}$
	- Take the difference in function outputs divided by the difference in function inputs as the inputs get closer and closer to each other
- <mark style="background: #FFB86CA6;">Derivatives are a linear process</mark>
	- $(f(x) + g(x))' = f'(x) + g'(x)$
	- $f'(ax) = af'(x)$
- [[Continuity & Derivability|Standard Derivative Formulas]]
	- Constant Rule: $f(x) = c \to f'(x) = 0$
	- Power Rule: $f(x) = cx^a \to f'(x) = cax^{a-1}$
	- Exponential Rule: $f(x) = e^x \to f'(x) = e^x$
	- Log Rule: $f(x) = ln(x) \to f'(x) = \frac{1}{x}$
	- Sine Rule: $f(x) = sin(x) \to f'(x) = cos(x)$
	- Cosine Rule: $f(x) = cos(x) \to f'(x) = -sin(x)$
- Product of Functions: $f(x) = u(x) * v(x)$
	- Cannot just multiply the derivatives
	- Example (see class video 1 at 1:50:00):
		- Consider the perturbation of the product of numbers. Assume there is a product $uv = 10, u = 2, v = 5$
		- If we add 1 to both u and v, the new product is NOT 11
			- difference in both v and u is 1, so $\frac{duv}{du} = 1$ and $\frac{duv}{dv} = 1$
		- Instead we need to multiply the change in each variable by the original value of the other to understand how much area is being added
	- $f(x) = u(x)v(x) \to f'(x) = u'(x)v(x) + v'(x)u(x)$
	- ![[Product Rule Geometry.jpg]]
- Chain Rule for Handling Composite Functions
	- $f(x) = u(v(x)) \to f'(x) = u'(v(x)) * v'(x)$
	- $\frac{\partial outside}{\partial inside} * \frac{\partial inside}{\partial input}$
	- Useful for derivates of logarithmic and exponential functions (w/ $u$ as a function of $x$)
		- $\frac{d\hspace{1mm} sin(u)}{dx} = cos(u)\frac{du}{dx}$ & $\frac{d\hspace{1mm} cos(u)}{dx} = -sin(u)\frac{du}{dx}$
		- $\frac{d}{dx}(e^u) = e^u\frac{du}{dx}$
		- $\frac{d}{dx}(a^u) = a^uln(a)\frac{du}{dx}$
		- $\frac{d}{dx}ln(u) = \frac{1}{u}\frac{du}{dx}$
		- $\frac{d}{dx}log_bu = \frac{d}{dx}\frac{ln(u)}{ln(b)} = \frac{1}{ln(b)*u}\frac{du}{dx}$
			- Derived from the change of base formula
- Quotient of Functions: $f(x) = \frac{u(x)}{v(x)}$
	- Similar to product rule in that you cannot simply divide the derivatives
	- Numerator is the product of functions rule
	- <mark style="background: #FFB86CA6;">Denominator is obtained by applying the chain rule</mark> and understanding that dividing by $v(x)$ is the same as multiplying by the inverse (see class video 1 @ 1:56:00)
		- $$\displaylines{
		f(x) = \frac{1}{v(x)} \to \\
		 f'(x) = ...\\
		u(x) = \frac{1}{x} \to u'(x) = -\frac{1}{x^2}\\
		\to f'(x) = -\frac{1}{v(x)^2}
		 }$$
		- Since the inverse is itself a function, $v(x)$ is the "stuff inside" and $u(x) = \frac{1}{x}$. We can then differentiate $u(x)$ and insert $v(x)$ back into the equation
	- $f'(x) = \frac{u'(x)v(x) + v'(x)u(x)}{v(x)^2}$
- Higher orders of derivatives
	- The first derivative $f'$ is the instantaneous rate of change
	- The second derivative $f''$ represents curvature at a given point
		- Concavity/convexity
		- Used to identify mins and maxes
		- A smaller second order derivative indicates a larger, more drawn-out curve
## Higher Dimensions and Partial Derivatives
- Higher dimensions are expressed by multiple inputs: $f(x,y)$
- Derivates in higher dimensions do not exist, so the goal is to come back to dimension 1
	- We do this using partial derivatives
- With partial derivatives, we consider only one variable and treat all others as constants
	- "Look down the mountain only in one direction"
	- For each input, there is a partial derivative
- In higher orders, there is a partial derivative for every permutation of variables
	- e.g., {$f'_{xx}(x,y)$, $f'_{xy}(x, y)$, $f'_{yx}(x, y)$, $f'_{yy}(x, y)$}
	- So, we have $n^2$ permutations to calculate
	- However, thanks to Young's Theorem, we know that cross partial derivates are equal
		- $f'_{xy}(x, y) = f'_{yx}(x, y)$
		- Reduces computational complexity to $\frac{n^2}{2}$