|       Course Name        |     Topic     |     Professor     |            Date             | Tags |
| :----------------------: | :-----------: | :---------------: | :-------------------------: | :--: |
| **Agent-Based Modeling** | Building ABMs | Gregoriy Bobashev | 8, 9, and 16 Septembre 2025 |      |

# Summary
*NetLogo is a software package which contains a user interface for world building and documentation as well as a code development environment in the logo language. Agents in logo are all turtles, but we can define other breeds of agents as well. Time in these models is processed as "ticks" which have no real mapping to the physical world except as defined by the modeler. [[Model Types and Use Cases|ABMs and Microsimulations]] in NetLogo can be as simple or complex as desired as NetLogo supports operations like social networks and continuous time processing as well as a vast ecosystem of extensions which include linear programming, statistics, and more.*

# Key Takeaways
1. NetLogo is both a user-interface and a logo language
2. The logo language is a case-sensitive, space-delimted language
3. Updates in the system can either be viewed on ticks or continuously
4. The `Info` tab of a NetLogo model contains the [[ODD Protocol and Documentation|documentation]] of the model
5. If a function is called within an `ask` loop, it has direct access to the attributes of the agent being acted upon
6. Boolean variables are defined using a question mark (e.g., `conditional-variable?`)

# Definitions
- World: In NetLogo, a world is the combination of the UI environment, documentation on the `Info` tab, and the Logo code itself
- Turtle: An individual agent of any [[Object-Oriented Design|class]]
	- `breed [persons person]` creates turtles of type `person`
- Tick: A unit of time in the system. Also a keyword of the language
	- The length of time a tick represents is specified in the documentation of the model by the modeler. It is a concept and not actually declared
- Widget: An element in the NetLogo UI added by the modeler to allow for setting of model parameters or reporting/plotting of metrics

# Additional Resources
- [NetLogo Documentation](https://docs.netlogo.org/)
- [NetLogo Download](https://www.netlogo.org/)
- [Introduction to Simulation with NetLogo (Medium)](https://thibaut-deveraux.medium.com/introduction-to-simulation-with-netlogo-how-to-create-a-small-factory-2955d45076b)

# Notes
## NetLogo User Interface
- Settings exist both for agent and world behavior
- When thinking spatially, it is important to consider the shape of the world
	- Is this a spherical world , a cylinder, or a box
![[Pasted image 20250921105348.png]]
## NetLogo Programming - Managing Worlds
- Reserved keywords `clear-all` and `reset-ticks` are often used in a setup function to remove all the elements and start from a blank state
- <mark style="background: #FFB86CA6;">Definitions for classes must come at the start</mark> of a Logo program
	- Class attributes are defined using the `{breed name}-owns [attr1 attr2 ...]` syntax
	- Must define both the singular and plural form (e.g., `breed [wolves wolf]`
- Typically, `setup` and `go` functions are created and mapped to equivalent buttons in the UI
- The world is divided as a grid into patches. These patches can also have attributes which are set using the `patches-own` function
- Any global variables can be set at the start of the program as well
- Example: Basic Sheep-Wolf Predation Setup
	 ```text
	 globals [ max-sheep ]  ; don't let the sheep population grow too large
	; Sheep and wolves are both breeds of turtles
	; sheep is its own plural, so we use "a-sheep" as the singular
	breed [ sheep a-sheep ]  
	breed [ wolves wolf ]
	
	turtles-own [ energy ]       ; both wolves and sheep have energy
	
	patches-own [ countdown ]    ; this is for the sheep-wolves-grass model version
	
	to setup
	  clear-all
	  ; Conditional processing using netlogo-web reserved keyword 
	  ifelse netlogo-web? [ set max-sheep 10000 ] [ set max-sheep 30000 ]
	end
	```
## NetLogo Programming - Managing Agents
- After defining breeds, there are generally initialization functions for each agent
	- We use the `create-{breed name} {# instances}` syntax and then in brackets, set the attributes using `set`
	- Once created, we can do specific actions on subsets of the agents by using
		- `ask n-of {count} {breed name} [ ... actions ...]` for a specific number
			- To test percentages, we would use `random-float {max}` and conditional logic to set a probability for each agent. <mark style="background: #FFB86CA6;">This could produce more or less agents than desired</mark>
		- `ask {breed name} with [ ... condition ... ] [ ... actions ...]`
		- These frameworks can also be used outside initialization
		- <mark style="background: #FFB86CA6;">Attributes can also be another agent</mark> (e.g., a destination)
			- Can select this randomly using `one-of` keyword
- Agents acting within the environment
	- Again, the `ask` keyword is used which iterates through each agent
		- We can call functions during this loop and all attributes of the agent will be available
	- We can check agents relative to their patch location `{patch / breed}-here` and/or their connections
- Linking agents (creating networks)
	- We can declare a breed of type link (including making this a directed link)
		- `directed-link-breed [plural-name singlar-name]`
	- With links created, we can form links using the syntax `create-{link-breed}-from {agent} to {agent}`
		- If already in the context of an agent via `ask`, we can omit `from` or `to`
	- We can count how many connections there are using `count-{breed}`
	- Also possible to create simple connections with no attributes or type between agents
		- Use the `create-link` reserved keyword in an `ask` loop for simple links
		- Can filter to say `let choice one-of other persons with [not link-neighbor? myself]` to set a local variable
- Order of operations
	- Choosing the correct order of operations for these models is essential for structure decisions. This choice is determined by your environment and the length of the tick
	- From an implementation standpoint, the key difference is if we process a function in a loop or only make updates on ticks
		- Example: `infect-others` vs `infect-others-continuous` where the latter checks the infection spread condition at each agent step. This makes sense if a tick is a day but doesn't if a tick is 5 minutes
