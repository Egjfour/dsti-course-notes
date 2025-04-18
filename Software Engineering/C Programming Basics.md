|          Course Name          |     Topic     | Professor |      Date      |     Tags     |
| :---------------------------: | :-----------: | :-------: | :------------: | :----------: |
| **Software Engineering Pt 1** | C Programming | Sebastien | 20-21 May 2024 | #Programming |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/ted_codd_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fted%5Fcodd%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FS24%2D%20DS%20%26%20Common%20LINK%20DS%5FDA%5FDE%2D20240520%5F095805%2DMeeting%20Recording%201%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E9bcac6ab%2Ddf07%2D4904%2Da694%2D2570e2d4a7d0)

# Summary
*C is a compiled, [[Programming Languages|classical programming language]] that was first written in the 1960s. It is the basis of all modern [[Operating System|operating system kernels]]. It is Explicit, loosely and statically typed language. It handles the passing of variables as function parameters by copy as a default but allows for (and is encouraged to use) pointers to pass by address. The standard library is essential in C since the base language offers very little functionality since only data in memory can be manipulated.*

# Key Takeaways
1. There may only be one main function per C project since this serves as the entrypoint for the project
2. Due to [[Programming Languages|explicit typing,]] data types are declared before variables
	a. Example: `int a = 1;`
3. Because the <mark style="background: #FFB86CA6;">core C language can only manipulate data in memory (RAM)</mark>, we have very limited [[Computer Systems Basics|BUS access]]. If we want anything beyond that, we will need the standard library
4. The malloc() command is used to allocate memory dynamically
	a. Example: `malloc(sizeof(int), 3)` dynamically reserves 3 additional spaces on RAM for data of type integer
5. Functions also must have a return datatype. <mark style="background: #FFB86CA6;">If there is no return, the data type is void</mark>

# Definitions
- Prefixed Syntax: A data type comes before the identifier
	- Practical examples can be added below
- Directives: Lines beginning with `#` that are generated by the [[The Compiling Process|preprocessor in the compile process]] (library imports, parameter declarations, etc)

# Additional Resources
- [Data Types in C](https://www.geeksforgeeks.org/data-types-in-c/)
- [C Standard Library](https://en.cppreference.com/w/c/header)
- [typedef Examples](https://www.ibm.com/docs/en/i/7.5?topic=definitions-examples-typedef)

# Notes
## Basic Syntax Rules
- The C language is explicitly typed, meaning that we must specify the datatype of variables. This is done with a prefixed syntax
- All statements end with a semi-colon `;`
- The language is case-sensitive but space insensitive
	- A single command can span multiple lines and the compiler will remove these as it translates the C code into microcode
- Blocks of code (flow control statements like if-else conditions and loops) are delimited with curly braces
## Standard Library
- The standard library expands upon the core language. It is guaranteed as part of any programming language with respect to the version
- This is essential in C as the core language can only do the following basic operations in memory (RAM)
	- Declare and compute over variables
	- Alternative (conditional) and iterative (loop) statements
	- Basic Arithmetic
	- Recognize and store function definitions
- To import a library, we use the `#include` syntax
	- This will <mark style="background: #FFB86CA6;">copy the code of that library into our code at compile time in the exact location</mark> that the include appears
	- We use the `#pragma once` command to help make sure we don't accidentally create an endless import loop
	- The name of a standard library always starts with "std" and ends with ".h" (header files) and is housed inside of <>
		- Example: `#include <stdio.h>` loads the standard input/output library giving us access to functions like `printf()`
## Custom Datatypes
- The `typedef` command is used to create custom datatypes
- In a simple version, we can create a boolean. The syntax shown means "treat any instance of BOOL in the code as an int". The compiler will actually make this replacement during the build process
	- Example: `typedef int BOOL;`
	- We then use the `#define` command to specify values to use. The `#define` command performs a "find and replace" all instances of the provided value with the other one at compile time and <mark style="background: #FFB86CA6;">DOES NOT need a semi-colon since it is not executable code</mark>
		- `#define TRUE 1`
		- `#define FALSE 0`
		- This is also used for parameters like `#define STEP_SIZE 10`
- More complex data type definitions (structures) can be created that have multiple attributes as well
```c
typedef struct {
	int* pBaseArray; // The p is standard C practice where variable types are the first char of the var name
	unsigned int nMemory_Size; // Unsigned means do NOT apply the Two's Complement (allows for larger arrays)
	unsigned int nNumber_Elements;
} OurVector;
```
- In the example above, we are creating a structure called "OurVector" that contains a pointer to an integer value and two unsigned integer values to act as metadata