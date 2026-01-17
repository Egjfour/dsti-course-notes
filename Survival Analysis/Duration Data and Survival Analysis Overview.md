|      Course Name      |     Topic     |       Professor        |       Date       |    Tags     |
| :-------------------: | :-----------: | :--------------------: | :--------------: | :---------: |
| **Survival Analysis** | Survival Data | Anna Freni Sterrantino | 17 décembre 2025 | #Statistics |

[Class Video Link](URL)

# Summary
*A 3-4 sentence description of what was learned in italics*

# Key Takeaways
1. The goal of survival analysis is to define the survival and/or hazard functions
2. Mean and median survival consider the censored subjects who left the study in the middle
3. The [[Confidence Intervals of Estimators|confidence interval]] (and thus uncertainty) of the survival function is increasing over time
4. The cumulative hazard function is strictly increasing
5. The exponential survival distribution has a constant hazard

# Definitions
- Survival Analysis: The study of survival times and the factors that influence them
	- How much longer does a new drug increase patients' lifespans
- Censoring: Subjects who survive beyond the study (right censoring) or who withdraw
- Median Time: The time $t$ at which 50% of the population is expected to still be surviving
	- $t: S(t) = 0.5 - S^{-1}(0.5)$
- Survival Function ($S(t)$): The percentage of the initial population still in the study at a time $t$
	- $S(t) = Pr(T \gt t)$
	- Example: Time taken to eat a package of biscuits![[Pasted image 20260117072651.png]]
- Hazard Function ($h(t)$): Potential risk of having an event given you've survived until time $t$
	- Instantaneous rate of the event happening
	- $h(t) = \underset{\delta \to 0}{lim}\dfrac{Pr(t \lt T \lt t+\delta | T \gt t)}{\delta}$
- Cumulative Hazard Function ($H(t)$): How much hazard a subject has accumulated over time up to time $t$
	- $H(t) = \int_0^t h(u)du$

# Additional Resources
- Name the hyperlink in brackets then outside the brackets put the URL in parens

# Notes
## Duration Data
- Bullets on the actual content in question