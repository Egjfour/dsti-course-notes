|   Course Name    |     Topic      |   Professor   |        Date         |      Tags      |
| :--------------: | :------------: | :-----------: | :-----------------: | :------------: |
| **Applied Math** | Linear Algebra | Didier Auroux | 05-06 Novembre 2024 | #LinearAlgebra |

[Class Video Link 1](https://dstisas-my.sharepoint.com/personal/johnny_najjar_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fjohnny%5Fnajjar%5Fdsti%5Finstitute%2FDocuments%2FRecordings%281%29%2FA24%20%2D%20Common%20Link%20%2D%20DS%2DDE%2DDA%2D20241105%5F095116%2DMeeting%20Recording%201%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJPbmVEcml2ZUZvckJ1c2luZXNzIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXciLCJyZWZlcnJhbFZpZXciOiJNeUZpbGVzTGlua0NvcHkifX0&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E1943ba8e%2Da361%2D4d68%2Db039%2Da6d956d20ecd)
[Class Video Link 2](https://dstisas-my.sharepoint.com/personal/johnny_najjar_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fjohnny%5Fnajjar%5Fdsti%5Finstitute%2FDocuments%2FRecordings%281%29%2FA24%20%2D%20Common%20Link%20%2D%20DS%2DDE%2DDA%2D20241106%5F095339%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E6b4bbffc%2Dee50%2D4a0a%2D89f8%2D7df6d6ab4955)

# Summary
*A vector is a list of numbers that let us communicate information about multi-dimensional spaces. Many operations from real numbers (summation, difference, scalar multiplication) work the same as in dimension 1 (though require consistent dimensions), but others need special definitions. Multiplication, for example, can either be expressed as element-wise or as an inner product. A family of vectors also has different properties that describe how they're related to each other such as dependence/independence and orthogonality. A family of n pair-wise independent vectors creates a basis in $\mathbb R^n$ which spans the entire space $\mathbb R^n$.*

# Key Takeaways
1. Multiplication of a vector by a scalar is simply a rescaling of the vector on the same line
2. With linear combinations of n independent vectors $\textbf v \in \mathbb R^n$, any vector in the space $\mathbb R^n$ can be created
3. There will exist perfect correlation between two vectors that are linearly dependent
4. The only solution for a linearly independent system is the trivial solution: **0**
5. Any vector in $\mathbb R^n$ can be generated with basis vectors <mark style="background: #FFB86CA6;">in a unique way</mark> using only linear combinations of the basis vectors
6. Dividing by the norm of a vector produces unit vectors (length is 1)
7. Any bilateral symmetric function can be called an inner product

# Definitions
- Vectors: A one-dimensional array of numbers
- Linear Combination: Multiply each vector by a scalar and add the resulting vectors together
- Linear Independence: All vectors in a family contain valuable information and cannot be created through a linear combination of other vectors in the same family
- Vector Space: A collection of vectors and the operators of addition and scalar multiplication for which the space is closed under these operations
	- For example, $\mathbb R^2$ is a vector space: any 2 linearly independent vectors form a basis for $\mathbb R^2$, generating all possible vectors in the space
- Rank: The number of independent vectors in a family
	- In a $\mathbb R^n$ family, this is *at most* n
- Dot/Inner Product of Vectors: A sum of the pair-wise multiplication of elements
	- `SUMPRODUCT()` function in Excel and `%*%` operation in R
- Norm: Represents the length of the vector and is found by taking the square root of the dot product of the vector with itself
	- $\sqrt{x_1^2 + ... + x_n^2}$
- Bilinear Symmetric Function: A function that is <mark style="background: #FFB86CA6;">commutative, distributive, and associative and is linear with respect to all arguments</mark>
	- The dot product: $(x, y) \in \mathbb R^n * \mathbb R^n \to \mathbb R$
- Basis: A family of n linearly independent vectors

# Additional Resources
- [Linear Independence](https://www.geeksforgeeks.org/linear-independence/)
- [Orthogonality and Orthonormality](https://www.youtube.com/watch?v=6nqMegdbxik)
- [Gram-Schmidt Orthogonalization Process](https://www.youtube.com/watch?v=zHbfZWZJTGc&list=PLybg94GvOJ9En46TNCXL2n6SiqRc_iMB8&index=18)

# Notes
## Vector Operations
- Sum/Difference
	- Requires vectors of the same dimension
	- Produces a vector of the same dimension as the inputs
		- $\textbf v - \textbf u = \textbf s;\hspace{5mm} v,u,s \in \mathbb R^n$
	- Operation is performed element-wise
- Scalar Multiplication $\alpha \textbf v = (\alpha v_1, ..., \alpha v_n)$
	- Multiply the scalar by each element of the vector
	- Produces a vector of the same size
	- <mark style="background: #FFB86CA6;">Represents a rescaling</mark> (stretching/squeezing of the vector along the same direction)
- Multiplication (2 methods)
	- Can multiply pair-wise similarly to what is done in summation
	- Can take the dot/inner product
		- Requires 2 vectors of the same size and produces a scalar ($\mathbb R^n \to \mathbb R$)
		- Calculation is the sum of the element-wise products
		- Example:
			- ![[Pasted image 20241110094216.png]]
## Linear Combinations and Independence
- Linear Combinations
	- A linear combination of vectors takes a family of vectors, multiplies each by a scalar, and sums the result to create a new vector
		- $\alpha \textbf x + \beta \textbf y + \gamma \textbf z; \hspace{5mm} \textbf{x,y,z} \in \mathbb R^n; \hspace{2mm} \alpha, \beta, \gamma \in \mathbb R$
	- <mark style="background: #FFB86CA6;">With linear combinations, we can create any vector in the vector space</mark> ($\mathbb R^n$)
- Linear Independence
	- Implies that all vectors provide valuable information
		- In $\mathbb R^2$, this means that two vectors do not go in the same direction (are not the same line), so we can combine to create 
	- If any vector in a family is a linear combination of other vectors in that family, then that vector is linearly dependent
	- An independent system has only the trivial solution for $\alpha \textbf x + \beta \textbf y = 0$
		- $\alpha$ and $\beta$ can only be 0, so the solution is the zero vector
	- If when solving the system, a row of all zeros is produced, then that row is dependent on the others
	- ![[Linear Independence Example.jpg]]
- Rank
	- For a family of vectors, rank is the number of vectors that are linearly independent
	- The max(rank) for any family in $\mathbb R^n$ is n
		- <mark style="background: #FFB86CA6;">If there are more rows than columns, then some of the rows MUST be linearly dependent</mark>
## Orthogonal Vectors ($\textbf v \perp \textbf u$)
- Orthogonality represents there being a 90-degree angle between 2 vectors (they are perpendicular)
- We can project into a new vector space by taking the dot product of our vector with another
	- This allows us to rotate our coordinate system
- ![[Pasted image 20241110112456.png]]
- We can determine if two vectors are orthogonal by taking the dot product. <mark style="background: #FFB86CA6;">If it is 0, they are orthogonal</mark>
## Norm ($\Vert \textbf v \Vert$)
- The norm of a vector represents its length (in $\mathbb R^2$) and is always strictly positive (except if **x** is the 0 vector)
	- Derived from the Pythagorean Theorem
		- ![[Pasted image 20241110115029.png]]
- Norm is found by taking the dot product of a vector with itself and then dividing by the square root 
	- $\sqrt{x_1^2 + ... + x_n^2}$
- Properties (Bilinear symmetric function)
	- Linearity
		- Distributive: $\textbf z (\alpha \textbf x + \beta \textbf y) = \alpha \textbf x \textbf z + \beta \textbf y \textbf z$
		- Associative: $(\alpha \textbf x) \textbf z = \alpha (\textbf x \textbf z)$
## Basis Vectors
- A basis is a set of linearly independent vectors which span an entire vector space
	- Example: $\mathbb R^2$ has a basis: $\textbf v = \begin{pmatrix}0\\1\end{pmatrix} \hspace{5mm} \textbf u = \begin{pmatrix}1\\0\end{pmatrix}$
- The standard basis is the Euclidean basis which contains vectors of 0s with a single 1 value for each direction
	- Euclidean basis in $\mathbb R^3 = \begin{pmatrix}1\\0\\0\end{pmatrix}\begin{pmatrix}0\\1\\0\end{pmatrix}\begin{pmatrix}0\\0\\1\end{pmatrix} = (\textbf e^1 \textbf e^2 \textbf e^3)$  
	- Each **e** vector is one of the directions in the basis
	- ![[Pasted image 20241110133622.png]]
- An orthogonal basis is a basis such that each vector **e** in the family of vectors is orthogonal to all other
	- We can orthogonally project our vector into any basis by taking the dot product of our vector with each of the basis vectors
		- Instead of solving a system of equations, we simply solve n equations
		- Multiplying our vector by the basis vectors removes the other direction
		- ![[Pasted image 20241110134030.png]]
	- The Gram-Schmidt Process lets us orthogonalize any basis
		- Pick a vector to be the starting point $\textbf u_1 = \textbf v_1$ (**v** is the original basis and **u** is the new orthogonal basis)
		- Then each vector thereafter is itself minus the dot product of itself with each of the new orthogonal vectors divided by the norm of each of the orthogonal vectors
		- ![[Pasted image 20241110134626.png]]
- Orthonormal bases are orthogonal bases where all vectors are unit vectors (length 1)
	- Divide all vectors of an orthogonal basis by their respective norms to create an orthonormal basis
	- This is "equal to" a Euclidean basis up to a rotation
	- Let's us measure things with Pythagorean theorem