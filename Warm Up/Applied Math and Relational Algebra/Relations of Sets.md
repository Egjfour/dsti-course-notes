|        Course Name        |     Topic     |  Professor   |     Date      |    Tags    |
| :-----------------------: | :-----------: | :----------: | :-----------: | :--------: |
| **Warm Up: Applied Math** | Set Relations | Jacques Blum | 25 Avril 2024 | #SetTheory |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/ted_codd_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fted%5Fcodd%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FS24%2DWarmUp%20%2D%20One%2DTime%2DLink%2D20240425%5F094757%2DMeeting%20Recording%201%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview)

# Summary
*A binary relation is a partition of a cartesian product of two sets. These relations (a, b) can be defined according to the relationship seen between their values with rules (R). These rules ultimately define whether the relation is equivalence or an ordered relation. The only difference between the equivalent and ordered relations is that the equivalent relation is symmetric about the first bisector (45-degree line).*

# Key Takeaways
1. The only difference between an equivalence and order relation is that an equivalence relation is symmetric about the first bisector and the order relation is not
2. Equivalence classes are either [[Union, Intersection, and Complement of Sets|disjoint]] or identical
3. An order relation that is either $aRb$ or $bRa$ $\forall (a,b) \in E^{2}$ is considered total

# Definitions
- Binary Relation: A [[Logic and Set Theory|partition]] of $E^{2}$ in two [[Logic and Set Theory|complementary subsets]]
- First Bisector: The 45-degree line through the origin
- Bounded: A set that has both a lower (infinimum) and upper (supremum) bound
- <mark style="background: #FFB86CA6;">Relative Numbers: Integers</mark>
- Omega ($\omega$): The universe of all elements from the result of a set
	- {$\omega$: $\omega \in \mathbb Z$} acts as a lambda function to generate the set of all integers

# Additional Resources
- [Equivalence and Order Relations (Libretexts)](https://math.libretexts.org/Courses/Mount_Royal_University/MATH_2150%3A_Higher_Arithmetic/2%3A_Binary_relations/2.2%3A_Equivalence_Relations%2C_and_Partial_order)
- [Symmetric Relations (Wikipedia)](https://math.libretexts.org/Courses/Mount_Royal_University/MATH_2150%3A_Higher_Arithmetic/2%3A_Binary_relations/2.2%3A_Equivalence_Relations%2C_and_Partial_order)
- [Infinimum and Supremum (Wikipedia)](https://en.wikipedia.org/wiki/Infimum_and_supremum)
- [Equivalence Classes (Wikipedia)](https://en.wikipedia.org/wiki/Equivalence_class)
- [Types of Numbers (Wikipedia)](https://en.wikipedia.org/wiki/List_of_types_of_numbers)

# Notes
## Binary Relations
- A partition between the [[Logic and Set Theory|cartesian product]] ($E^{2}$) of two sets that results in in two complementary subsets
	- $aRb \iff (a, b) \in G$
	- $a \centernot R b \iff (a, b) \in C_{E^{2}} G$
	- "All elements that abide by relation R are in the subset G of $E^{2}$. Those that do not are in the complement of G within $E^{2}$"
	![[Binary Relation Graph.jpg]]
- <mark style="background: #FFB86CA6;"><b>Possible</b></mark> Properties
	- Reflexivity: The first bisector is included in the rule (G)
		- $aRa, \forall a \in E$ : any number in the set E satisfies the rule when comparing with itself
		- Example: less than or equal to
	- Symmetry: The rule set G is symmetric with respect to the first bisector
		- $aRb \implies bRa$
		- Example: Equal to
	- Anti-symmetry: The rule set G does not work in both directions
		- IF $aRb \implies bRa, a=b$ 
		- "If we assume the rules can be reversed, then a = b which is false"
		- Less than or equal to
			- a = 4 and b = 5; 4 <= 5 is true but 5 <= 4 is false
		 ![[Pasted image 20240427184708.png]]
	- Transitivity
		- If $aRb$ and $bRc \implies aRb$

## Equivalence Relations
- These are binary relations that are Reflexive, Symmetric, and Transitive <mark style="background: #FFB86CA6;">(RST)</mark>
- This is a set of elements that are related to the class (a) by a rule (R)
	- $C_a$ = {$x \in E$} such that $xRa$
- Because equivalence classes are either disjoint or identical, they form a partition of the set (E)
	- This set is noted $\frac{E}{R}$ = {$C_a$}
- The equivalence classes for the set of relative numbers ($\mathbb{Z}$)(integers) is the set of rational numbers ($\mathbb{Q}$)
	- $(p,q) \in \mathbb{Z} x \mathbb{Z}^{*}$
	- $(p,q)R(p^{'}, q^{'} \iff pq^{'}) = p^{'}q \iff \frac{p}{q} = \frac{p^{'}}{q^{'}}$
		- This ultimately shows how we get fractions

## Order Relations
- These are binary relations which are reflexive, anti-symmetric, and transitive <mark style="background: #FFB86CA6;">(RAT)</mark>
- Essentially, these are relations where the elements are able to be ranked against each other
	- "X is larger/stronger/faster than y"
- Any set with this relation is partially-ordered. If the relation exists for all elements, it is totally ordered (either the initial rule or contraposition is true)
	- In a totally ordered set, a is an upper bound if $xRa, \forall x \in A$

## Subsets and Equivalence
- Given 2 sets, A and B
	- $A \subset B \Leftrightarrow (\omega \in A \implies \omega \in B)$
		- A is included in B and/or A is a subset of B
	- $A=B \Leftrightarrow A \subset B$ and $B \subset A$
		- A is equal to B, so both are a subset of each other

