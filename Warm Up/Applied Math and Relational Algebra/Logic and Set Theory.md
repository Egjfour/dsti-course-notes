|        Course Name        |      Topic      |  Professor   |     Date      |    Tags    |
| :-----------------------: | :-------------: | :----------: | :-----------: | :--------: |
| **Warm Up: Applied Math** | Basic Operators | Jacques Blum | 25 Avril 2024 | #SetTheory |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/ted_codd_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fted%5Fcodd%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FS24%2DWarmUp%20%2D%20One%2DTime%2DLink%2D20240425%5F094757%2DMeeting%20Recording%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview)

# Summary
*Sets allow us to examine and define relationships between objects. We express these relationships mathematically with a set of symbols such as implication ($\implies$) and equivalence ($\iff$). Sets also can be negated and can be contained within other sets as a subset ($\subset$). Sets also contain the empty set ($\emptyset$) which has zero elements.*

# Key Takeaways
1. The empty set $\emptyset$ is always a subset of any other set
2. The number of possible subsets in a given set E with n elements is 2^n
	a. If card(E) = n, card(P(E)) = 2^n (If the cardinality of E is n, then the cardinality of the parts of E is 2^n)

# Definitions
- Reciprocal: The inverse of an implication
	- If (A) $\implies$ (B), then the reciprocal is (B) $\implies$ (A) which may not necessarily be true
- Empty Set ($\emptyset$): A set with zero elements contained within
- Cardinality ($|A|$): The size of a set (A)

# Additional Resources
- [Introductory Set Theory - University of Houston](https://www.math.uh.edu/~dlabate/settheory_Ashlock.pdf)
- [Proof by Contradiction](https://en.wikipedia.org/wiki/Proof_by_contradiction)

# Notes
## Logical Symbols
- $\implies$: Implication - used to show that a property leads to another property
	- Negated by $\centernot\implies$ "does not imply"
- $\iff$: Equivalence - both properties imply each other
- $\forall$ : For all/any
- $\in$ : in the set of
- $\exists$ : There exists
	- $\centernot\exists$ is the negation ("there does not exist")
- $\exists$! : There exists one and only one

## Proof by Contradiction
- Goal here is to show that something is true by first assuming it is false and demonstrating that assuming it's false will lead to a contradiction
*Example:*
Statement: ((A) $\implies$(B)) $\iff$ (($\centernot B$) $\implies$($\centernot A$))
Proof:
1. Assume A is true
2. If we have $\centernot B$, then we must have $\centernot A$
3. Since we now have $\centernot A$ and A, we have a contradiction, so the original statement must be true

## Statement Negation
- Need to be careful to devise exactly what makes the statement no longer true
- Example:
	- Statement: $\forall x \in (P)$ "for all x, P is true"
	- Negation: $\exists x (\centernot P)$ "There exists at least one x, where P is not true"

## Sets
- Sets are collections of unique elements that are not necessarily ordered in a specific way
- We show elements belonging to a set using the following
	- $a \in E$ "Given element 'a' and set 'E', 'a' belongs to the set 'E'"
- We can also show note belonging to a set
	- $a \notin E$ "Element 'a' is not in set 'E'"

## Subsets
- A set is a subset of a larger set if all elements of the set are also elements of the larger set
- $A \subset E\:\: if\:\: \forall x \in A, x \in E$ : "A is a subset of E if for all x in A, x in E"
- Example: A = {1, 2, 3} and E = {1, 2, 3, 4}
- The <mark style="background: #FFB86CA6;">set of all subsets is defined as the parts or power P(E)</mark>
	- Example: E = {1, 2, 3}, P(E) = {{1}, {2}, {3}, {1,2}, {2,3}, {1,3}, {1,2,3}, {$\emptyset$}}
	- The cardinality of the parts of a set is 2^cardinality of the original set
	 ![[Pasted image 20240508094820.png]]

