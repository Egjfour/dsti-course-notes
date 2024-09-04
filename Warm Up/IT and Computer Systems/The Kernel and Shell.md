|     Course Name      |          Topic          | Professor |    Date    |         Tags         |
| :------------------: | :---------------------: | :-------: | :--------: | :------------------: |
| **Computer Systems** | Computer Systems Basics | Sebastian | 2023-03-26 | #ComputerEngineering |

[Class Video](https://learn.dsti.institute/mod/url/view.php?id=12623)

# Summary
*After the [[Operating System|operating system]] is launched by the [[Central Processing Unit|Bootloader]], the kernel is the first program to run. It has 3 key features that must exist. The kernel is responsible for providing hardware resources to user applications and other programs. The kernel is interacted with by the shell which is what allows users to launch various programs.*

# Key Takeaways
1. All operating systems are written in the C programming language because it is small, compact, and has a compiler. This is the "<mark style="background: #FFB86CA6;">modern kernel</mark>"
2. There are 3 fundamental features that must exist in a Kernel:
	- Exclusive Hardware Appropriation *(Kernel owns the hardware)*
	- Scheduling of Processes *(Play multiple tapes at once)*
	- Interprocess Communication *(Share data across programs)*
3. The kernel kills any program trying to access memory that it has no rights to
4. The OS Subsystem is everything in-between the kernel and shell such as file management, networking, and drivers
5. The shell has the ability to launch a program
6. A child process calls the <mark style="background: #FFB86CA6;">kernel EXEC function</mark> which substitutes the binary executable content of one program to another

# Definitions
- Exclusive Hardware Appropriation: Ownership and ability to lend out hardware resources
- Interprocess Communication: Ability to allow programs to share data with each other
- Microkernel: A kernel that is only comprised of the 3 fundamental features
- Monolithic Kernel: A kernel that allows for other code outside of the 3 fundamental features including drivers
- Drivers: Software that lets us decode the data [[Operating System|protocol]]
- Forking: Kernel duplication in memory to launch an application

# Additional Resources
- [Microkernel vs Monolithic Kernel](https://www.geeksforgeeks.org/difference-between-microkernel-and-monolithic-kernel/)
- [Kernel vs Shell](https://www.geeksforgeeks.org/difference-between-shell-and-kernel/)
- [FORK and EXEC functions](https://www.cs.swarthmore.edu/~kwebb/cs31/s15/bucs/fork_and_exec.html)

# Notes
## Defining the Kernel
- First piece of code to run after bootloader identifies the operating system
- Not directly visible to users
- Has 3 fundamental features
	- Exclusive hardware appropriation
		- Kernel owns and lends hardward resources outside of the kernel
		- Apps not on the kernel are in "userland" vs "kernel land"
		- Allows apps to only have <mark style="background: #FFB86CA6;">access to certain memory elements</mark>
	- Scheduling of Processes
		- Play multiple tapes at one time vs the [[Computer Systems Basics|Turing Maching]] which can only play one
	- Interprocess Communication
		- Kills any program trying to access memory it has no rights to
		- Multiple programs can share data with each other

## Types of Kernels
- Microkernel
	- Only has the 3 fundamental features with the rest in userland
	- Drivers cannot access the kernel. If they try, they are unloaded and killed
		- Windows "blue screen of death"
	- Example: Mac OS
- Monolithic Kernel
	- Allows for driver code inside the kernel space
	- More study and stable but can be less safe
	- Example: Linux
- Windows is a hybrid kernel
	- Some drivers have access to kernel land such as graphics drivers
	- Optimizes performance since kernel land is faster as you do not need to request use of hardware components

## The Shell
- Last element to load as part of the Operating System
	- Once loaded, the computer is ready to use
- Allows users to interact with apps and the kernel
	- This is done either using a command line interface (CLI) or a Graphical User Interface (GUI)
	- The CLI on Windows is the command prompt (cmd) and the GUI is Explorer

## Launching a Program
- The shell is what allows users to launch a program
- Shell asks the kernel to duplicate itself using the kernel function FORK()
	- A parent process calls this function with an IPC
	- The child process then receives the file path of the program needing loaded and calls the kernel EXEC function on this forked kernel
![[Kernel and Shell.png]]
