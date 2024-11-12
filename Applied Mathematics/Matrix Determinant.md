|   Course Name    |    Topic     |   Professor   |        Date         |      Tags      |
| :--------------: | :----------: | :-----------: | :-----------------: | :------------: |
| **Applied Math** | Determinants | Didier Auroux | 06-07 Novembre 2024 | #LinearAlgebra |

[Class Video Link 1](https://dstisas-my.sharepoint.com/personal/johnny_najjar_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fjohnny%5Fnajjar%5Fdsti%5Finstitute%2FDocuments%2FRecordings%281%29%2FA24%20%2D%20Common%20Link%20%2D%20DS%2DDE%2DDA%2D20241106%5F095339%2DMeeting%20Recording%202%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E991e6303%2D0561%2D48d9%2D90a7%2D2454ed28ccea)
[Class Video Link 2](https://learn.dsti.institute/mod/url/view.php?id=20906)
# Summary
*A determinant is a function that takes a square matrix as input and returns a single number as output using a recursive process. This number is used to help identify many things including the presence of an inverse for a given matrix (as well as calculating it). The general process for calculating the determinant is to perform cofactor expansion along a selected row/column of the matrix.*

# Key Takeaways
1. Only [[Matrices|square matrices]] can have a determinant
2. If the determinant of a matrix $\ne$ 0, it has an [[Matrix Inverse|inverse]]
	a. Practically speaking, noise means we will never get exactly zero, so we should look for numbers close to zero
3. The determinant of a [[Matrices|diagonal matrix]] is simply the product of its elements

# Definitions
- Determinant: A [[Functions and Derivatives of Functions|function]] that takes a matrix and returns a number 
	- In geometry, the determinant is the signed area/volume of a plane/cube
- Minor Matrix ($\textbf M$): A matrix of the determinants of matrix **A** expanded along the corresponding row and column
	- $m_{ij} = det(\textbf A \hspace{1.5mm}(excluding\hspace{1.5mm} row\hspace{1.5mm} i\hspace{1.5mm} and \hspace{1.5mm}column\hspace{1.5mm} j))$
- Cofactor Matrix ($\textbf C$): A matrix of the minors multiplied by their sign resulting from the circular permutation
	- $c_{ij} = (-1)^{i+j}m_{ij}$

# Additional Resources
- [Cofactor Matrix](https://www.cuemath.com/algebra/cofactor-matrix/)

# Notes
## Determinant of a 2-Dimensional (2x2) Matrix
- Take the product of the elements on the main diagonal and subtract from it the product of the elements on the opposite diagonal
- Example: $\textbf A = \begin{pmatrix}a,c\\b,d\end{pmatrix}$
	- $det(\textbf A) = ad - bc$
## Determinant of n-Dimensional Matrix
- Need to consider all permutations of one element from each row and column
	- All permutations of $(i, j)$ such that each $(i, j)$ is only used once in each permutation
	- Column j and row i can only be used ONCE in a given permutation (not the combination of them necessarily)
	- Like a game of Sudoku
	- This is a recursive algorithm: we keep expanding until we find 2x2 matrices
- We can expand along one of the rows or columns to calculate -- Example: $det(\begin{pmatrix}2,1,0\\1,4,5\\0,2,-1\end{pmatrix})$
	- If we expand along the first column, $2 * det(\begin{pmatrix}4,5\\2,-1\end{pmatrix}) - 1 * det(\begin{pmatrix}1,0\\2,-1\end{pmatrix}) + 0 * det(\begin{pmatrix}1,0\\4,5\end{pmatrix})$
	- Now, we have 2x2 matrices and can solve: $2 * -14 - 1 * -1 + 0 * 1 = -27$
	- Can make this easier by creating zeros with elementary operations
## Minor and Cofactor Matrices
- Both the minor $\textbf M$  and cofactor $\textbf C$ matrices are the same dimensions as the original matrix $\textbf A$
- Minor Matrix
	- Contains the determinant of the matrix $\textbf A$ excluding the corresponding row and column
	- This does not include the multiplication of $a_{ij}$ with the determinant
- Cofactor matrix
	- Minor matrix with the sign resulting from the permutation movements applied
	- The sign on the diagonal is always positive
- If the matrix $\textbf A$ is <mark style="background: #FFB86CA6;">diagonal (or triangular)</mark>, then $\textbf M = \textbf C$
	- Each element in $\textbf M$ and $\textbf C$ is the determinant which is the <mark style="background: #FFB86CA6;">sum of the elements along the diagonal</mark>
	- This means that the [[Matrix Inverse|inverse]] is simply the inverse of each element numerically
- This operation is very computationally expensive without triangular/diagonal matrices
	- $n!$ for a non-diagonal matrix but $n - 1$ for triangular
