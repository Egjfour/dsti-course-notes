|   Course Name    |    Topic     |   Professor   |       Date       | Tags |
| :--------------: | :----------: | :-----------: | :--------------: | :--: |
| **Applied Math** | Trigonometry | Didier Auroux | 08 Novembre 2024 |      |

[Class Video Link](URL)

# Summary
*A 3-4 sentence description of what was learned in italics*

# Key Takeaways
1. The polar coordinates are used to express [[Complex Numbers|complex numbers]]
2. All vectors on the unit circle have a modulus of 1
3. The x-axis of the unit circle is the cosine axis and the y axis is the sine axis
4. [[Complex Numbers|Imaginary numbers]] are a rotation of $\frac{\pi}{2}$ on the unit circle
5. $sin$ and $cos$ are periodic functions with periods of $2\pi$

# Definitions
- Modulus of z: $|\textbf z|$ = $\sqrt{\textbf z \cdot \bar{\textbf z}} = \sqrt{\textbf x^2 + \textbf y^2}$ 
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
## Converting to/from Polar Coordinates
- Since $i$ is represented using the unit circle, trigonometric functions help us convert between the coordinate sets
- Convert TO polar
- Convert FROM polar
	- $x = |z| * cos(\theta)$ - Modulus of the complex number times cosine(argument)
	- $y = |z| * sin(\theta)$ - Modulus of the complex number times sine(argument)