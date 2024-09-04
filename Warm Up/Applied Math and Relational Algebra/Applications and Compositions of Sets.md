|        Course Name        | Topic |  Professor   |     Date      |    Tags    |
| :-----------------------: | :---: | :----------: | :-----------: | :--------: |
| **Warm Up: Applied Math** | Sets  | Jacques Blum | 25 Avril 2024 | #SetTheory |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/ted_codd_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fted%5Fcodd%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FS24%2DWarmUp%20%2D%20One%2DTime%2DLink%2D20240425%5F094757%2DMeeting%20Recording%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview)

# Summary
*Applications are simply functions that allow us to map a value in one set to a value in another set. These applications can also be composed with each other and certain relationships between input and output sets (injectivity, surjectivity, and bijectivity) have important and interesting properties. Bijections (applications which are one-to-one between input and output) are able to be defined in the inverse as well. Sometimes, we need to apply restrictions to applications to make them bijective.*

# Key Takeaways
1. Identifying injectivity/surjectivity/bijectivity is a <mark style="background: #FFB86CA6;">triplet of considerations</mark> that involves the function itself, the departure space, and the arrival space
2. A bijection is a one-to-one relationship (much like a [[Data Management & Relational Algebra|primary key]])
3. $f^{-1}$ is the <mark style="background: #FFB86CA6;">reciprocal bijection ("Inverse Function")</mark>
4. An injection from E to F is a bijection from E to f(E)
	a. Since we restrict the application result set

# Definitions
- Application: Given two sets E and F, an application f from E to F is defined as a link or association to each element of a in E an element b in F such that b = f(a)
	- This is just a fancy way to say function. The application f is a function that maps from a domain E to a range F
- Image: The result of an application -- b is the image of a
- Antecedent: The input value for the application -- a is the antecedent of b
- Injection: A function where any element of a result set F has at most one antecedent in the input set E
- Surjection: A function where the entire range of possible inputs maps to the full output range
	- f(E) is the full set F
- Bijection: A <mark style="background: #FFB86CA6;">one-to-one relationship</mark>. Any function that is both injective and surjective

# Additional Resources
- [Image - Mathematics (Wikipedia)](https://en.wikipedia.org/wiki/Image_(mathematics))
- [Injection, Surjection, and Bijection (Wikipedia)](https://en.wikipedia.org/wiki/Bijection,_injection_and_surjection)
- [Restriction (Wikipedia)](https://en.wikipedia.org/wiki/Restriction_(mathematics))

# Notes
## Applications and Images
- Applications are functions that go from one set (inputs) (E) to another set (outputs) (F)
- Images of Subsets
	- An image of a subset will result in a subset
	- f(A) = {$b \in F$ such that $b = f(a), a \in A$}
- The pre-image is the reciprocal/inverse image of $B \subset F$
	- $f^{-1}[B]$ = {$a \in E$ such that b = f(a)}
	- "The reciprocal image of F, B, is the set of all elements 'a' in E such that f(a) is in the set B"
	- Essentially, all elements of E that map to F

## Injectivity/Surjectivity/Bijectivity
![[Pasted image 20240425220020.png]]

## Application Composition
- Composition describes passing the result of one function onto the next to obtain the final result
- Given sets F, E, and G, with elements a, b, and c; there exists an element a in E such that b = f(a) in set F such that c = g(b) in set G
	- $\forall a \in E \rightarrow b = f(a) \in F \rightarrow c = g(b) \in G$
![[Composition of Applications.jpg]]
- Function composition also has [[Logic and Set Theory|associativity]] as a property
	- $h \circ (g \circ f) = (h \circ g) \circ f$
	- Derived from fact that *injection $\circ$ injection = injection

## Reciprocal Bijection
- "Inverse function": For all elements in the result set (F), there is a corresponding value in the input set (E) $\forall b \in F, \exists !\: a$ such that b = f(a), so a = $f^{-1}(b), \forall b \in f$
- Special Properties
	- The inverse composed with the original is the identity of the input set (E) $f^{-1} \circ f = ID_E$
	- The original composed with the inverse if the identify of the output set (F) $f \circ f^{-1} = ID_F$
	- The inverse of the inverse is the original $(f^{-1})^{-1} = f$
	- <mark style="background: #FFB86CA6;">The inverse of the composition is the composition of both inverse functions switched</mark>
		- $(g \circ f)^{-1} = f^{-1} \circ g^{-1}$

## Restriction of Applications
- A new application (p) which chooses a smaller domain than the original application (function)
	- If $E \rightarrow^{f} F$ and A $\subset E$, then p(x) = f(x), $\forall x \in A$
	- If f is an application of E to F and A is a subset of E, then the restricted application, p, is equal to the full application, f, where the input value, x, is in the set A
- The original application (f) is said to extend the restriction
- This is useful when we want to examine a function that, in its entire domain, has no inverse like $y = x^{2}$