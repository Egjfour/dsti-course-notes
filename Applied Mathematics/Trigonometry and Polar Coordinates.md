|   Course Name    |    Topic     |   Professor   |       Date       | Tags |
| :--------------: | :----------: | :-----------: | :--------------: | :--: |
| **Applied Math** | Trigonometry | Didier Auroux | 08 Novembre 2024 |      |

[Class Video Link](URL)

# Summary
*Polar coordinates are a mechanism for representing the [[Complex Numbers|complex number]] space in a means that is better-suited for mathematical operations such as multiplication and division. The polar coordinates represent the complex number space as a length of the vector and an angle between the vector and the real number axis (x-axis). To calculate the polar coordinates, we use the normalized vector alongside trigonometric properties of the sine and cosine functions. Euler also provides a mechanism to represent these coordinates: $||z||e^{i\pi}$. Using this representation, multiplication and division of complex numbers becomes trivial.*

# Key Takeaways
1. The polar coordinates are used to express [[Complex Numbers|complex numbers]]
2. All vectors on the unit circle have a modulus of 1
3. <mark style="background: #FFB86CA6;">The x-axis of the unit circle is the cosine axis and the y axis is the sine axis</mark>
4. [[Complex Numbers|Imaginary numbers]] are a rotation of $\frac{\pi}{2}$ on the unit circle
5. $sin$ and $cos$ are periodic functions with periods of $2\pi$

# Definitions
- Modulus of z: $||\textbf z||$ = $\sqrt{\textbf z \cdot \bar{\textbf z}} = \sqrt{\textbf x^2 + \textbf y^2}$ 
	- Simply the norm of $\textbf z$
- Argument of z: The angle between the real axis and z ($\theta$)

# Additional Resources
- [Polar Coordinates (Skip First 5 Minutes)](https://www.youtube.com/watch?v=cEwmlyaxLKQ)
- [Converting Between Coordinate Systems](https://www.mathsisfun.com/polar-cartesian-coordinates.html)

# Notes
## Polar Coordinates
- Allow us to express [[Complex Numbers|complex numbers]] as vectors
- Use two coordinates, the length (modulus) and the angle between the real and imaginary (x and y) axes (the argument, $\theta$)

## Unit Circle and Basic Trigonometric Properties
- A circle which is centered around the origin with a radius of 1
- Angles are measured counter-clockwise (the trigonometric way)
- A $90 \degree$ rotation is $\frac{\pi}{2}$ and the measurements continue to repeat as we go around the circle
	- Angles become negative as we move clockwise
- $sin$ and $cos$ are periodic functions with periods of $2\pi$
- ![[Pasted image 20241111234651.png]]
- Important values of $sin(\theta)$ and $cos(\theta)$

| $\theta$        | $cos(\theta)$       | $sin(\theta)$       |
| --------------- | ------------------- | ------------------- |
| 0               | 1                   | 0                   |
| $\frac{\pi}{6}$ | $\frac{\sqrt 3}{2}$ | $\frac{1}{2}$       |
| $\frac{\pi}{4}$ | $\frac{1}{\sqrt 2}$ | $\frac{1}{\sqrt 2}$ |
| $\frac{\pi}{3}$ | $\frac{1}{2}$       | $\frac{\sqrt 3}{2}$ |
| $\frac{\pi}{2}$ | 0                   | 1                   |
## Trigonometric Relations
- $sin$ is an *odd function*: $sin(-\alpha) = -sin(\alpha)$
- $cos$ is an *even function*: $cos(-\alpha) = cos(\alpha)$
- Angle sum and difference
	- $sin(\alpha \pm \beta) = sin(\alpha)cos(\beta) \pm cos(\alpha)sin(\beta)$
	- $cos(\alpha \pm \beta) = cos(\alpha)cos(\beta) \mp sin(\alpha)sin(\beta)$
- Double angle
	- $sin(2\alpha) = 2sin(\alpha)cos(\alpha)$
	- $cos(2\alpha) = cos^2(\alpha) - sin^2(\alpha)$
- Power Relations
	- $sin^2(\alpha) = \frac{1}{2}(1 - cos(2\alpha))$
	- $cos^2(\alpha) = \frac{1}{2}(1 + cos(2\alpha))$
## Converting to/from Polar Coordinates
- Since $i$ is represented using the unit circle, trigonometric functions help us convert between the coordinate sets
- Convert TO polar
	- First find the modulus of the complex number
	- Then determine where the following statements are true for $\theta$
		- $cos(\theta) =$ *real part*
		- $sin(\theta) =$ *imaginary part*
	- Example: Given $z = 1 + \sqrt{3i}$, find the polar coordinates
		- Determine Modulus: $\sqrt{1^2 + (\sqrt 3)^2} = \sqrt 4 = 2$
		- Normalize the vector of cartesian coordinates $\begin{pmatrix}1\\ \sqrt 3 \end{pmatrix}$
			- $\begin{pmatrix}1\\ \sqrt 3 \end{pmatrix} * \frac{1}{2} = \begin{pmatrix}\frac{1}{2}\\ \frac{\sqrt 3}{2} \end{pmatrix}$
		- Identify Theta
			- $cos(\theta) = \frac{1}{2}$
			- $sin(\theta) = \frac{\sqrt 3}{2}$
			- So, $\theta = \frac{\pi}{3}$
		- Polar Coordinates = $(2, \frac{\pi}{3})$
- Convert FROM polar
	- $x = ||z|| * cos(\theta)$ - Modulus of the complex number times cosine(argument) = *real part*
	- $y = ||z|| * sin(\theta)$ - Modulus of the complex number times sine(argument) = *imaginary part*
	- Example: Given polar coordinates (2, $\frac{\pi}{3}$), find the cartesian coordinates
		- $||z|| * (cos(\theta) + isin(\theta)) = 2(cos(\frac{\pi}{3}) + isin(\frac{\pi}{3}))$
			- $cos(\frac{\pi}{3}) = \frac{1}{2}$
			- $sin(\frac{\pi}{3}) = \frac{\sqrt 3}{2}$
		- So, $\begin{pmatrix}\frac{1}{2} * 2\\ \frac{\sqrt 3}{2} *2\end{pmatrix} = \begin{pmatrix}1\\ \sqrt 3\end{pmatrix}$
		- Thus, $z = 1 + \sqrt{3i}$
## Complex Exponential Form
- Complex exponential form is derived from Euler's identity and uses the polar coordinates to express
- The exponential piece always has a modulus of 1
	- $||e^{i \hspace{1mm}*\hspace{1mm} anything}|| = 1$
- This is represented using the modulus $|z|$ and argument $\theta$ 
	- Formula: $|z|e^{i\pi}$
- <mark style="background: #FFB86CA6;">Allows for much easier multiplication and division of complex numbers</mark>
	- Since multiplication of two exponents of the same base is just addition of the exponents
		- Example: $e^{i\theta_1}e^{i\theta_2} = e^{i\theta_1 + i\theta_2} = e^{i(\theta_1 + \theta_2)}$
		- $z_1 * z_2 = (||z_1|| * ||z_2||) * e^{i(\theta_1 + \theta_2)}$
	- Division is subtraction of the exponents with the same base
		- $\frac{z_1}{z_2} = \frac{||z_1||e^{i\theta_1}}{||z_2||e^{i\theta_2}}= \frac{||z_1||}{z_2}e^{i(\theta_1 - \theta_2)}$
## Properties to Remember
- Multiples of $2\pi$ get us to the same spot, so $25\pi$ = $\pi$ since $25\pi = 24\pi * \pi$
- $e^{i\pi} = -1$
- Dividing by i means to rotate by $-\frac{\pi}{2}$ ($90\degree$ clockwise)
	- Since i is periodic (we keep spinning around the circle), fractions of $i$ can be seen as exponents of $i$ as well
		- $\frac{1}{i} = i^3$
- We can break down exponents of $i$ fairly easily by remembering that $i^2 = \sqrt{-1}$
	- Example: $i^{41} = i^{40}*i= ({i^{2}})^{20} * i = (-1)^{20} * i = 1 * i = i$