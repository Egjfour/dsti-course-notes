|       Course Name        |        Topic        |    Professor     |       Date        | Tags |
| :----------------------: | :-----------------: | :--------------: | :---------------: | :--: |
| **Agent-Based Modeling** | Model Documentation | Gegoriy Bobashev | 15 Septembre 2025 |      |

[Class Video Link](login.microsoftonline.com/e5d15069-41a2-48be-a3f3-d7f52db16425/oauth2/authorize?client_id=00000003-0000-0ff1-ce00-000000000000&response_mode=form_post&response_type=code%20id_token&resource=00000003-0000-0ff1-ce00-000000000000&scope=openid&nonce=8DC85402705EEC47CFE8CB8D55943E4A71F1C6E559B86586-A676745B2A3F662FBC90694CCCF1C109E62D5EC12FF1A9647A12F34432B662F6&redirect_uri=https%3A%2F%2Fdstisas-my%2Esharepoint%2Ecom%2F_forms%2Fdefault%2Easpx&state=OD0w&claims=%7B"id_token"%3A%7B"xms_cc"%3A%7B"values"%3A%5B"CP1"%5D%7D%7D%7D&wsucxt=1&cobrandid=11bd8083-87e0-41b5-bb78-0bc43c8a8e8a&client-request-id=e0d7c9a1-f07e-e000-2465-019aaf08286f)

# Summary
*ODD Protocol (Overview, Design Concepts, Detail) is the standard for documenting complex agent-based models. It is a framework which is appropriate for audiences of all levels from non-technical stakeholder to the developer implementing the model.*

# Key Takeaways
1. The three main sections of an ODD protocol are the overview, design concepts, and detail
2. Defining the model purpose in the overview is the most important part of the model build
3. Agents in these models should always designed to be updated in random order

# Definitions
- ODD: A standard protocol which acts as a checklist for describing [[Model Types and Use Cases|agent-based and other simulation models]]
- Emergence: The patterns that the model produces independently which are not explicitly implemented in the code
- Burn-in/Spin-Up Period: Allowing models to get from initialization to their steady-state

# Additional Resources
- [ODD Documentation - Journal for Artificial Societies and Social Simulation](https://www.jasss.org/23/2/7.html)

# Notes
## Overview
- Purpose and Patterns
	- Should have a clear and concise statement of the question/problem addressed by the model
	- It is better to get an approximate answer to the right question than a precise answer to the wrong question
- Entities, state variables, and scales (model components)
	- Agents (Who)
	- Environments (Where)
	- Major variables - global and state (what)
	- Major rules (how)
	- Scales for temporal, spatial, and populations/boundaries
- Process overview and scheduling
	- How do components function
	- What are the agents doing (searching, mating, fighting, etc.)
	- How does the environment change
	- What does the observer do
	- <mark style="background: #FFB86CA6;">Should use pseudo-code to describe the schedule in detail</mark>
## Design Concepts
- How are concepts translated to the model
- How are entities, rules, and their interactions modeled
- What are the measures for variables and parameters
- How are choices and decisions modeled
- Key elements
	 ![[Pasted image 20250927155020.png]]
- Do agents have an objective or are they acting randomly
- Environments
	- Natural environments like roads/buffers
	- Degradation and regrowth
- How to handle randomness
	- Probabilistic decisions
	- Random connections between agents
	- What does and does not need randomized
## Detail
- How do initial values get assigned
	- Need for burn-in period
- How environment is initialized
	- From data/random draws
	- If random, is there a seed
- How are records kept
- Are there input files and if so are they static or dynamic
- Are there sub-models and if so how are they adapted or connected
- Any mathematical models