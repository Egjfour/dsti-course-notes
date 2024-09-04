|        Course Name        |     Topic      |  Professor   |     Date      |   Tags    |
| :-----------------------: | :------------: | :----------: | :-----------: | :-------: |
| **Warm Up: Applied Math** | Real Functions | Jacques Blum | 26 Avril 2024 | #Calculus |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/ted_codd_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fted%5Fcodd%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FS24%2DWarmUp%20%2D%20One%2DTime%2DLink%2D20240426%5F095208%2DMeeting%20Recording%201%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Efab822b1%2D4dd8%2D4947%2Da9b5%2Db29beea35369)

# Summary
*[[Real Numbers, Real Sequences, and Limits|Limits]] of a function do not necessarily imply that the value of the function is the same at the given point. Limits are evaluated on a function for many different operations like summation, multiplication, and division. Limits also help us understand rates of variation.*

# Key Takeaways
1. If the limits of two functions have a certain order relation, then the functions themselves have an order relation
2. For [[Applications and Compositions of Sets|composed functions]], if the sense of variation is the same for each of the individual functions, then the composition is increasing. If they are different, then it is decreasing
3. It is <mark style="background: #FFB86CA6;">possible that f(x) does not actually exist or that it is different from the limit</mark> 

# Definitions
- Rate of Variation: Slope
- Sense of Variation: Sign of the slope

# Additional Resources
- [Limits (Openstax)](https://openstax.org/books/calculus-volume-1/pages/2-2-the-limit-of-a-function)
- [Limit Laws (Openstax)]()https://openstax.org/books/calculus-volume-1/pages/2-3-the-limit-laws

# Notes
## Real Functions
- A is the domain of definition of a function f
	- $x \in A \to f(a) \in \mathbb R$
- If the limits of two functions maintain an ordered relation, the functions themselves maintain that same ordered relation
	- $u_n \to L$ and $v_n \to M$ and $L <= M$, then $u_n <= v_n \forall n \in \mathbb R$
	- *Not* a strict inequality

## Operations on Limits
![[Pasted image 20240430155028.png]]

## Rate and Sense of Variation (Slope)
- Defined as the difference between the output of a function for two different inputs with respect to the difference of the inputs
	- $\frac{f(x_2) - f(x_1)}{x_2-x_1}$
	- If >= 0, then increasing (if > then strictly)
	- If <= 0, then decreasing (if < then strictly)
- Sense of variation can also be determined across operations of functions
	- For a function with an increasing sense of variation, multiplying by a positive constant results in an increasing function and multiplying by a negative constant results in a negative function
	- When adding, if the direction of the functions is the same, the addition will match. Direction is indeterminate if we are unsure
	- For products and compositions, if the sense of variation matches, the result is positive. If the two functions differ, the result is negative
	- If a function's sign is constant on the interval I, then 1/f(x) varies in the inverse direction


