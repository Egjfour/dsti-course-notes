|   Course Name    |                        Topic                        |   Professor   |        Date         |      Tags      |
| :--------------: | :-------------------------------------------------: | :-----------: | :-----------------: | :------------: |
| **Applied Math** | Diagonalization of Matrices (Square and non-Square) | Didier Auroux | 07-08 Novembre 2024 | #LinearAlgebra |

[Class Video Link 1](https://dstisas-my.sharepoint.com/personal/johnny_najjar_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fjohnny%5Fnajjar%5Fdsti%5Finstitute%2FDocuments%2FRecordings%281%29%2FA24%20%2D%20Common%20Link%20%2D%20DS%2DDE%2DDA%2D20241107%5F095151%2DMeeting%20Recording%201%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E85e764e1%2Dbfdb%2D4c9e%2Db851%2D933121f101da)
[Class Video Link 2](https://dstisas-my.sharepoint.com/personal/johnny_najjar_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fjohnny%5Fnajjar%5Fdsti%5Finstitute%2FDocuments%2FRecordings%281%29%2FA24%20%2D%20Common%20Link%20%2D%20DS%2DDE%2DDA%2D20241108%5F095114%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E0426196a%2Dabe7%2D4da3%2D9084%2D522791403eab)

# Summary
*Creating a diagonal matrix is essential for performing matrix operations as the size of the matrix scales upward. This is done by calculating the eigenvalues and by using the eigenvectors as a rotation matrix. Creating a diagonal matrix is predicated on first having a square, symmetric matrix which can be created by multiplying with the transposed matrix.*

# Key Takeaways
1. Goal is to find numbers that when multiplied with the [[Matrices|identity matrix]] and then multiplied with the original matrix, produce the zero matrix: $det(\textbf A - \lambda \textbf I) = 0$
2. The original matrix $\textbf A$ and the new diagonal matrix $\textbf D$ have the same determinant
3. <mark style="background: #FFB86CA6;">The values of the diagonal matrix are simply the eigenvalues of the original matrix</mark>
4. All square, symmetric matrices have positive eigenvalues

# Definitions
- Rotation Matrix ($\textbf Q$): The set of all eigenvectors
	- <mark style="background: #FFB86CA6;">Columns must preserve the order of the eigenvalues </mark>
- Positive Matrix: For a square matrix $\textbf M$, the result of multiplying by any vector $\textbf x$ and then taking the dot product with the same vector $\textbf x$ is always positive
	- $(\textbf {Mx})\textbf x \ge 0 \hspace{2mm} \forall \textbf x \in \mathbb R^n$
	- On a diagonal matrix, simply means all eigenvalues are positive

# Additional Resources
- [Diagonalization](https://www.youtube.com/watch?v=WTLl03D4TNA&list=PLybg94GvOJ9En46TNCXL2n6SiqRc_iMB8&index=20)
- [Diagonal Matrix is Just Eigenvalues?](https://math.stackexchange.com/questions/1752105/diagonal-matrix-just-eigenvalues#:~:text=Yes.,proper%20multiplicities)
- [Positive/Negative Matrix](https://math.stackexchange.com/questions/2369328/easy-way-to-determine-matrix-positive-negative-definiteness)

# Notes
## Rotation Matrix ($\textbf Q$)
- The rotation matrix is formed from the [[Eigenvalues and Eigenvectors|eigenvectors]]
- Properties
	- [[Vectors|Orthogonality]]: $\textbf{QQ}^T = \textbf Q^T \textbf Q = \textbf I \implies \textbf Q^T = \textbf Q^{-1}$
		- The transpose of the rotation matrix is its inverse
## Using the Rotation Matrix to Diagonalize
- We can apply the rotation to create the diagonal matrix $\textbf D$
	- $\textbf Q^{-1} \textbf {AQ} = \textbf D$
- All properties of $\textbf A$ are the same as the properties on $\textbf D$
	- Same [[Matrix Determinant|determinant]]
		- The product of the eigenvalues is the determinant
	- Same [[Eigenvalues and Eigenvectors|trace]]
		- The sum of the eigenvalues is the trace
- In $\mathbb R^2$ the trace and determinant are in the [[Eigenvalues and Eigenvectors|polynomial expression]] that solves $\lambda$
	- $\lambda^2 - 4\lambda - 45 = 0$
	- $tr(\textbf A) = -4$
	- $det(\textbf A) = -45$
## Handling Non-Square Matrices
- Calculating [[Eigenvalues and Eigenvectors|eigenvalues and eigenvectors]] requires matrices that are square
- Typical datasets have far more observations (rows) than features (columns), so they are not square
- We can create a square matrix from our data by multiplying it by itself transposed
	- Works from either side, so should multiply transpose from the left to produce smallest matrix possible
		- $\textbf A^T\textbf A$ is preferred to $\textbf{AA}^T$
	- Such a matrix has the <mark style="background: #FFB86CA6;">same amount of information as the original matrix</mark>
		- Multiplying from both sides also conveys the same amount of information
		- Contains the eigenvalues of the matrix $\textbf A$
	- These matrices are always positive
		- The eigenvalues will also always be positive
			- Negative matrix has strictly negative eigenvalues
		- The <mark style="background: #FFB86CA6;">eigenvalues communicate the amount of information provided in the corresponding direction</mark>
			- Relative Information $= \frac{\lambda_i}{\sum\lambda_i}$
	- If any of these eigenvalues is zero, then there is a relation between the columns