|                          Course Name                           |       Topic       |     Professor      |      Date       | Tags |
| :------------------------------------------------------------: | :---------------: | :----------------: | :-------------: | :--: |
| **Foundations of Statistical Analysis and Machine Learning 1** | Mathematic Basics | Christophe Bécavin | 13 janvier 2025 |      |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/johnny_najjar_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fjohnny%5Fnajjar%5Fdsti%5Finstitute%2FDocuments%2FRecordings%281%29%2FA24%20%2D%20Common%20Link%20%2D%20DS%2DDE%2DDA%2D20250113%5F095353%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E2952e528%2Db4b0%2D495f%2Db450%2D7f5977db0488)

# Summary
*Sums and products are useful mathematical tools that have useful properties which make solving them much easier. Both have a constant multiple and can be separated (for different operators). Summations also have important equalities that make it much easier to calculate summations of geometric series for decay problems.*

# Key Takeaways
1. Addition within a product is not able to be separated

# Additional Resources
- [Sum of Numbers 1-100 Explained](https://betterexplained.com/articles/techniques-for-adding-the-numbers-1-to-100/)

# Notes
## Summation
- Notation is a capital sigma with a from (below) and to (above): $\Sigma_{i=1}^{10}$
	- Implicit notation just has the from and is implied to infinity: $\Sigma_{i}$
- Constant Multiple Rule
	- $\sum_k c*a_k = c * \sum_k a_k$
- Addition is Separable
	- $\sum_k b_k + a_k = \sum_k a_k + \sum_k b_k$
- Special Properties
	- If $a_k = k$
		- $\sum_k = \frac{k(k+1)}{2}$
		- Example: The sum of all numbers from 1-100 = $\frac{100(100 +1)}{2} = 5050$
	- If $a_k = x^k$
		- $\sum_k a_k = \frac{x-x^{n+1}}{1-x}$
		- <mark style="background: #FFB86CA6;">Represents the partial sum of a geometric series</mark>
		- Example: Total value of an asset with diminishing marginal returns over time
			- **Scenario:** You start with an initial value of 1 unit of currency (normalized). In each subsequent year, the additional value added decreases by a factor $x$. Over $n$ years, you want to calculate the total value remaining after accounting for this decay.
			- **Parameters**:
				- $x=0.9x = 0.9x=0.9$ (the asset retains 90% of its value each year),
				- $n=4n = 4n=4$ (you want the total value for the first 4 years).
			- $\sum_{k=0}^4​x^k=1+0.9+0.81+0.729+0.6561$
			- OR with the formula: $\sum_{k=1}^4 0.9^k = \frac{0.9 - 0.9^5}{1 - 0.9}$
				- Then add the initial value at time 0 (1) to get 4.0951
## Product
- Notation is the same as a sum, but it is the product of the elements
	- $\prod_{k=1}^{10} a_k$
- Constant Multiple Rule
	- $\prod_k^n c*a_k = c^n * \prod_k^n a_k$
	- Need to take the constant to the power of the number of elements being multiplied
- <mark style="background: #FFB86CA6;">Two products are separable but NOT two sums</mark>
	- $\prod_k a_kb_k = \prod_k a_k \prod_k b_k$
	- $\prod_k a_k + b_k \ne \prod_k a_k + \prod_k b_k$
- A product of elements to a power equals the product to that same power
	- $\prod_k a_k^x = (\prod_k a_k)^x$