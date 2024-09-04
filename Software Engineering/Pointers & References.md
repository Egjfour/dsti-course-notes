|           Course Name           |  Topic   | Professor |    Date     |     Tags     |
| :-----------------------------: | :------: | :-------: | :---------: | :----------: |
| **Software Engineering Part 1** | Pointers | Sebastien | 21 May 2024 | #Programming |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/ted_codd_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fted%5Fcodd%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FS24%2D%20DS%20%26%20Common%20LINK%20DS%5FDA%5FDE%2D20240521%5F094946%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Ea2e0abbf%2Df296%2D40d5%2Dad58%2Dc048b03f3b60)

# Summary
*The unary operator allows us to pass a pointer or memory address to a callee. This action allows us to change values inside the scope of a caller function. Pointers exist in all [[Programming Languages|programming languages]], though only certain ones (C/C++) have explicit pointers that can be accessed by the developer. In C++, there is a special type of pointer called a reference which automatically de-references a pointer and is <mark style="background: #FFB86CA6;">type-compatible with the base datatype</mark>. Pointers are primarily used when we need a callee function to modify data inside a caller function or to handle dynamic memory allocation.*

# Key Takeaways
1. The python interpreter is the the stack of any python program since only compiled code can be on the stack
2. Pointers are used for one of two operations
	a. Callee function needs to modify data in the caller (example of the swap function)
	b. We need more memory than the size of the stack and must dynamically allocate memory
3. In Python, all variables are to an internal datatype of the python interpreter, a PyObject, which is a C datatype
4. void (generic) pointers do not have an associated datatype. They can point to any datatype but cannot be dereferenced
5. The NULL pointer references RAM address 0 which is unwritable as it is the the BIOS/UEFI
6. Stack memory is contiguous as a whole but the heap memory is scattered throughout the RAM and is only <mark style="background: #FFB86CA6;">contiguous per block (per malloc call)</mark>

# Definitions
- Stack: The memory footprint of a program which includes our actual code (space for declared variables and the code itself), imported libraries, and the <mark style="background: #FFB86CA6;">runtime of our programming language</mark>
- Heap: Memory that is dynamically allocated to a program during runtime that is not a part of the stack via a call to `malloc()`
- Pointer: An explicit data type which is an integer representing the memory address of a variable
	- These can be explicit via syntax ("\*" in C/C++) or implicit (Java/Scala) where there is no direct access to pointers
- De-referencing ("\*" and "&" symbol): Read/change the data at a given memory address associated with the pointer value ("Get the data at this location")
	- We actually <mark style="background: #FFB86CA6;">physically move along to the memory location of the pointer</mark> in this process which is what allows us to change the value
- Syntactic Sugar: The process of a programming language creating a more streamlined and simplified operation for a given operation
- Dangling Pointer: A pointer for which we lose the memory location that was given by malloc and thus continue to "rent" it from the OS even after the program terminates

# Additional Resources
- [Differences Between Stack and Heap Memory](https://www.linkedin.com/pulse/difference-between-stack-heap-c-eloghene-otiede/)
- [C-Pointers (GeeksForGeeks)](https://www.geeksforgeeks.org/c-pointers/)
- [Dangling, Void , Null and Wild Pointers in C](https://www.geeksforgeeks.org/dangling-void-null-wild-pointers/)

# Notes
## Stack Memory
- When a compiled program is launched, the stack memory is deterministic. We know exactly which variables have been declared and their type, so we know how much memory is needed
- The stack of our program contains several parts: the actual code and space for declared variables, imported libraries, and the runtime of the language
- This memory is <mark style="background: #FFB86CA6;">constant in time and cannot be changed</mark>
	- All python variables must be dynamically allocated and are not located on the stack
![[Pasted image 20240528105711.png]]
## Pointers
- The two use cases are for allowing callee functions to read/change data in the caller and to handle dynamic memory allocation
- In Python, all variables are pointers to an internal datatype of the Python interpreter called a PyObject in C
	- From the point of view of C, everything in the interpreter is a `PyObject*` object which are a set of the base address of a dynamic memory allocation
- Some languages allows you to explicitly interact with pointers (C/C++) using datatype modifiers ("\*"). In these languages, parameters are passed by copy as a default and pointers must be explicitly chosen
- Java and Scala do not have explicit pointers (defaults cannot be changed)
	- Default behavior is pass by copy for non-object data types and pass by address for objects
- Python is like Java *except* everything is an object, so everything is passed by address
	- Some classes, however, are immutable meaning they cannot be changed once instantiated
- <mark style="background: #FFB86CA6;">Pointers also have data type definitions</mark>
	- `int*` means a pointer to an integer value
	- There is also a generic pointer `void*` which is untyped
		- malloc calls return a void* pointer to the <mark style="background: #FFB86CA6;">base address of the new block of contiguous memory</mark>
## Updating Caller Values in Callee
- This is one of the two main use cases for pointers
- In the scenario below, we have a main() function and would like to swap 2 variables.
- If we try to simply pass by copy. The values provided as input to swap would be copied into parameters a and b and then we would modify the data at memory the memory addresses for a and b. This would do nothing for x and y in main
```c
void swap(int a, int b)
{
	// Swap exchanges the values of a and b
	// Needs to allow access across environment scopes
	int buffer;

	// Store initial value of b in the buffer
	buffer = b;

	// Change b to the value of a
	b = a;

	// Change a to the value of the buffer
	a = buffer;
}

void main()
{
	// Initialize multiple vars at once
	int x = 10, y = 50;

	// The caller function main needs x & y by the callee
	// swap() cannot take copies of these -- need the actual memory location instead
	// C provides a unary operator (one operand)
		// "&" when applied to a variable, gives the memory address of the variable instead
	swap(x, y); // Pass by copy - default behavior
}
```
- If we want to change the values of x and y in main, we need to provide the references of x and y as inputs to a function that expects to receive inputs of type `int*`
## Dynamic Memory Allocation
In [[C Programming Basics|C]], the `malloc` function is what provides this additional [[Computer Systems Basics|RAM]] space
```c
void main()
{
	// A stack-based array of 10 integers
	int intArray[10]; // Size is hard-coded with a constant [10]

	/*
	* CANNOT DO THIS:
	* int size = 50; -- this could come from anywhere: console, file, etc
	* int anotherArray[size];
	* 
	* If we try, the initial memory footprint of the stack would be non-deterministic
	which violates the principles of a Turing machine on the Von Neuman architecture
	*/

	// A possible scenario
	int size = 5000; // Suppose this is read from a file
	// This would happen at runtime when then program executes

	// We now know that we need an array of 5000 integers
	// Second pointers use-case: Dynamic Memory Allocation

	// We ask the operating system memory manager for supplemental memory
	// Use the malloc function ("Memory Allocation") from the stdlib.h library

	//malloc asks the OS memory manager for a CONTIGUOUS block of memory as the size given in parameter (given in bytes)
	//sizeof one int multiplied by the desired size read in I/O

	// Need to capture the base address of thie new memory block
	int* dynIntArray =	malloc(sizeof(int) * size); // We are setting the memory address of the new array

	// If the OS accepts the request, malloc returns a memory address to serbe as the base address of the new block
	// If the OS doesn't accept, malloc returns NULL

	// So we should always check to make sure it succeeded
	if (dynIntArray != NULL)
	{
		// Cool, there is more memory
			// The program now has a STACK and HEAP
			// The stack is contiguous as a whole
			// The hear is only contiguous per block but discontiguous across blocks

		// Fill with values

		for (int i = 0; i <= size; i++)
			dynIntArray[i] = i * 2;


		// Okay, but now there is more data to load and process
		// We cannot increase the size of this array because the RAM doesn't belong to us. We need to ask for more
		// We cannot predict if the zone is extendable on the RAM

		/*
		* This means:
		*	1. Requests for more memory (to the new size)
		*	2. Copy data from old block into new
		*	3. De-allocate the old block
		*	4. Use the new block
		*/

		// Suppose size changes
		size = 10000;
	}
	else
	{
		printf("Cannot allocate memory for %d integers, exiting\n", size);
	}
```
- The malloc call asks the OS memory manager to lease more memory to our program outside of the stack
	- This memory must be contiguous since the <mark style="background: #FFB86CA6;">array name is a pointer to the BASE memory address</mark>
	- If the malloc call fails, it returns the NULL pointer
- When allocating dynamic memory in low-level languages, we must be sure to free this memory and avoid memory leaks