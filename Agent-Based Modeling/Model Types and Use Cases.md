
|       Course Name        |      Topic      |    Professor     |        Date        | Tags |
| :----------------------: | :-------------: | :--------------: | :----------------: | :--: |
| **Agent-Based Modeling** | Model Hierarchy | Gregory Bobashev | 8-9 Septembre 2025 |      |

# Summary
*Models are representations of a phenomenon occurring in the real world. There are many techniques to build models at different levels of granularity and complexity. Agent-based modeling is used for the highest complexity situations where we need individual-level granularity. These models are defined by individual entities making decisions and acting within an environment.*

# Key Takeaways
1. Agent-based models are particularly useful in high interaction, high complexity settings
2. It's generally preferable to consider models as a state change from the current state when working in an agent-based framework
3. Homogenous mixing is a key assumption of agent-based models
4. [[Conditional Probability and Independence|Bayesian modeling]] is the foundational approach of agent-based modeling
5. Often, people can accept and plan for risk. Modeling should help reduce uncertainty
6. All of these models are simplifications and none (even ABMs) are considered [[Data Assimilation Overview|digital twins]]

# Definitions
- Model: A representation/essence of a physical phenomenon. A "simplified summary" intended to promote understanding
- Agent: Computer objects that are defined by states, transitions between the states and rules of interaction between each other and environment
- Monte Carlo Simulation: Use a model to generate many possibilities of $\hat Y$ and calculate characteristics on this sample
- Markov Models: The transition from the current state to the next only depends on the knowledge of the current state
- Microsimulation: Models which have individual entities which pass through stages/compartments
	- Queueing system
- Agent-Based Model: Individual entities which can make decisions and interact with each other and/or their environment
- Homogenous Mixing: Everyone (each agent) has an equal chance of being matched with anyone (any other agent)
- Jensen's Inequality: For a nonlinear [[Convexity|convex]] function, the function of the mean is less than or equal to the mean of the function (opposite if concave)
- Decision Models: Models (statistical, Markov, ABM, optimization, etc) estimate effects of various choices and determine the set of downstream consequences

# Additional Resources
- [ABM Introduction Book](http://www.railsback-grimm-abm-book.com/)

# Notes
## Model Hierarchy and Methodologies
- Two main branches: population-averaged and individual-based
	- Important to have both since $\mathbb E[f(X)] \ne f(\mathbb E[X])$ if $f$ nonlinear (Jensen)
	 ![[Pasted image 20250920182653.png]]
- Model Methodologies
	- Models can be solved analytically (known theorems/simplifications and/or approximations like [[Taylor Series|Taylor Expansion]]) or run using Monte Carlo simulation
	- As models become increasingly complex, simulation becomes more attractive as analytical solutions are computationally infeasible
## Population-Averaged Models
- Statistical Models
	- Often is useful to think of these models in a Bayesian context
	- Instead of taking the model as ground truth
		- Example (simple linear model): $y_{new} = \beta_0 + \beta_1 x_{new}$
	- We look at the model as a change
		- $y_{new} = y_{old} + \beta_1 (x_{new} - x_{old})$
- Markov Models
	- Defined as a system which can exist in multiple, mutually exclusive states with transition probabilities between the states
	- These transition probabilities to the next state are <mark style="background: #FFB86CA6;">based only on the value of the current state</mark>
	- Generally, discretization of time steps is done and rates of change from state to state are analyzed as a proxy for transition probabilities
		- Probability: $X_{n+1} = AX_n \Rightarrow \sum A_i = 1$
		- Rate: $\dfrac{\partial X}{\partial t} = AX(t) \Rightarrow \sum A_i = 0$
- System Dynamics
	- The key difference between these models and Markov models is that <mark style="background: #FFB86CA6;">system dynamics models have feedback loops</mark> based on unintended consequences that are felt with some delay
	 ![[Pasted image 20250920184138.png]]
- These models tend to suffer from the <mark style="background: #FFB86CA6;">bias of early averaging</mark>
## Individual-Based Models
- Microsimulation Models
	- Entities are passively moving through stages/compartments
	- Advantages
		- Can be easier to program since we only <mark style="background: #FFB86CA6;">program first principles</mark>
		- Use equations and rules
		- Handle broad stochasticity with summaries and rules
- Agent-Based Model
	- Individuals operate within a system and make decisions after evaluating their current state
	- Examples
		- Segregation Model
		- Flock of Birds
		- Wealth distribution
	- If agents are passive the model is just a microsimulation (e.g. discrete event)
	- Rules in this model can be
		- [[Computer Systems Basics|Deterministic]]: If agent A sees food, he eats it
		- Stochastic: If agent A sees food, he flips a coin and if it's heads, then he eats it
		- Simple: At each timestep, move forward by 1 meter
		- Complex Logical: If agent A sees food he checks if he is hungry, if he is not hungry passes by, if hungry, inspects food quality, and if the quality is better than average eats it
	- Agents in a model can
		- Make decisions based on rules
		- Be adaptive
		- Have several state charts and internal dynamics
		- Have [[Existing Vocabularies|social networks]]
		- Have a life of their own (be agents)
	- With agent-based models, we <mark style="background: #FFB86CA6;">create virtual societies</mark>
- Generally a microsimulation model can be aggregated to an equivalent system dynamics model
	- But to build an ABM from a system dynamics model, the assumption of homogenous mixing is required among potentially others
## Building and Using Models
- Model purposes
	- Models can be used to make decisions, predict values, identify relationships, or implement theory
	- Models help us handle the unknown and complex structure of the real world where decisions have a delay and high cost of error
- Decision Modeling
	- Developed as an analytical framework to <mark style="background: #FFB86CA6;">make decisions under conditions of uncertainty</mark>
	- Two main frameworks
		- Predictive: Analyses and explanations of how decision makers actually make decisions
			- Answers the question of "what would they do in this circumstance"
		- Prescriptive: Analyses of how decision makers should make decisions optimally
			- We choose an outcome criteria and optimize to it
- Model Calibration
	- Data is needed to calibrate model parameters/settings and establish rules
	- Different parameter spaces which all need to be calibrated
		- Background space: what is given
		- Situation space: what are variable factors
		- Decision space: what can we potentially do
	- Collected from primary study data. literature reviews, expert opinion, etc
	- Typically, intermediate split values aren't known, but we do know intermediate probabilities and end values so we can take the average out/fold back approach
		 ![[Pasted image 20250920202107.png]]
	- Most importantly, we test our assumptions with the model and experts who can evaluate our setup
		- This is why [[ODD Protocol and Documentation|documentation]] is so essential so we can explain and test our assumptions