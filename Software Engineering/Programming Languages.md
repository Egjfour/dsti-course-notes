|        Course Name         |             Topic             | Professor |    Date     |                   Tags                    |
| :------------------------: | :---------------------------: | :-------: | :---------: | :---------------------------------------: |
| **Software Engineering 1** | Software Engineering Overview | Sebastien | 20 May 2024 | #Python #ComputerEngineering #Programming |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/ted_codd_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fted%5Fcodd%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FS24%2D%20DS%20%26%20Common%20LINK%20DS%5FDA%5FDE%2D20240520%5F095805%2DMeeting%20Recording%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0%3D&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0=&ga=1)

# Summary
*Programming languages are a tool used in software engineering. Within these, there are two main camps, classical programming (C, and SQL) and object-oriented programming (C++, Java, Python). The main distinctions between programming languages are the methodology used for typing variables (implicit vs explicit) and how parameters are passed to functions (copy the data vs provide a memory address)*

# Key Takeaways
1. The official Python interpreter is written in C ("CPython")
2. Classical software engineering is only concerned that the input and output are in the correct format for a function. It is thus said that classical design is a "<mark style="background: #FFB86CA6;">constraint on the data</mark>"
3. Since software engineering is the only engineering discipline not backed by the laws of physics, there is no definitive "right" or "wrong" design. This is true in the concepts of encapsulation as well
4. Since <mark style="background: #FFB86CA6;">python is strongly typed</mark> (i.e., we cannot transtype like in C), a new object must be created in memory when we create a new variable. This interrupts the thread and the process is then subject to [[Multitasking|kernel scheduling]]
	a. This same implication exists for the instantiation of any object in an interpreted language (compiled languages start with all variables on the stack)
5. Exceptions have execution time costs (though are still essential) 
6. Exception management DOES NOT exist in C
# Definitions
- Software Engineering: The productionization of programming/code that fits into a larger system
- Programming Language: The core features of the languate AND the standard library
- Caller: The environment from which a function is called
	- The `main()` function in a C project
- Callee: The function that is invoked from the Caller
- Abstraction: The use of human-readable artifacts (notably variable names) which exist to hide the memory location which is what is ultimately used by the micro-code
- Just-in-time (JIT): An interpreted language where the code is converted to microcode just before it runs

# Additional Resources
- [GLUE Languages](https://www.devx.com/terms/glue-language/#:~:text=Glue%20languages%20facilitate%20communication%20between,of%20use%20and%20flexible%20nature.)
- [Data Typing](https://en.wikipedia.org/wiki/Type_system#STATIC)

# Notes
## Reasons for Learning C & C++
- The official python interpreter as well as many fundamental python packages are written in C
	- Python is designed to be a GLUE language
		- A glue language, also known as a scripting language, is a programming language that is used to connect and communicate between various software components. It allows different programming languages, libraries, and software applications to work together seamlessly. (*Reference Above*)
	- For example, NumPy and Pandas exist as python wrappers around C and Fortran code
		- This allows for much better performance since these libraries are then compiled
- Relational Database Management Systems' core engines are also written in C
- The kernels of all modern operating systems are written in C
	- Our code is not the only thing trying to run on the system at any given time, so by using the same language as the operating system kernel, we can leverage the same tools that exist in the OS already
## General Programming Language Features
- Typing (Implicit - Python vs Explicit - C): Do you have to explicitly write the type or not?
	- Minimally all languages have an integer type
	- Languages also decide if the data is strongly typed (data type is immutable - Python) or loosely types (data type is able to change - C)
		- C is able to have data type of a change through trans-typing/recasting
		- The datatype of a given variable cannot change in python. Once that memory location is allocated, we have to use a function call to create an entirely new object
	- We also determine if a data type is static (type cannot change at runtime  - C) or dynamic (data type can change at runtime - Python sometimes)
		- The first time a variable is assigned in python, it is dynamic, but then, the type is immutable since it <mark style="background: #FFB86CA6;">recycles the values of immutable classes</mark> (int, float, str, etc)
	-  *Stack Overflow Explanation*
		- Strong/Loose Typing is about **how strictly** types are distinguished (e.g. whether the language tries to do an <mark style="background: #FFB86CA6;">implicit conversion</mark> from strings to numbers).
		- Static/Dynamic Typing is about **when** type information is acquired (Either at <mark style="background: #FFB86CA6;">compile time or at runtime</mark>)
- Passing Values to Functions
	- "How are values provided to a function actually used in the function call"
		- Ultimately, the concern here is how data goes from the caller to the callee (and sometimes back to the caller)
	- The invocation of a function is the callee and the usage is the caller
	- Callers and Callees have their own separate environments and local variables exist either within the scope of the caller or the callee
	- The simplest way to pass data is to actually copy the values themselves (Pass by Copy/Value). The data is then copied bit-by-bit to the callee from the caller's variable
## Classical vs Object-Oriented Language Features
- Classical Key Features
	- Exist on the principle of functions where x (input data) is the only dimension and y is the output y = f(x)
		- In RDBMS, the SQL engine is f, x is a query, and y is the result of applying f(x)
	- <mark style="background: #FFB86CA6;">Only concern is that x & y are in the right format for f</mark>
		- Functions using data structures receive and return understandable/processable data
		- We have a "constraint on the data" such that we design the data structure and then code to apply to it
- Object-Oriented
	- <mark style="background: #FFB86CA6;">Encapsulation: Main principle and design concept</mark>
	- Inheritance
	- Polymorphism
	- Overloading
	- Aggregation
- In addition, both styles offer abstraction where we are able to use human-readable names to reference memory locations
## Exception Handling
- Relevant in situations where there is an error but the error is not so bad that we must terminate immediately (like going out of an array) but we still are not able to proceed
	- The code must stop executing but does not terminate. Rather, it is trapped
- Implemented as a class and used with a try/catch statement
	- This is managed by the runtime which monitors the try block and branches to the catch block if necessary
	- A try statement can have many catch blocks (these should go from most specific to most general)
- These are necessary in compiled or Just-in-Time (JIT) interpreted languages so that we don't throw exceptions
	- In Python, however, the interpreter is already running which handles the exceptions anyway, so there is no benefit to having more tests


