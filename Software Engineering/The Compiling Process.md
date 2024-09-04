|           Course Name           |   Topic   | Professor |    Date     |         Tags         |
| :-----------------------------: | :-------: | :-------: | :---------: | :------------------: |
| **Software Engineering Part 1** | Compiling | Sebastien | 20 May 2024 | #ComputerEngineering |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/ted_codd_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fted%5Fcodd%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FS24%2D%20DS%20%26%20Common%20LINK%20DS%5FDA%5FDE%2D20240520%5F095805%2DMeeting%20Recording%201%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E9bcac6ab%2Ddf07%2D4904%2Da694%2D2570e2d4a7d0)

# Summary
*The compiler is a piece of software that converts our human-readable [[Programming Languages|abstracted]] code into microcode with respect to a given language, OS, and hardware. Ultimately, the output of a compiler is an object file that contains the microcode. The linking process is then what creates the actual executable file for an operating system/hardware combination with respect to the application binary interface defined by the operating system.*

# Key Takeaways
1. The result of the compile process is an object file which is NOT executable directly by the OS
2. Compilers & Linkers must provide executable files that are ABI compatible to a specific target architecture (OS and CPU)
3. In interpreted languages, the compile-link process is instead performed on the compiled code of the interpreter -- not our own

# Definitions
- Compile Target: The OS/environment and hardware ([[Central Processing Unit|CPU type]] - bitness and design)
- Application Binary Interface: The necessary data and metadata to inform the OS about a given program

# Additional Resources
- [The Compile Process Overview](https://www.javatpoint.com/compilation-process-in-c#:~:text=The%20compilation%20is%20a%20process,it%20generates%20the%20object%20code.)
- [Steps of Compilation (Medium)](https://medium.com/@samiribrahimov2277/understanding-the-steps-of-compilation-f118dead3697)
- [What is an ABI (StackOverflow)](https://stackoverflow.com/questions/2171177/what-is-an-application-binary-interface-abi)

# Notes
### The General Compile Process
- This is performed for each source file
- The compiler will:
	- Preprocess the code by removing unnecessary spaces and run any [[C Programming Basics|preprocessor directives]]
	- Analyze the syntax (sometimes perform semantic analysis as well)
	- Transform the source code into assembly code wrt the hardware and OS
	- Convert the assembly code into Microcode (binary)
		- This is an object file and is NOT executable by the OS
## The Linking Process
- After the compiler runs on each source file, the linker integrates everything and packages it into an executable for the OS
- The linker integrates external code (libraries) into our own
- The linker also integrates the C runtime as well as the data and metadata to inform the OS about the program called the Application Binary Interface (ABI)
	- The ABI needs to know the size of the program, the location of the main entry point, etc and fit it into the target OS and CPU
![[Pasted image 20240526222225.png]]