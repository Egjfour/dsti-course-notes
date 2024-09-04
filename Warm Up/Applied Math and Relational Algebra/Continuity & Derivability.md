|        Course Name        |                     Topic                     |  Professor   |     Date      |   Tags    |
| :-----------------------: | :-------------------------------------------: | :----------: | :-----------: | :-------: |
| **Warm Up: Applied Math** | Continuity and Derivability of Real Functions | Jacques Blum | 26 Avril 2024 | #Calculus |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/ted_codd_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fted%5Fcodd%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FS24%2DWarmUp%20%2D%20One%2DTime%2DLink%2D20240426%5F095208%2DMeeting%20Recording%201%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Efab822b1%2D4dd8%2D4947%2Da9b5%2Db29beea35369)

# Summary
*Real functions are continuous at a given point if they exist at that point and if their limit exists at that point. Continuity has important properties like the intermediate and mean value theorem which allows for chords to be created between the value of interest and another value. As these values get closer and closer, it is a derivative which gives the sense of variation at a particular point. If we take the derivative of the derivative, we are able to see the convexity of a function.*

# Key Takeaways
1. The conditions for continuity are that both the result of the function exists and that the limit of the function as it approaches the point in question exists
2. If a function, f, is continuous on \[a,b\], then f(x) is bounded on the continuous image of a segment \[a,b\] defined by \[m, M] where m = min(f(x)) and M = max(f(x)) on \[a, b]
3. If a function is derivable at a given point, it is continuous at that point as well
4. The<mark style="background: #FFB86CA6;"> second derivative is what allows us to identify if a function is convex</mark>

# Definitions
- Intermediate Value Theorem: Any point between f(a) and f(b) exists for a [[Real Functions of a Real Variable|continuous function]]
- Rolle's Theorem: If f is defined and continuous on \[a, b] and derivable on ]a, b\[, and f(a) = f(b), then there are places where the derivative is 0
- Mean Value Theorem: If f satisfies Rolle's Condition , then the slope of the chord between f(a) and f(b) is a tangent line to at least one other point
	- f satisfies Rolle's $\implies c \in ]a,b[$ s.t.  $f'(c) = \frac{f(b) - f(a)}{b-a}$
- Discontinuity of First Species (First Kind): A function where the left-hand and right-hand limits both exist but are not equal

# Additional Resources
- [Continuity Chapter (Openstax)](https://openstax.org/books/calculus-volume-1/pages/2-4-continuity)
- [Chain Rule (StatQuest)](https://www.youtube.com/watch?v=wl1myxrtQHQ&ab_channel=StatQuestwithJoshStarmer)

# Notes
## Continuity
- Both the function and it's limit exist at a given point
- <mark style="background: #FFB86CA6;">If f is monotonous, then there can only exist a discontinuity of first species</mark>
- Continuation of a function by continuity
	- Involves creating a new function g(x) such that g(x) = f(x) except at the point of discontinuity. At that point, we define g(x) as L (the limit)

## Derivability
- Derivative at a point
	- Define f in a neighborhood of $x_0$ and find the [[Real Functions of a Real Variable|sense of variation]] given that point
	- $f'(x) = \lim_{x \to x_0} \frac{f(x) - f(x_0)}{x - x_0}$ (slope of the chord between x and $x_0$)
- Operations on the derivative
	- ![[Pasted image 20240430163020.png]]
- Sense of Variation
	- On a monotonic function,
		- If f is increasing on $I \implies f'(x_0) >= 0$
		- If f is decreasing on $I \implies f'(x_0) <= 0$

