|   Course Name    |     Topic      |   Professor   |        Date         |      Tags      |
| :--------------: | :------------: | :-----------: | :-----------------: | :------------: |
| **Applied Math** | Matrix Inverse | Didier Auroux | 06-07 Novembre 2024 | #LinearAlgebra |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/johnny_najjar_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fjohnny%5Fnajjar%5Fdsti%5Finstitute%2FDocuments%2FRecordings%281%29%2FA24%20%2D%20Common%20Link%20%2D%20DS%2DDE%2DDA%2D20241106%5F095339%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E7c94bf05%2Dd87a%2D41d0%2Da118%2D9f7b5e46e3c8)

# Summary
*The inverse of a matrix is a matrix that when multiplied with the original, results in the identity matrix. This can be found by solving a system of linear equations or by computing the determinant and cofactor matrix. Only square matrices can have an inverse and not all square matrices have an inverse. If any of the columns/rows are linearly dependent, then there will be no inverse.*

# Key Takeaways
1. When columns (or rows) are [[Vectors|linearly dependent]] in a matrix, there is no inverse
2. If a matrix is [[Matrices|diagonal]], the <mark style="background: #FFB86CA6;">inverse is simply the inverse of each of the elements along the diagonal</mark>
3. The inverse of a matrix **A** is 1/[[Matrix Determinant|det(A)]] multiplied by the [[Matrices|transposed]] [[Matrix Determinant|cofactor matrix]] 
4. A diagonal matrix is invertible if and only if all its elements are nonzero

# Definitions
- Inverse: In mathematics, the inverse of an element is another element that, when combined with it under a given operation, yields the identity element
	- Used for [[Matrices|matrix division]] in linear algebra
- Gauss-Jordan Elimination: Gauss-Jordan elimination is an algorithm for solving linear equations by transforming a matrix into reduced row echelon form using row operations.

# Additional Resources
- [Inverse Matrices and Their Properties](https://www.youtube.com/watch?v=kWorj5BBy9k&list=PLybg94GvOJ9En46TNCXL2n6SiqRc_iMB8&index=8)
- [Gauss-Jordan Elimination](https://online.stat.psu.edu/statprogram/reviews/matrix-algebra/gauss-jordan-elimination)

# Notes
## Finding Inverse Matrices
### Using Matrix Multiplication
- The inverse of a matrix is the matrix that results in the [[Matrices|identity matrix]] when multiplying with the original (on the left or on the right)
	- $\textbf{AA}^{-1} = \textbf A^{-1}\textbf A = \textbf I$
- This can be found by solving the system of equations resulting from multiplying with a matrix of unknowns -- Example: Find inverse of **A** = $\begin{pmatrix}2,1\\5,3\end{pmatrix}$
	- Assume $\textbf A^{-1} = \begin{pmatrix}a,c\\b,d\end{pmatrix}$
	- Perform matrix multiplication: $\textbf {AA}^{-1} = \begin{pmatrix}2a+b, 2c+d\\5a+3b, 5c+3d\end{pmatrix}$
	- Find where this matrix equals the identity matrix $\begin{pmatrix}2a+b, 2c+d\\5a+3b, 5c+3d\end{pmatrix} = \begin{pmatrix}1,0\\0,1\end{pmatrix}$
	- This creates $n$ (2 in our example) equivalent systems of equations
	- Solve using Gauss-Jordan Elimination
		- $\left(\begin{array}{cc|cc}2 & 1 & 1 & 0\\5 & 3 & 0 & 1 \end{array}\right)\thicksim R_2 - 2.5R_1$
		- $\left(\begin{array}{cc|cc}2 & 1 & 1 & 0\\0 & \frac{1}{2} & -\frac{5}{2} & 1 \end{array}\right)\thicksim 2R_2$
		- $\left(\begin{array}{cc|cc}2 & 1 & 1 & 0\\0 & 1 & -5 & 2 \end{array}\right)\thicksim R_1-R_2$
		- $\left(\begin{array}{cc|cc}2 & 0 & 6 & -2\\0 & 1 & -5 & 2 \end{array}\right) \thicksim \frac{1}{2}R_1$
		- $\left(\begin{array}{cc|cc}1 & 0 & 3 & -1\\0 & 1 & -5 & 2 \end{array}\right)$
	- Solutions are thus $\begin{pmatrix}3\\-5\end{pmatrix}\begin{pmatrix}-1\\2\end{pmatrix}$
- <mark style="background: #FFB86CA6;">For diagonal matrices, the system of equations is trivial to solve</mark> -- Example: **A** = $\begin{pmatrix}1,0,0\\0,4,0\\0,0,-2\end{pmatrix}$
	- Assume $\textbf A^{-1} = \begin{pmatrix}a,0,0\\0,b,0\\0,0,c\end{pmatrix}$
	- Perform matrix multiplication: $\textbf {AA}^{-1} = \begin{pmatrix}a, 0, 0\\0,4b,0\\0,0,-2c \end{pmatrix}$
	- Finding where this equals $\textbf I \begin{pmatrix}1,0,0\\0,1,0\\0,0,1\end{pmatrix}$ is trivial:
		- a = 1, 4b = 1, -2c = 1
		- a = 1, b = $\frac{1}{4}$, c = $-\frac{1}{2}$
### Using the Determinant
- An inverse can be easily found if we know the determinant
	- $\textbf A^{-1} = \frac{1}{det(\textbf A)}\textbf C^T$
	- We multiply the [[Matrices|transposed]] [[Matrix Determinant|cofactor matrix]] with the inverse of the [[Matrix Determinant|determinant]] of $\textbf A$