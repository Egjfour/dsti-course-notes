|     Course Name      |          Topic          | Professor |    Date    |         Tags         |
| :------------------: | :---------------------: | :-------: | :--------: | :------------------: |
| **Computer Systems** | Computer Systems Basics | Sebastian | 2023-03-26 | #ComputerEngineering |

[Class Video](https://learn.dsti.institute/mod/url/view.php?id=12624)

# Summary
*Multitasking is a computer engineering illusion that makes it appear as though many processes are running simultaneously. Rather, what is happening is a continuous, rapid-fire switching of resource allocation managed by the operating system to provide brief access to hardware resources. This is what allows a computer to run more programs than it has available logical units.*

# Key Takeaways
1. The [[The Kernel and Shell|kernel]] itself is a program that is subject to scheduling
2. Preemptive multitasking is based on a quantum of time
3. The context of a program must be saved for when it restarts
4. It is essential that the scheduling decision is less than the quantum of time
5. It is threads that are scheduled, not processes
6. Python is a mono-threaded language due to the global interpreter lock (GIL)
	a. This blocks global variables from being altered whenever any thread touches them

# Definitions
- Cooperative Multitasking: Apps put themselves to sleep
- Preemptive Multitasking: Authoritative scheduling - apps don't decide when to sleep
- Quantum of Time: Maximum duration for which a program can run
	- Usually very small (miliseconds or nanoseconds)
- Context: The total sum of all [[Central Processing Unit|CPU Registers]]
- Context Switching: Copying the context to main memory
- Thread: A unit of execution

# Additional Resources
- [Preemptive vs Cooperative Multitasking](https://www.geeksforgeeks.org/difference-between-preemptive-and-cooperative-multitasking/)
- [Processes and Threads (Microsoft)](https://learn.microsoft.com/en-us/dotnet/standard/threading/threads-and-threading)
- [Thread Race Explanation](https://www.techtarget.com/searchstorage/definition/race-condition)

# Notes
## Defining Multitasking
- Multiple programs have code loaded into memory
- Essential to schedule these are there are more programs available than the computer has ALUs
	- Results in a <mark style="background: #FFB86CA6;">need for time sharing</mark>
	- The kernel and scheduler must also be running and are scheduled
- The Windows kernel is divided into many parts that are all individually subject to scheduling

## Multitasking Mechanisms
- Cooperative Multitasking
	- Apps yield hardware use back to the scheduler
	- Any one app can not yield resources and halt all other processes
	- Permits malicious actors to tie up resources
- Preemptive Multitasking
	- Authoritative - operating systems controls which apps get resources and when
	- Based on a quantum of time which is the max duration for which a program can run
	- The scheduler uses the [[Computer Systems Basics|PIC]] to halt the CPU the individual app is using
		- The <mark style="background: #FFB86CA6;">PIC changes the CPU instruction pointer back to the scheduler code</mark>
	- The context (precise state) of the program must be saved for when the program restarts
		- This is the <mark style="background: #FFB86CA6;">total sum of CPU registers and is saved to the main memory</mark>
	- This context is switched extremely rapidly (miliseconds or nanoseconds) to give the illusion of true multitasking -- the quantum of time is smaller on a [[The Kernel and Shell|microkernel]]
		- To allow for this to be successful, the scheduling decision for what to allocate resources to next MUST be smaller than the quantum of time

## Threads and Threading
- What and Why
	- Threads are units of execution within a program
	- These represent sections of code that should be subject to scheduling and multitasking
- Mono vs Multi-Threaded Code
	- Mono-threaded programs are processes that only run using one unit of execution
		- A single task will block others from running
	- Multi-threaded processes, by contrast, divide the work across many units of execution
		- This means that the <mark style="background: #FFB86CA6;">threads within the same program will compete with each other</mark> to be scheduled in preemptive multitasking
	- With multi-threaded code, we cannot be sure of the order of the execution, so we must take care to <mark style="background: #FFB86CA6;">avoid a potential thread race</mark>
		- A function is parallelizable (can be multi-threaded or multi-processed if it is summable) -- example: calculating an average
- Threading in Python
	- It is technically possible but should never be done since the global interpreter lock will block it from happening
	- Instead, in python, we use multiprocessing with mono-threaded code