|   Course Name    |                 Topic                  |   Professor   |       Date       |      Tags      |
| :--------------: | :------------------------------------: | :-----------: | :--------------: | :------------: |
| **Applied Math** | Calculating Eigenvalues / Eigenvectors | Didier Auroux | 07 Novembre 2024 | #LinearAlgebra |

[Class Video Link](URL)

# Summary
*Eigenvalues are values that scale a vector such that the vector multiplied by the eigenvalues is equal to the same vector multiplied by some matrix. We calculate these by solving a polynomial of degree $n$ such that the determinant of our matrix less the identity matrix times the eigenvectors is zero. Finding these values is essential to [[Matrix Diagonalization|diagonalizing matrices]]. The vector $\textbf x$ that the eigenvalues scale are the eigenvectors. There is one eigenvalue for each eigenvector*

# Key Takeaways
1. Eigenvectors must be non-trivial (cannot be the zero vector)
2. A matrix $\textbf A \in \mathbb R^{n\hspace{0.5mm}x\hspace{0.5mm}n}$ has at most $n$ eigenvalues and each eigenvalue corresponds to a unique eigenvector
3. <mark style="background: #FFB86CA6;">The values along the main diagonal of a triangular or diagonal matrix are the eigenvalues</mark>
4. Eigenvectors are pair-wise [[Vectors|orthogonal]]
5. In $\mathbb R^2$, the sign of the trace and [[Matrix Determinant|determinant]] gives the sign of the eigenvalues
6. Eigenvalues help us see if linear relations exist even in the presence of noise since [[Matrices|rank]] cannot handle noise being present
7. If one or more eigenvalues for a matrix is 0, then there is a relationship between the columns of that matrix ($\exists$ linear dependency)
8. If the eigenvalues are all positive, then the entire matrix is positive
9. If the matrix $\textbf A$ is not symmetric, then we will get no real roots and the eigenvalues will be a [[Complex Numbers|complex conjugate]]
10. A matrix in space $\mathbb R^n$ creates a polynomial of degree $n$ where there is only one value of degree $n$ which does not have a coefficient but does have a sign

# Definitions
- Eigenvector: A vector of values such that when it is multiplied by a matrix, it equals a scaling of the original vector
	- $\textbf {Ax} = \lambda \textbf x$
- Eigenvalue: The various scalar values ($\lambda$) that scale the eigenvectors. Measure the amount of information/energy in each direction
- Matrix-Vector Multiplication: Process that takes a matrix in $\mathbb R^{m\hspace{1mm} x \hspace{1mm} n}$ and multiplies it by a vector $\textbf v \in \mathbb R^n$ to produce a vector in $\mathbb R^n$
	- Calculate the [[Vectors|dot product]] of the vector with each row of the matrix
- Matrix <mark style="background: #FFB86CA6;">Trace: Sum of the elements on the main diagonal</mark>
	- $\textbf A = \begin{pmatrix}3,-1,2\\0,4,1\\1,-1,-5\end{pmatrix}$
	- $tr(\textbf A) = 3 + 4 + (-5) = 2$

# Additional Resources
- [Finding Eigenvalues and Eigenvectors](https://www.youtube.com/watch?v=TQvxWaQnrqI&list=PLybg94GvOJ9En46TNCXL2n6SiqRc_iMB8&index=19)

# Notes
## Use Cases of Eigenvalues
- Solve systems of linear differential equations
- Describe frequencies of vibrations
- Separate modes of motion
- Convert a [[Matrices|square, symmetric matrix]] into a [[Matrix Diagonalization|diagonal matrix]]
## Calculating Eigenvalues ($\lambda$)
- $\textbf A$ must be a [[Matrices|square, symmetric matrix]]
- We want to find the values of $\lambda$ that satisfy $\textbf {Ax} = \lambda \textbf x$
	- Subtract $\lambda \textbf x$: $\textbf {Ax} - \lambda \textbf x = 0$
	- Factor out $\textbf x$: $(\textbf A - \lambda) \textbf x = 0$
	- Multiply $\lambda$ by the identity matrix: $(\textbf A - \lambda \textbf I) \textbf x = 0$
		- This lets us perform the subtraction with $\textbf A$
	- We want non-trivial solutions (x cannot be **0**)
		- Thus we want a non-invertible matrix so that we are not able to calculate **x** as **0** by multiplying both sides by the inverse
	- Find where $det(\textbf A - \lambda \textbf I) = 0$
		- Characteristic equation
		- Solutions to this polynomial equation will be the eigenvalues
- Example: Let $\textbf A = \begin{pmatrix}2,7\\7,2\end{pmatrix}$
	- Find $det(\textbf A - \lambda \textbf I) = 0$
	- Perform the [[Matrices|subtraction]]: $det(\begin{pmatrix}2-\lambda, 7\\7,2-\lambda\end{pmatrix}) = 0$
	- Apply [[Matrix Determinant|Determinant Formula]]: $(2 - \lambda)(2-\lambda) - 49 = 0$
	- Simplify the polynomial: $\lambda^2 - 4\lambda - 45 = 0$
	- Solve for $\lambda$ (Solve - Quadratic Roots)
		- Calculate the discriminant ($\Delta$ = $b^2 - 4ac$): $(-4)^2 - 4(1)(-45) = 196$
		- Apply the quadratic formula ($\lambda = \frac{-b \pm \sqrt \Delta}{2a}$): $\frac{4 \pm \sqrt {196}}{2(1)} = 9, 5$
	- Eigenvalues are thus 9 and 5
## Calculating Eigenvectors ($\textbf q$)
- The eigenvectors are the vectors $\textbf x$ after being scaled by the eigenvalues $\lambda$
- To do this, we need to calculate $\textbf {Ax} = \lambda \textbf x$ for each value of $\lambda$
	- Can solve as a system of equations
- <mark style="background: #FFB86CA6;">All the eigenvectors will be orthogonal</mark>
	- We can divide by the norm to create an orthonormal set of vectors
		- This creates a [[Vectors|basis]]
- Example: Let $\textbf A = \begin{pmatrix}2,7\\7,2\end{pmatrix}$
	- Calculate eigenvalues: $\lambda_1 = 9; \hspace{2mm} \lambda_2 = 5$
	- Apply $\lambda_1$ to solve for $\textbf x$: $(\textbf A - \lambda_1 \textbf I) \textbf x = \textbf 0$
		- $-7x_1 + 7x_2 = 9x_1$ AND $7x_1 - 7x_2 = 9x_2$
			- So the eigenvector is $\begin{pmatrix}7\\16\end{pmatrix}$
		- $\begin{pmatrix}2-9, 7\\7, 2-9\end{pmatrix}\textbf x = \textbf 0 = \begin{pmatrix}-7,7\\7,-7\end{pmatrix}\textbf x$
		- Solve: $\left(\begin{array}{cc|c}-7 & 7 & 0\\7 & -7 & 0\end{array}\right) = \begin{pmatrix}\frac{1}{\sqrt 2}\\ \frac{1}{\sqrt 2}\end{pmatrix}$
	- Apply $\lambda_2$ to solve for $\textbf x$
		- $\begin{pmatrix}2-5, 7\\7, 2-5\end{pmatrix}\textbf x = \textbf 0 = \begin{pmatrix}-3,7\\7,-3\end{pmatrix}\textbf x$
		- Solve: $\left(\begin{array}{cc|c}-3 & 7 & 0\\7 & -3 & 0\end{array}\right) = \begin{pmatrix}\frac{1}{\sqrt 2}\\ -\frac{1}{\sqrt 2}\end{pmatrix}$
	- Thus, our eigenvectors are $\textbf v_1 = \begin{pmatrix}\frac{1}{\sqrt 2}\\ \frac{1}{\sqrt 2}\end{pmatrix}$ and $\textbf v_2 = \begin{pmatrix}\frac{1}{\sqrt 2}\\ -\frac{1}{\sqrt 2}\end{pmatrix}$
