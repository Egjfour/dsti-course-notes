|                             Course Name                             |    Topic    |     Professor      |      Date       |          Tags          |
| :-----------------------------------------------------------------: | :---------: | :----------------: | :-------------: | :--------------------: |
| **Foundations of Statistical Analysis and Machine Learning Part 1** | Probability | Christophe Bécavin | 14 janvier 2025 | #Statistics #SetTheory |

[Class Video Link](URL)

# Summary
*Probability is a function that represents the confidence that an event will happen among a set of all possible outcomes. Probability is heavily tied to set theory and many of the key properties of probability can be derived from set theory.*

# Key Takeaways
1. The frequentist definition of probability is based on the [[Convergence|law of large numbers]]
2. Probability is a [[Real Functions of a Real Variable|function]]
3. Countable infinite sets (real numbers) define probability on a boundary 

# Definitions
- Probability: The limit of the frequency of successes in a sequence of trials performed in the same conditions (frequentist definition) or a theoretical ratio (classical)
	- favorable outcomes / all outcomes
- Sample Space ($\Omega$): The universe of all possible outcomes
- Sigma Algebra ($\sigma$-algebra OR $\mathcal A$): A nonempty collection of subsets of $\Omega$ closed under complement, countable unions, and countable intersections
	- For a sample space $\Omega = \{H, T\}$ (outcomes of a coin toss), a sigma-algebra could be $\{\emptyset, \{H\}, \{T\}, \{H, T\}\}$, representing all possible events.
- Events: Sets A within the sigma algebra
	- $A \in \mathcal A$
- Almost Sure Event: If and only if $P(A) = 1$
- Almost Impossible Event: If and only if $P(A) = 0$

# Additional Resources
- [Frequentist vs Bayesian Probability](https://www.redjournal.org/article/S0360-3016(21)03256-9/fulltext)

# Notes
## Properties of Probability
- Sigma Algebra ($\sigma(\Omega) = \mathcal A: \sigma$-algebra of events)
	- Non-empty collection of subsets of the sample space $\Omega$
	- Properties
		- $A, B \in \mathcal A \implies A \cup B \in \mathcal A$: If A and B are both in the sigma algebra, the union is too
		- $A \in \mathcal A \implies A^C \in \mathcal A$: If A is in the sigma algebra, so is its complement
		- $A_i \in \mathcal A \implies U_{i=1}^\infty A_i \in \mathcal A$: The union of all elements in the sigma algebra is in the sigma algebra
- Probability: A function $P: \Omega \rightarrow [0, 1]$ representing the confidence level one has in the realization of the event with the following properties
	- $\forall A, A \in \mathcal A$, $P(A) \ge 0$: For all events in the sigma algebra, the probability of any event is greater than or equal to 0
	- $P(\Omega) = 1$: The probability of the sample space is 1
	- $A \cap B = \emptyset \implies P(A \cup B) = P(A) + P(B)$: For two [[Union, Intersection, and Complement of Sets|disjoint sets]] of events, <mark style="background: #FFB86CA6;">the probability of the union of the sets equals the sum of the probabilities of the individual events</mark>
	- $A_i \cap A_j = \emptyset \implies P(U_{i=1}^\infty A_i) = \sum_{i=1}^\infty P(A_i)$: For any set of disjoint subsets, the probability of the union of all the subsets is equal to the sum of all the individual probabilities
- A probability space is defined as $( \Omega, \mathcal A, P)$

## Probability Functions
- Three fundamental properties
	- $P(\emptyset) = 0$: The probability of the empty set in the sigma algebra is 0
	- $P(A) \le 1$: The probability of any event in the sigma algebra is at most 1
	- $P(A^C) = 1 - P(A)$: <mark style="background: #FFB86CA6;">The probability of the complement of an event equals 1 less the probability of the event</mark>
- Additional Properties
	- $P(B \cap A^C) = P(B) - P(A\cap B)$
		 ![[Pasted image 20250119121933.png]]
	 - $P(A \cup B) = P(A) + P(B) - P(A \cap B)$
		  ![[Pasted image 20250119121854.png]]
	- $A \subset B \implies P(A) \le P(B)$
		 ![[Pasted image 20250119121804.png]]
- For finite sets, $P(A) = \sum_{w_i \in A}p_i$
- For countable/[[Descriptive Statistics|discrete]] infinite sets, the same definition can be used
	- Set in [[Applications and Compositions of Sets|injection]] with $\mathbb N$
- For continuous infinite sets,
	- For a sample space based on $\mathbb R$, the definition of the probability will depend on the [[Random Variables|random variable]]