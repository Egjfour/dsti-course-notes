|   Course Name    |   Topic    |  Professor   |     Date      |    Tags    |
| :--------------: | :--------: | :----------: | :-----------: | :--------: |
| **Applied Math** | Set Theory | Jacques Blum | 25 Avril 2024 | #SetTheory |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/ted_codd_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fted%5Fcodd%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FS24%2DWarmUp%20%2D%20One%2DTime%2DLink%2D20240425%5F094757%2DMeeting%20Recording%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview)

# Summary
*A union of a set ($\cup$) is used to combine elements from both sets. The opposite of this is an intersection ($\cap$) which says that an element must be contained in both sets. Both the union and intersection operators are commutative and associative. They are also distributive with each other. The complement of a set is all elements that are not contained within that set.*

# Key Takeaways
1. Both the union and intersection operators are <mark style="background: #FFB86CA6;">commutative and associative</mark>
2. The union and intersection operators are also <mark style="background: #FFB86CA6;">distributive</mark> with each other
	a. $A \cup (B \cap C) = (A \cup B) \cap (A \cup C)$
	b. $A \cap (B \cup C) = (A \cap B) \cup (A \cap C)$

# Definitions
- Commutative: Operation can be reversed and still hold true
	- $A \cup B = B \cup A$
	- $A \cap B = B \cap A$
- Associative: Order of grouping of operations does not change the outcome
	- Basically just the commutative property with more than two sets
	- $(A \cap B) \cap C = A \cap (B \cap C)$
	- $(A \cup B) \cup C = A \cup (B \cup C)$
- Disjoint: Two sets with no shared elements between them
	- $A \cap B = \emptyset$
- Partition: Two [[Logic and Set Theory|subsets]] that are disjoint and also when intersected, represent a full set
	- $A \cap B = E$ AND $A \cap B = \emptyset$
- Cartesian Product: All possible pairings that are created from the elements of two or more sets
	- A = {1, 2}; B = {3, 4}; A x B = {(1, 3), (1, 4), (2, 3), (2, 4)}

# Additional Resources
- [Commutative, Associative, Distributive Properties](https://www.varsitytutors.com/hotmath/hotmath_help/topics/commutative-associative-distributive-laws)

# Notes
## Union and Intersection
- $\cup$: Union ("OR") represents any element that is in <mark style="background: #FFB86CA6;">either</mark> set among two sets
	- Example: $A \cup B$ = $x \in A \:\:OR\:\: x \in B$ 
- $\cap$: Intersection ("AND") represents any element that is in <mark style="background: #FFB86CA6;">both</mark> sets among two sets
	- Example: $A \cap B$ = $x \in A \:\:AND\:\: x \in B$
- Both the union and intersection statements are commutative and associative
	![[Union and Intersection Venn Diagram.jpg]]

## Neutral Element
- Neutral element is what to either take the union or intersection with a subset to have the original set be the result as well
- Given that $A \subset E$,
	- The union of A and the empty set is A: $A \cup \emptyset = A$
	- The intersection of a subset and the whole is the subset: $A \cap E = A$

## Complementary Sets
- Any element "x" in a set E that is not a member of set A
	- $C_E A = {x \in E, x \notin A}$
- The complement of the empty set is the full set and the complement of the full set is the empty set: $C_E \emptyset = E$ AND $C_E E = \emptyset$
- The complement of the complement of a subset is the subset $C_E C_E A = A$
![[Complementary Sets Diagram.jpg]]