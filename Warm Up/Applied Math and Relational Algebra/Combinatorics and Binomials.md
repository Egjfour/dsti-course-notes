|        Course Name        |     Topic     |  Professor   |     Date      |          Tags          |
| :-----------------------: | :-----------: | :----------: | :-----------: | :--------------------: |
| **Warm Up: Applied Math** | Combinatorics | Jacques Blum | 25 Avril 2024 | #SetTheory #Statistics |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/ted_codd_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fted%5Fcodd%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FS24%2DWarmUp%20%2D%20One%2DTime%2DLink%2D20240425%5F094757%2DMeeting%20Recording%201%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview)

# Summary
*Combinations and Permutations both seek to identify how many subsets of p elements can be created from n elements. Both are solved using the factorials with the only difference being that in a permutation, the order of the elements in each subset is a relevant difference and results in a different set unlike in a combination. Combinations also are useful with the binomial theorem in determining how to expand the power of a binomial coefficient (x + y).*

# Key Takeaways
1. Two arrangements give the same combination if they have the same elements irrespective of order
2. Pascal's Rule states that $C_n^{p} = C_{n-1}^{p-1} + C_{n-1}^{p}$
3. The binomial theorem states that $(x + y)^{n} = \sum_{k=0}^{n}\binom{n}{k}x^{n-k}y^{k}$
4. By convention, a permutation or combination with p=0 is 1

# Definitions
- Permutation: A subset of [[Relations of Sets|totally ordered]] p elements among n total elements
- Combination: A subset non-ordered p elements among n total elements
- Factorial (!): The successive multiplication of a number less one until one
	- n! =  n \* (n-1) \* (n-2) \* ... \* (1)

# Additional Resources
- [Pacal's Rule (Wikipedia)](https://en.wikipedia.org/wiki/Pascal%27s_rule)
- [Binomial Theorem](https://en.wikipedia.org/wiki/Binomial_theorem)

# Notes
## Permutations
- A totally ordered finite set of elements
	- E = finite set with n elements
	- F = {1, ..., n} (the index of E)
	- Goal is to define [[Applications and Compositions of Sets|bijections]] between E and F
		- "How many possible subsets exist given the set E"
		- Compute this as n! ("n factorial")
- Can also look for arrangements of a certain length within E
	- A subset of totally ordered p elements
	- These arrangements <mark style="background: #FFB86CA6;">differ either by the nature of the elements or their order</mark>
	- Formula: $A_n^{p} = \frac{n!}{(n-p)!}$
		- Total number of all arrangements divided by the number of arrangements less than the group size

## Combinations
- A non-ordered subset of p elements among the n total elements
	- <mark style="background: #FFB86CA6;">Several arrangements give the same combination</mark>
- Need to divide the permutations by the group size factorial to account for the repeated records
	- $C_n^{p} = \frac{A_n^{p}}{p!} = \frac{n!}{(n-p)!p!}$
- Special Relations
	- $C_n^{n-p} = C_n^{p}$
	- $C_n^{0} = C_n^{n} = 1$
## Pascal's Formula
- Derived by identifying the number of combinations that do and don't contain a specific value $a_1$
	- E = {$a_1$, ..., $a_n$}
	- Number of combinations including $a_1$: $C_{n-1}^{p-1}$
		- Remaining elements for the group size from remaining elements of the set E
	- Number of combinations excluding $a_1$: $C_{n-1}^{p}$
		- Create groups of the with one less element
	- Implies that $C_n^{p} = C_{n-1}^{p-1} + C_{n-1}^{p}$
- From this we can create Pascal's Triangle
	- Add the elements that are above the current element to get number of combinations
	 ![[Pasted image 20240427200358.png]]

## Binomial Formula
- This is the algebraic extension of Pascal's Triangle that allows us to identify the expansion of a binomial formula (x + y)
![[Pasted image 20240427200625.png]]