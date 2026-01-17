|      Course Name      |     Topic     |       Professor        |       Date       |    Tags     |
| :-------------------: | :-----------: | :--------------------: | :--------------: | :---------: |
| **Survival Analysis** | Survival Data | Anna Freni Sterrantino | 17 décembre 2025 | #Statistics |

[Class Video Link]([URL](https://dstisas.sharepoint.com/sites/RecordingsArchive/_layouts/15/stream.aspx?id=%2Fsites%2FRecordingsArchive%2FShared%20Documents%2FA24%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20251217%5F085734%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Eb7179cf8%2D55bf%2D4050%2Da1fc%2D1c150c62f8ef))

# Summary
*Survival analysis is the modelization of duration data which features as its outcome, a time to event. Such data has additional complexities to model since it also often has censoring. The goals of working with this data are to try to understand the survival and hazard functions and any factors which contribute to them.*

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
- Non-Informative Censoring: Censoring time is not related to the unobserved survival time
	 ![[Pasted image 20260117081855.png]]

# Additional Resources
- [Overview in R (great resource)](https://stats.oarc.ucla.edu/wp-content/uploads/2025/02/survival_r_full.html)
- [Survival Analysis (Python)](https://scikit-survival.readthedocs.io/en/stable/user_guide/00-introduction.html)
- [Survival Analysis Overview (NIH)](https://pmc.ncbi.nlm.nih.gov/articles/PMC2394262/)

# Notes
## Duration Data
- Duration data is the <mark style="background: #FFB86CA6;">strictly non-negative</mark> and often partially recorded
- The <mark style="background: #FFB86CA6;">outcome is time to event</mark> and each unit has an outcome and a time value associated to it
- Relevant variables
	- $T$: A [[Random Variables|random variable]] for a person/unit survival time
	- $t$: Specific value for the random variable $T$
	- $d$ indicator if the observation is censored
		- $d=0$ if censored
		- $d=1$ if the event occurred within the study
- The survival plot (above) shows this data aggregated to the entire population
	- Time is on the x-axis and the proportion of remaining observations is on the y axis
- In R, duration data is created using function `Surv({time}, {status})` with `status` referring to censoring
- Goals of survival analysis
	- Estimate the survival and/or hazard functions
	- Compare the functions
	- Asses the relationship of other variables with the survivor and hazard functions
## Survival Function
- A mapping of time to the probability of still being in the study at that time
	- $S(t) = Pr(T \gt t)$
- The [[Distributions of Probability and Random Variables|CDF]] is $F(t) = Pr(T \le t) = 1 - S(t)$
- The [[Distributions of Probability and Random Variables|PDF]] is $f(t) = -S'(t)$
- Key characteristics
	- All subjects survive the first moment
		- $S(0) = 1$
	- <mark style="background: #FFB86CA6;">All subjects fail after infinite time</mark>
		- $S(\infty) = 0$
	- The survival function is a probability and is thus bounded between 0 and 1 inclusive
		- $S(t) \in [0, 1]$
- Median and Mean
	- The median is the time at which exactly half the population is expected to still be surviving
		- $S^{-1}(0.5)$
	- The mean time is the [[Moments of Random Variables|expectation]] of the random variable
		- $\mu = \mathbb E[T] = \int_0^{\infty}tf(t)dt = \int_0^{\infty}S(t)dt$
	- These measures both include censored subjects in their estimation
- The descriptive statistics of survival data can be calculated in R using `survfit({Surv} ~ {factors}, data = df)`
	- These can be described using function `tbl_survfit`
- Example: Getting Median Survival Time in R
	 ![[Pasted image 20260117080845.png]]
- Common Survival Distribution - [[Distributions of Probability and Random Variables|Exponential]]
	- $S(t) = e^{-\lambda t}$
	- $f(t) = \lambda e^{-\lambda t}$
	- Median: $\log(2)/\lambda$
	- Mean: $1/\lambda$
	- This distribution has constant hazard
		- $h(t) = \lambda$
		- Thus, $H(t) = \lambda t$
	- This is <mark style="background: #FFB86CA6;">considered a baseline approach</mark> since it proposes constant hazard
## Hazard Function
- The hazard function is the [[Functions and Derivatives of Functions|derivative]] of the event happening at time $t$
	- Represents the risk of the event happening given survival up until this point
	- $h(t) = \underset{\delta \to 0}{lim}\dfrac{Pr(t \lt T \lt t+\delta | T \gt t)}{\delta}$
- Often, the <mark style="background: #FFB86CA6;">cumulative hazard function is more impactful</mark> to understand
	- $H(t) = \int_0^t h(u)du$
	- This is often what modeling methodologies seek to fit
	- This expresses how much hazard/risk a subject has accumulated over time
- Relationships with the survival function
	- $h(t) = \dfrac{f(t)}{S(t)}$
	- $S(t) = exp(-H(t))$
- An increasing hazard function means that more events are expected over time and survival is expected to decrease more rapidly
	 ![[Pasted image 20260117081526.png]]
- In R, we can quickly switch from a survival to a hazard function using the `epi.insthazin` function
## Censoring
- A core assumption of survival analysis methods is non-informative censoring
- If this assumption is violated, it can bias the estimation of survival/hazard
- Examples:
	- Oldest subjects drop out of study of time to death after surgery (Oldest might have shortest survival times, so survival estimates might be <mark style="background: #FFB86CA6;">biased upward</mark>)
	- Travel-loving subjects drop out of study of time to first marriage (Travel-loving subjects may delay marriage to travel more and have longer survival times, so survival estimates might be <mark style="background: #FFB86CA6;">biased downward</mark>)