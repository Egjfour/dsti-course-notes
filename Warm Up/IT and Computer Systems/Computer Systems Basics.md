|     Course Name      |    Topic     | Professor |    Date    |         Tags         |
| :------------------: | :----------: | :-------: | :--------: | :------------------: |
| **Computer Systems** | Introduction | Sebastian | 2023-03-26 | #ComputerEngineering |
|                      |              |           |            |                      |


[Class Video Link](https://learn.dsti.institute/mod/url/view.php?id=12623)

# Summary
*Modern digital computers are based on the Von Neumann design which utilizes Turing Machines to execute inputs. The initial startup of a computer launches the BIOS from the No Operation Process (NOP) which enables the RAM and CPU to communicate via the BUS.*

# Key Takeaways
1. A modern general purpose computer is one that can run any task using the machine
2. Alan Turing is the father of the modern general purpose computer
3. A Turing Machine takes input data and instructions to produce an output
4. Exiting the idle process is "unloading the tape" to do something else
5. The PIC essentially presses pause on the Turing tape reader

# Definitions
- Algorithmics: Designing and evaluating the performance of an algorithm
- Deterministic: Same output is always provided for the same inputs when applied systematically
	- In computer terms, this means that our computers are "finite-state automatons"
- BIOS: Hardwired interruption at value 0. The first thing that interrupts NOP when a computer is powered on
- Digital Computer: A computer that acts on discrete sets of data (binary code)
- Analog Computer: A computer that gets its input from continuous data input
	- Sound waves, electricity, etc.

# Additional Resources
- [Turing Machines](https://www.youtube.com/watch?v=dNRDvLACg5Q&t=7s&ab_channel=Computerphile)
- [Von Neumann Architecture](https://www.geeksforgeeks.org/computer-organization-von-neumann-architecture/)
- [Analog vs Digital Systems](https://www.geeksforgeeks.org/difference-between-digital-and-analog-system/)

# Notes
## Computer Science vs Engineering
- Computer Science
	- Branch of applied mathematics with a primary focus on algorithmics
- Computer Engineering
	- Science of constructing and operating computers
	- Necessary for other disciplines to understand to industrialize their work

## Types of Computers
- Modern digital computers are general purpose
	- By contrast, specific-purpose computers (the enigma machine) can only be used for their designated purpose
- Analog vs Digital Computers
	- Ultimately a question of data input
	- Analog uses a continuous signal, whereas the signal for digital computers is discrete
		- Continuous: sound/light waves
		- Discrete: A program executing as binary
	- Digital computers only work with analog input and output devices
		- Mouse, keyboard, etc
	- Analog computes instantaneously and is excellent at linear algebra and differential equations

## Turing Machines
- Alan Turing (father of the modern general purpose computer)
	- Decoded the German Enigma machine in WWII
	- Initial approach, Colossus, was a failure because it utilized a naive, brute-force approach and the combinatorics required for the Enigma machine were too great
- Turing machines are based on math and logic
	- Uses an input tape that carries data and instructions
	- Produces an output tape with only data
	- System is <mark style="background: #FFB86CA6;">deterministic</mark>
- Based on the theory of languages
	- Grammar on the inputs must be decidable

![[Turing Machine Diagram.jpg]]

## Von Neumann Architecture (3 Components)
- Algorithmics and Logical Unit (ALU)
	- Precursor to the modern-day Central Processing Unit (CPU)
	- Able to perform <mark style="background: #FFB86CA6;">basic math and basic logic</mark> (and, or, not)
	- The ALU is the Turing Machine
- Main Memory
	- Akin to the input tape of the Turing Machine
	- Memory used for the active process
	- Can host a library of tapes in a secondary memory
	- Precursor to modern-day RAM
- BUS
	- Connection between ALU and any memory
	- Wires move data from one component to another

![[Von Neumann Architecture.png]]

## Initial Startup
- When the power is turned on, the electric current begins to flow
- The No Operation Process (NOP) begins and is running nothing in an infinite loop
	- Since the current is flowing, *something* must always be running
	- This is called the System Idle Process on Windows
- The Programmable Interruption Controller (PIC)
	- Methodology for exiting the NOP since it is an infinite loop
		- Historically was done manually by physically changing the tape to run a new program
	- PIC is connected directly to the BUS
	- Contains a <mark style="background: #FFB86CA6;">small amount of built-in memory which can be visualized as an array</mark>
	- Gives the CPU instruction pointer which tells it what to do next
	- Active waiting uses computer resources to wait for an event (wasteful for resources)
	- Passive waiting sends an electrical signal to the program to tell it to go do something else

| Interruption Value | Address (examples) |
| ------------------ | ------------------ |
| 0                  | 10250              |
| 1                  | 23522              |
| etc                | etc                |
