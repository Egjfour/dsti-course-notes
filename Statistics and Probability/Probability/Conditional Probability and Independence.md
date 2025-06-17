|                             Course Name                             |    Topic    |     Professor      |        Date        |          Tags          |
| :-----------------------------------------------------------------: | :---------: | :----------------: | :----------------: | :--------------------: |
| **Foundations of Statistical Analysis and Machine Learning Part 1** | Probability | Christophe Bécavin | 14-15 janvier 2025 | #Statistics #SetTheory |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/johnny_najjar_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fjohnny%5Fnajjar%5Fdsti%5Finstitute%2FDocuments%2FRecordings%281%29%2FA24%20%2D%20Common%20Link%20%2D%20DS%2DDE%2DDA%2D20250114%5F095131%2DMeeting%20Recording%201%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Eb0f1ed8c%2D56ad%2D47f3%2D8945%2D9e7c7c39a16f)

# Summary
*Conditional probability allows us to understand how events are related to one another and determine if knowledge of the outcome of one event can help us make more informed decisions regarding other events. Events in which having knowledge of one does not provide more information are independent and this can be measured by comparing the joint probability to the marginal probability of the event.*

# Key Takeaways
1. $P(A|B) = P(A) \hspace{2mm}\mathrm{iff}$ A and B are independent
2. $P(A|B) \ne P(B|A)$
3. Bayes Theorem: $P(A|B) = \dfrac{P(B|A) * P(A)}{P(B)}$
# Definitions
- Independence: Knowledge of the outcome of one event gives no information about another
	- $P(A \cap B) = P(A) * P(B)$
- Incompatibility: Two events that cannot occur together
	- $A \cap B = \emptyset$
- Joint probability: The probability of two events occurring together (intersection)
	- $P(A \cap B)$
- Marginal Probability: The sum of the joint probabilities for an event A across all possibilities B
	- $P(A) = \sum_i P(A \cap B_i)$
- Sensitivity = True Positive / (True Positive + False Negative)
	- "Proportion of people with the disease who test positive"
- Specificity = True Negative / (True Negative + False Positive)
	- "Proportion of people without the disease who test negative"

# Additional Resources
- [Bayes Theorem](https://www.geeksforgeeks.org/bayes-theorem/)
- [Sensitivity and Specificity (Video)](https://www.youtube.com/watch?v=psELBu7muNY)

# Notes
## Conditional Probability
- $P(A|B) = \dfrac{P(A \cap B)}{P(B)}$
	- The probability of event A given a specific known outcome of event B equals the intersection of events A and B divided by the marginal probability of B
	- Probability of event B must be > 0
- The reversal of the conditions does not hold $P(A|B) \ne P(B|A)$
	- Example: Diagnosing HIV
		- Outcome: E = test is positive; $A_1$ = has HIV; $A_2$ = does not have HIV
		- $A_1 \cup A_2 = \Omega$ and $A_1 \cap A_2 = \emptyset$
			- Partition of the sample space
		- $P(E|A_1) = 0.999$: Probability of a positive test given that you have HIV
			- Sensitivity
		- $P(E|A_2) = 0.001$: Probability of a positive test given that you do not have HIV
			- 1 - Specificity
		- Since $P(A_1|E) \ne P(E|A_1)$, there is not a 99.9% chance of HIV due to the positive test
		- Instead, $P(A_1 | E) = \dfrac{P(E|A_1)*P(A_1)}{P(E)} = \dfrac{P(A_1 \cap E)}{P(E)}$
			- We don't know $P(A_1 \cap E) = P(E \cap A_1) = P(E|A_1)*P(A_1)$ and can get $P(A_1)$ as the base rate of the disease 0.01% in a developed Western country
		- $P(E)$ can be found as $P(E \cap A_1) + P(E \cap A_2)$ because $A_1$ and $A_2$ form a partition
		- So, $P(A_1|E) = \dfrac{P(E|A_1)*P(A_1)}{P(E \cap A_1) + P(E \cap A_2)} = \dfrac{99.9 * 0.01}{99.9 * 0.01 + 0.01 * 99.9} = 50$
		- Thus, having a positive result means that there is a 50% chance of having HIV
		 ![[Pasted image 20250119140751.png]]
- Bayes Theorem
	- <mark style="background: #FFB86CA6;">We are multiplying the inverse conditional probability by the ratio of the marginal probabilities to effectively do a "change of base"</mark>
	- Since, $P(A|B) \ne P(B|A)$, we instead calculate $P(A|B) = \dfrac{P(B|A) * P(A)}{P(B)}$
## Independence
- Prisoner example (Independent):
	- 3 prisoners are on death row and one is pardoned at random. The warden randomly chooses between prisoners B and C and tells prisoner A that B will not be executed. Prove that this provides no additional information to Prisoner A
	 ![[Pasted image 20250119134027.png]]
- Monte Hall Problem (Dependent):
	- You choose a door among three randomly where one wins and the other two lose. You are then shown one losing door. Prove that you can increase the probability of winning by changing doors.
	 ![[Pasted image 20250119134051.png]]
- More than 2 events
	- All events are mutually independent iff for any collection {$A_1, ..., A_n$}, we have $P(\cap_i^n A_i) = \prod_{j\in[1,k]}P(A_i)$
	- The intersection of all the probabilities is equal to the product of all marginal probabilities
	- A set of events {A, B, C} might be pairwise independent but not be jointly independent as a triplet