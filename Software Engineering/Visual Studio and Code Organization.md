|           Course Name           |              Topic               | Professor |      Date      |     Tags     |
| :-----------------------------: | :------------------------------: | :-------: | :------------: | :----------: |
| **Software Engineering Part 1** | VS Enterprise and File Structure | Sebastien | 20-21 May 2024 | #Programming |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/ted_codd_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fted%5Fcodd%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FS24%2D%20DS%20%26%20Common%20LINK%20DS%5FDA%5FDE%2D20240520%5F095805%2DMeeting%20Recording%201%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E9bcac6ab%2Ddf07%2D4904%2Da694%2D2570e2d4a7d0)

# Summary
*Visual Studio is an integrated development environment that is multi-language and multi-target developed by Microsoft. VS code is organized using solutions that have projects of a single language within them. It can be used to create end-to-end applications.*

# Key Takeaways
1. Solutions are collections of projects and each project within a solution is its own separate directory on Windows and is consistent in one programming language
2. We should seek to isolate code into files with respect to the purpose and intent of the functions
3. Header files are not compiled code, so they do not get converted to binary
	1. In interpreted languages, this means NONE of the actual source code in a user's program is converted and is all still human-readable creating potential IP concerns

# Definitions
- Multi-Target: The OS/Hardware that the solution will operate on
	- Windows OS on an Intel Chip
- Instrumenting the code: Debugging, testing, and fixing
- Dissociation: Putting the definition (function signature) and actual code of a function in different files
- Function Signature: The name, return type, and number and order of input parameters

# Additional Resources
- [Visual Studio Enterprise User Guide](https://learn.microsoft.com/en-us/visualstudio/windows/?view=vs-2022)

# Notes
## Integrated Development Environments (IDEs)
- Core components to building an app
	- Write the code (Separate product VS Code offers this)
	- Run the code (compile or interpret)
	- Instrumentation of the code
	- Deployment towards production pipelines
		- local or cloud-based
- A fully-integrated development environment like Visual Studio allows us to handle all of these steps
## Visual Studio Components
- Since it is multi-language and multi-target, we need to specify the language and target of a given project (language) and solution (target)
	- e.g., If we select x64, we will use the compiler for [[Central Processing Unit|64-bit CPUs]]
- Code is organized into solutions which contain projects
- Visual Studio Enterprise comes pre-installed with compilers for supported compiled languages
## Source Code Organization
- Main principle: Don't put everything in one file
	- Isolate code wrt purpose and intent
- When possible, use dissociation (C/C++)
	- Separate functions based off signature (header files) and 
	- Data structure definitions also belong in header files