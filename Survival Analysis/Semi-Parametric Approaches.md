|      Course Name      |    Topic     |       Professor        |         Date          |    Tags     |
| :-------------------: | :----------: | :--------------------: | :-------------------: | :---------: |
| **Survival Analysis** | Cox PH Model | Anna Freni Sterrantino | 17 & 18 décembre 2025 | #Statistics |

[Class Video Link](URL)

# Summary
*A 3-4 sentence description of what was learned in italics*

# Key Takeaways
1. The Cox Proportional Hazards Model allows for testing of multiple groups, assessing continuous factors, and, in-general, performing regression analysis
2. Partial likelihood is necessary since failure times are [[Duration Data and Survival Analysis Overview|censored]]
3. With a lower hazard ratio, the treatment has fewer expected events and thus, a better survival rate than the control
4. A hazard ratio of 2 means that the treatment has twice the hazard of the control or a 100% increase - therefore, a worse survival

# Definitions
- Partial [[Constructing Estimators|Likelihood]]: Compare the hazard of subject $i$ to the [[Duration Data and Survival Analysis Overview|cumulative hazard]] of all subjects at-risk at time $j$
	- $\mathcal l(\beta) = \underset{j=1}{\overset{D}{\prod}}\dfrac{h_0(t_j)exp(x_{i_{(j)}}\beta)}{\underset{k \in R}{\sum}h_0(t_j) exp(x_k\beta)} = \underset{j=1}{\overset{D}{\prod}}\dfrac{exp(x_{i_{(j)}}\beta)}{\underset{k \in R}{\sum}exp(x_k\beta)}$
	 ![[Pasted image 20260117134320.png]]
- Hazard Ratio: The ratio comparing the hazard for treatment to control
	- $HR = \dfrac{h(t|X_1 = 1)}{h(t | X_1 = 0)} = \dfrac{h_0(t)exp(b_1)}{h_0(t)} = exp(b_1)$

# Additional Resources
- [Understanding Cox PH and Partial Likelihood (Medium)](https://medium.com/data-science/survival-analysis-optimize-the-partial-likelihood-of-the-cox-model-b56b8f112401)

# Notes
## Section 1
- Bullets on the actual content in question