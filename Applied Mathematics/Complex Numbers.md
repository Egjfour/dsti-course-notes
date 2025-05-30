|   Course Name    |      Topic      |   Professor   |       Date       | Tags |
| :--------------: | :-------------: | :-----------: | :--------------: | :--: |
| **Applied Math** | Complex Numbers | Didier Auroux | 08 Novembre 2024 |      |

[Class Video Link](URL)

# Summary
*Complex numbers are a superset of the set of real numbers that account for $\sqrt{-1}$ which does not exist on the real number plane. In the complex number space, $i$ defines $\sqrt{-1}$, and such numbers are represented as a [[Vectors|vector]] in $\mathbb R^2$ or as the sum of a real and imaginary component. Operations on complex numbers are similar to vector operations with an exception of multiplication and division. These numbers show up when calculating the eigenvalues of a non-symmetric matrix.*

# Key Takeaways
1. A [[Matrices|non-symmetric matrix]] will have complex roots when calculating [[Eigenvalues and Eigenvectors|eigenvalues]]
2. If the discriminant $\Delta$ is negative, the solution for the eigenvalues is a complex conjugate
3. A [[Eigenvalues and Eigenvectors|hessian matrix]] or a matrix formed through [[Matrix Diagonalization|diagonalization]] will never be non-symmetric
4. The solution to multiplying a complex number by its conjugate is the real part squared plus the imaginary part squared
5. Multiplying complex numbers includes both a scale ([[Trigonometry and Polar Coordinates|modulus]]) and rotation

# Definitions
- Complex number: A superset of the [[Real Numbers, Real Sequences, and Limits|real numbers]] $\mathbb R$ which define negatives for square roots
- Conjugate of a Complex Number: Same number with the opposite sign on the imaginary part

# Additional Resources
- [Complex Numbers (First Third)](https://www.youtube.com/watch?v=cEwmlyaxLKQ)

# Notes
## Square Root of a Negative
- It is not actually possible to calculate this using $\mathbb R$
	- Instead we can split it out - example: $\sqrt{-16} = \sqrt{16} * \sqrt{-1}$
- Frequently see this arise within time-series data
- Complex numbers will be used
	- Lets us switch to a frequency view or perform signal processing
- All eigenvalues and eigenvectors will contain $i$
## Complex Numbers $\mathbb C$
- A [[Real Numbers, Real Sequences, and Limits|complex number]] lets us define a new number outside $\mathbb R$, $i = \sqrt{-1}$
- Complex numbers are composed of a real part and an imaginary part
	- $z =$ real + imaginary(i)
	- $z = x + iy$
- In a polynomial function of degree n, there will always be n roots in the complex space
- These can be represented using $\mathbb R^2$ and considered as a 2D vector
- Operations
	- Sum of vectors is the same as the sum of complex numbers
	- Multiplication is treated like a FOIL operation (NOT matrix multiplication or a dot product)
		- ![[Pasted image 20241115121922.png]]
		- Example: $z_1 = 4 + 2i$ & $z_2 = 3 - 4i$, find $z_1 z_2$
			- $(4 + 2i)(3 - 4i) = 12 - 14i +6i -8i^2$
				- $8i^2 = 8*-1 = -8$
			- $= 20 - 8i$
	- Division is not defined without a real number in the denominator
		- We need to multiply by the conjugate of the denominator
		- Example: $\frac{1 + 2i}{-3 + 3i} = \frac{(1 + 2i)(-3-3i)}{(-3+3i)(-3-3i)}=\frac{3-9i}{18} = \frac{1}{6} - \frac {1}{2}i$