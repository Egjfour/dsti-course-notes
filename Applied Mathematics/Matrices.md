|   Course Name    |       Topic       |   Professor   |       Date       |      Tags      |
| :--------------: | :---------------: | :-----------: | :--------------: | :------------: |
| **Applied Math** | Matrix Operations | Didier Auroux | 06 Novembre 2024 | #LinearAlgebra |

[Class Video Link 1](https://dstisas-my.sharepoint.com/personal/johnny_najjar_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fjohnny%5Fnajjar%5Fdsti%5Finstitute%2FDocuments%2FRecordings%281%29%2FA24%20%2D%20Common%20Link%20%2D%20DS%2DDE%2DDA%2D20241106%5F095339%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E7c94bf05%2Dd87a%2D41d0%2Da118%2D9f7b5e46e3c8)
[Class Video Link 2](https://dstisas-my.sharepoint.com/personal/johnny_najjar_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fjohnny%5Fnajjar%5Fdsti%5Finstitute%2FDocuments%2FRecordings%281%29%2FA24%20%2D%20Common%20Link%20%2D%20DS%2DDE%2DDA%2D20241106%5F095339%2DMeeting%20Recording%202%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Ebe1c6c31%2Dabb8%2D4f97%2D87bf%2D3e64d8a2ef2f)

# Summary
*Matrices are 2-dimensional vectors which allow us to represent systems of equations. A square matrix has the same number of rows and columns, and within square matrices are many other types of matrices which have useful properties. Among these, the most useful is the diagonal matrix since it allows for a massive simplification of the computational complexity of matrix operations (particularly matrix multiplication, which for two square matrices normally has a computational complexity of n-cubed.*

# Key Takeaways
1. Matrices do not contain any missing elements
2. Goal is to create a diagonal matrix since it reduces computational complexity greatly
3. To perform matrix multiplication between **A** and **B**, the number of columns in **B** must be equal to the number of rows in **A**
4. Matrix multiplication is NOT a linear operation and is <mark style="background: #FFB86CA6;">NOT commutative</mark>
5. If a two matrices are diagonal, the product is simply the product of the elements on the diagonal
6. There is no defined matrix division, instead we multiply by the [[Matrix Inverse|inverse]] ($\textbf A^{-1}$)
7. <mark style="background: #FFB86CA6;">Diagonal matrices allow us to perform n independent calculations in dimension 1</mark>

# Definitions
- Matrix: A 2-dimensional [[Vectors|vector]] defined in $\mathbb R^{m\hspace{0.5mm}x\hspace{0.5mm}n}$
	- m as # of rows and n as # of columns
- Square Matrix: A matrix with the same number of rows and columns $R^{n\hspace{0.5mm}x\hspace{0.5mm}n}$
- Triangular Matrix: A square matrix that only has values on and above (or below) the main diagonal
- Diagonal Matrix: A square matrix that only has values on the main diagonal (zeros elsewhere)
	- $a_{ij} = 0 \hspace{2mm} \forall i \ne j$
- Symmetric Matrix: A square matrix where all off-diagonal elements of the inverted row and column index are the same: $a_{ij} = a_{ji}\hspace{2mm} \forall i,j$
	- $\textbf A$ is symmetric if $\textbf A^T = \textbf A$ (The matrix is equal to its transpose)
- Identity Matrix: A diagonal matrix with only ones on the diagonal
	- In $\mathbb R^2$: $\begin{pmatrix}1,0\\0,1\end{pmatrix}$

# Additional Resources
- [Matrix Multiplication Visualized](https://matrixmultiplication.xyz/)

# Notes
## Matrix Notation
- Capital boldface letters used to represent matrixes
- Matrix elements are defined by their index ($a_{ij}$ is the element at row i and column  j)
- Matrices are defined in a 2-dimensional space of real (or [[Complex Numbers|complex]]) numbers
	- $\mathbb R^{m\hspace{0.5mm}x\hspace{0.5mm}n}$ OR $\mathbb C^{m\hspace{0.5mm}x\hspace{0.5mm}n}$
## Simple Matrix Operations
- Sum/difference
	- Defined for 2 matrices of the same dimensions
	- Simply add element-wise as we did for [[Vectors|vector addition]]
	- Same rules and procedure applied for subtraction
	- If diagonal, only the diagonal elements need to be calculated and stored
		- Becomes a vector addition
- Scalar Multiplication
	- Multiply each element of the matrix by the scalar
	- $\alpha \textbf A = \sum_{i=1}^m\sum_{j=1}^n\alpha a_{ij}$
- Both operations are commutative, distributive, and associative
- Matrix Transposition
	- Columns become rows and rows become columns
	- $a_{ij} = a_{ji} \hspace{2mm} \forall i,j$
	- Denoted as a superscript with "$T$"
		- Transpose of $\textbf A$: $\textbf A^T$
## Matrix Multiplication
- NOT defined as the element-wise product
- Instead, this is <mark style="background: #FFB86CA6;">viewed as the linear application of a function</mark>
- Take the dot product of each row in **A** with each column in **B**
- Produces a matrix with the same number of rows as **A** and same number of columns as **B**
- NOT a commutative operation: $\textbf{AB}\ne\textbf{BA}$
	- **BA** may not even be possible given the dimensions
	- Still true even with square matrices
- <mark style="background: #FFB86CA6;">Distributivity exists, but the order of the multiplication MUST be preserved</mark>
	- $(\textbf A + \textbf B)\textbf C = \textbf{AC} + \textbf{BC} \ne \textbf{CA} + \textbf{CB} = \textbf C (\textbf B + \textbf A)$
		- Addition is commutative which is why order of **A** and **B** can be switched inside the parentheses
- Associativity is preserved: $\textbf{ABC} = \textbf A(\textbf{BC}) = (\textbf{AB})\textbf C$
- The computational cost of matrix multiplication is $m * n * p$
	- We need $n$ multiplications and $n-1$ additions for each $n^2$ elements
	- For two diagonal matrices, the number of operations is simply $n$ since we can take the product of the diagonal elements
## Matrix Division
- There is no defined matrix division
	- Instead we need to multiply by the [[Matrix Inverse|matrix's inverse]]
- Reasoning
	- Let **A** be a square matrix $n\hspace{0.5mm}x\hspace{0.5mm}n$
	- **B** is $n\hspace{0.5mm}x\hspace{0.5mm}n$ such that **AB** = **BA**
	- **B** must then be the inverse of **A**
	- So, the product is the identity matrix, **I**
	- Thus, **B** = $\textbf A^{-1}$