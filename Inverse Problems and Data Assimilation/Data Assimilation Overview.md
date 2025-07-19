|                Course Name                 |       Topic       |   Professor   |      Date       |   Tags    |
| :----------------------------------------: | :---------------: | :-----------: | :-------------: | :-------: |
| **Inverse Problems and Data Assimilation** | Data Assimilation | Didier Auroux | 11 juillet 2025 | #Calculus |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/blaise_pascal_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fblaise%5Fpascal%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20250711%5F132853%2DMeeting%20Recording%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0%3D&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0=&ga=1)

# Summary
*Data assimilation applies an observations of data from a data-independent model and solves the inverse function to recover $x$. The relevance of different components/functions of the model will change based on the situation, so the first step of building a data assimilation model is to calibrate the parameters.*

# Key Takeaways
1. The model is never data driven in data assimilation models. It is independent of the data 
2. Taking the derivative of something noisy shouldn't be done because local slopes are amplified
3. When there are data problems, we either exclude or update the system if the error is systematic. For measurement errors, we can adjust observations

# Definitions
- Data Assimilation: Assume a non data-driven model with observations of the system. Data assimilation combines these [[Conditional Probability and Independence|independent]] sources of information to solve the [[Direct and Inverse Problems|inverse problem]] and recover $x$
- Chaos Theory (Butterfly Effect): A small perturbation can have a very large effect

# Additional Resources
- [Lorenz System](https://en.wikipedia.org/wiki/Lorenz_system)

# Notes
## Process Overview
- First calibrate parameters to create a digital twin then use it to recover $x$
- We use the same model for all situations at all scales, but parameters must be recalibrated for the given relevant state
	- Influence of Earth's rotation is higher for climate-level and entire year predictions versus local forecasts
- Once the twin experiment is designed, we simulate the outcome
	- A "true" state which is not known in reality
- Then fit observations to actual data
## Data Assimilation Models
- Mainly physical phenomenon like traffic flows and using obstacles to redirect
- Models likely need to be updated (change equations) based on which situation it is being applied
- The Lorenz model is the most chaotic model and was the first to predict the atmosphere
	- Nonlinear based on $x,y,z$ and depending on $\sigma, \rho, \beta$
## Observations
- Come from many heterogenous sources
	- For weather: satellites, ships, planes, ballons, etc.
- Because of noise, sometimes having too much data is worse
- It is impossible to observe every element of a system at all times
	- Data assimilation must extrapolate in time, space, or both