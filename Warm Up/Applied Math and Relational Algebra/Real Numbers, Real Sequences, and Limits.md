|        Course Name        |      Topic      |  Professor   |     Date      |   Tags    |
| :-----------------------: | :-------------: | :----------: | :-----------: | :-------: |
| **Warm Up: Applied Math** | Calculus Basics | Jacques Blum | 26 Avril 2024 | #Calculus |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/ted_codd_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fted%5Fcodd%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FS24%2DWarmUp%20%2D%20One%2DTime%2DLink%2D20240426%5F095208%2DMeeting%20Recording%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Eef1ba1d8%2D812e%2D4805%2D8779%2Dad303940aef5)

# Summary
*Real numbers include the entire set of rational numbers as well as irrational numbers that have no end like pi. When we have a sequence of these real numbers, they have certain properties such as accumulation points. As real sequence converge around a unique accumulation point, it is said that that sequence has a limit. Certain sequences are also monotonous meaning they only move in one specific direction (increasing or decreasing).*

# Key Takeaways
1. A bounded set of [[Relations of Sets|rational numbers]] ($\mathbb{Q}$) does not necessarily have a lowest upper bound
2. Real numbers ($\mathbb R$) that are not rational are called irrational numbers ($\pi, e, \sqrt{2}$)
3. There exists a total order relation in $\mathbb R$ that is Archimedean
4. If a point x, is in the set A ($x \in A$), then it is either an accumulation point or an isolated point
5. We say that $u_n$ converges to L (or that there's a limit, L) where as n progressively increases, the result of the function $u_n$ gets progressively closer to the value L
	a. $n \rightarrow \infty$ if $\forall \epsilon > 0, \exists N$ such that for $n > N, |u_n - L| < \epsilon$
6. If the limit of $u_n$ exists, then it is unique (<mark style="background: #FFB86CA6;">unicity of limits</mark>)
	a. This produces the necessary and sufficient condition for the convergence of a sequence (bounded with a unique accumulation value)
7. Two adjacent sequences converge to the same limit

# Definitions
- Archimedean: In a set, there exists an integer n such that for any two positive numbers (x and y), nx > y meaning that there is no infinitely large or infinitely small element
	- $\forall x, y \in \mathbb R^{+}, \exists n$ such that $nx > y$
- Accumulation Point: A point that always has an element of A within a neighborhood of any size
![[Pasted image 20240429140603.png]]
- Isolation Point: For a given point a in the set A, there exists an interval centered around a that does NOT contain any point in the set A
![[Pasted image 20240429135738.png]]
- Real Sequence: An [[Applications and Compositions of Sets|application]] of $\mathbb N$ to $\mathbb R$
	- $\forall n \in \mathbb N, u_n = f(n) \in \mathbb R$  


# Additional Resources
- [Real Numbers (Wikipedia)](https://en.wikipedia.org/wiki/Real_number#:~:text=In%20mathematics%2C%20a%20real%20number,can%20have%20arbitrarily%20small%20differences.)
- [Accumulation Point (Wikipedia)](https://en.wikipedia.org/wiki/Accumulation_point)
- [Isolation Point](https://en.wikipedia.org/wiki/Isolated_point)
- [Isolated and Accumulation Points Video](https://www.youtube.com/watch?v=9D-ZlJUnNZM&ab_channel=JoshuaHelston)
- [Theorem of Bolzano-Weirstrass](https://en.wikipedia.org/wiki/Bolzano%E2%80%93Weierstrass_theorem)

# Notes
## Real Numbers
- The real numbers ($\mathbb R$) exist as a superset of the rational numbers ($\mathbb Q$)
	- This superset has the property that **any** bounded set of $\mathbb R$ has a lowest upper bound
	- This gives the following relationship between the different types of numbers
	![[Pasted image 20240429134554.png]]
- Properties of Real Numbers
	- Between 2 arbitrary real numbers, there exists at least one rational and one irrational number
	- Any subset of $\mathbb R$ that is different from $\emptyset$ which is bounded has both a lowest upper bound and a highest upper bound
	- Interval Notation
		- ]a,b\[ (open)
		- \[a, b] (closed)
		- \[a, b\[ OR \]a, b\[ (semi-open)
- Operations of Real Numbers
	- Sum
		- Commutative and associative
		- Neutral element of 0 (x +0 = x)
		- Symmetric (x + (-x) = 0)
	- Product
		- Commutative, associate, and distributive
		- Neutral element of 1 (x * 1 = x)
		- Symmetric *except* for 0

## Accumulation and Isolated Points
- Accumulation Points
	- Let $E \subset \mathbb R, E \centernot = 0$
	- a is an accumulation point of E if $\forall \epsilon > 0, \exists x \in E, x \centernot = a$ such that $x \in ]a-\epsilon, a+\epsilon[$
	- Example: {1, 1/2, 1/3, ..., 1/n} $\rightarrow$ 0 is an accumulation point
- Theorem of Bolzano-Weierstrass
	- If $a \subset \mathbb R$, which is infinite and bounded, then a has at least one accumulation point
	- "Each inifinite bounded sequence in $\mathbb R^{n}$ has a convergent subsequence"
	- Infinite meaning that there are an <mark style="background: #FFB86CA6;">infinite number of elements</mark> and bounded meaning that there is an <mark style="background: #FFB86CA6;">upper and lower bound</mark>
- Isolated Point
	- $a \in A, \exists \epsilon > 0$ such that $]a - \epsilon, a + \epsilon \notin A$
	- There exists an interval centered around point a which is a member of set A that does not contain another member of set A
- Neighborhood of A
	- Any subset of $\mathbb R$ that contains an interval of center a
	- Consequence:
		- IF $A \subset \mathbb R, A$ bounded $\implies \exists sup.\:\: A \in \mathbb R$ (if A is a bounded subset of real numbers, there exists a supremum)
		- <mark style="background: #FFB86CA6;">If the supremum/infinimum is not in the set, then it is an accumulation point</mark>
		- If the supremum/infinimum is in the set, then it is either an accumulation or isolated point

## Real Sequences and Convergence (Limits)
- A real infinite sequence is an application from any number in the natural number set $\mathbb N$ (positive integers) that maps to the real number set $\mathbb R$
- As the input number to $u_n$ increases, we say that {$u_n$} converges to L or that there is a limit
	- $\lim{n\to\infty}u_n=L$
- Key Propositions of Limits
	- <mark style="background: #FFB86CA6;">If a limit of a sequence exists, it is unique</mark>
	- Any convergent sequence is bounded
	- If $u_n \to L$ and $v_n \to M$, then there exists N>0 such that n > N, $u_n < v_n$
		- The functions will preserve the same order relation as their limit
- Operations on Convergent Sequences
	- The sum of two convergent functions converges to the sum of their limits
	- If one function converges but not the other, the sum diverges
	- If both functions diverge, the sum is indeterminate
		- Can potentially "cancel out" and go to zero
	- The product of two convergent functions converges to the product of their limits
	- The quotient of two convergent functions converges to their quotient provided the divisor is not zero
	- The absolute value of a function converges to the absolute value of the limit
		- Relationship does not work in the inverse direction

## Monotonous and Adjacent Sequences
- Monotonous
	- A sequence that only moves in one direction as n increases
		- These sequences are allowed to be flat
		- A horizontal line is sais to be both monotonically increasing and decreasing (but not strictly)
	- If a monotonous sequence is increaseing and upper bounded, then it converges towards its lower upper bound. If it is increasing and not upper bounded, it converges towards $\infty$
	- We can also define this on an interval, $I, \forall x_1, x_2 \in I, x_1 < x_2 \implies f(x_1) <= f(x_2)$
- Adjacent
	- Two sequences are adjacent if $u_n$ is increasing and $v_n$ is decreasing and $u_n <= v_n, \forall n$ and $\lim_{n\to\infty} v_n - u_n = 0$
	- Adjacent sequences converge to the same limit
	- ![[Adjacent Sequences.jpg]]

## Accumulation Value of a Sequence
- a (in the set of real numbers) is an accumulation value of {$u_n$} if either
	- an infinite number of values of $u_n = A$
	- a is an accumulation point of the set {$u_n$}
- A convergent sequence has a unique accumulation value which is its limit
- A bounded sequence has at least one accumulation value
- Cauchy Criterion
	- A necessary and sufficient condition for the convergence of a sequence is that the absolute value of the difference between two image values given two arbitrary output values approaches zero as the pre-image values respectively approach infinity
	- $\forall \epsilon > 0, \exists N > 0$ s.t. for $n > N, p > N, |u_n - u_p| < \epsilon$