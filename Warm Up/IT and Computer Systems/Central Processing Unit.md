|   Course Name    |          Topic          | Professor |    Date    |         Tags         |
| :--------------: | :---------------------: | :-------: | :--------: | :------------------: |
| Computer Systems | Computer Systems Basics | Sebastian | 2023-03-26 | #ComputerEngineering |

[Class Video](https://learn.dsti.institute/mod/url/view.php?id=12623)

# Summary
*The central processing unit is made up of at least one [[Computer Systems Basics|ALU]] as well as a zone of registers. This zone of registers is the L1 cache. The [[Computer Systems Basics|BUS]] is then made available for loading the operating system using the Basic Input/Output Subsystem (BIOS) which enables the [[Operating System]].*

# Key Takeaways
1. The CPU has two main components: an ALU and the zone of registers
2. The BIOS is a command and control software that makes the BUS available
3. The ROM and RAM chips form a unique and *unified* global address space
4. [[Computer Systems Basics|Digital Computers]] can only handle integers
	1. It is essential therefore to remember that any real number is only an approximation

# Definitions
- Registers: Memory Zones containing data or instructions
- The BUS: System of electrical connections between hardware elements
- CPU Bits: The length of all CPU registers
	- A 64-bit CPU means the register area is physically constructed with transistors to accommodate a value based on 64 binary digits
- Read-Only Memory (ROM): Nonvolatile memory where the data has been recorded and is stored even after the computer has been turned off
- Random Access Memory (RAM): Volatile memory used to store the programs and data being used by the CPU in real-time
- Metadata: CPU registers that indicate how to manage data
- Instruction Set: The grammar provided to the CPU to understand the program
	- Once mapped to an integer set for the machine to read, this is known as <mark style="background: #FFB86CA6;">microcode</mark>
	- While still in a human-readable format, this is known as <mark style="background: #FFB86CA6;">Assembly Code</mark>
- Input/Output Bottleneck: The delay in processing time as data/microcode moves from component to component with some being slower than others

# Additional Resources
- [How BIOS Works](https://computer.howstuffworks.com/bios.htm)
- [ROM and RAM](https://www.geeksforgeeks.org/difference-between-ram-and-rom/)
- [Two's Complement](https://en.wikipedia.org/wiki/Two%27s_complement)

# Notes
## CPU Components (Intel Description)
- At least one (or multiple) ALU (monocore vs multicore)
- Zone of Registers
	- Knowns as the L1 cache
	- This is the real [[Computer Systems Basics|Turing Tape]]
	- Registers are either used for storing data and instruction or are used to manage data
	- Includes the instruction pointer register
	- This exists to help mitigate the Input/Output Bottleneck
- CPU size is expressed in bits which is the number of binary digits that can be accommodated
- Computations are ONLY performed in the memory area allocated in the zone of registers
	- This happens according to the following process
		- FETCH (From RAM)
		- DECODE (Apply Grammar)
		- EXECUTE
		- WRITE BACK (To RAM)

## Basic Input/Output Subsystem (BIOS)
- Provides and makes available the BUS
- Historically was located in ROM
	- Replaced by UEFI today
- ROM and RAM chips form a unique global address space
	- flat, indexed array from 0 -> n where n is the total amount of memory
- Once BIOS is loaded, the tape changes again to enable the operating system

## CPU Input
- A digital computer is only able to accept integers as input, so everything else must be converted
- For integers, we simply convert from base 10 to base 2
	- Successive long division by two until you reach 1
	- Take all remainders starting from the inner-most division to the top
	- To convert in the reverse, use power addition
		- EX: 11001 in base 10 would be
$$
1 x 2^4 + 1 x 2^3 + 0 x 2^2 + 0 x 2^1 + 1 x 2^0 = 25
$$
- For negative values, there are two methods
	- Flag method: reserve the first or last binary digit to serve as the negative
		- More complex hardware needed
	- Two's Complement: Flip and Invert
	- No matter what, with negative values, total number of digits we can process is cut in half
- For real numbers, we use scientific notation and reserve certain bits for the sign, mantissa, and exponent