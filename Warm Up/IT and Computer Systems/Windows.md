|        Course Name        |          Topic           |   Professor   |  Date   |             Tags              |
| :-----------------------: | :----------------------: | :-----------: | :-----: | :---------------------------: |
| **Computer Systems Labs** | Windows Operating System | Clément Ziane | 4/16/23 | #Windows #ComputerEngineering |

[Class Video Link](https://learn.dsti.institute/mod/url/view.php?id=12734)

# Summary
*Windows is an [[Operating System|operating system]] that works on different hardware providing portability and has symmetric multiprocessing and client-server computing. It manages memory through the driver. Because of it's flexibility, windows is extensible as well.*

# Key Takeaways
1. Windows is designed for business owners and commercial users
2. Primary Specificities of Windows OS
	a. Licensed operating system
	b. Supports multiple operating environments
	c. Allows for symmetric multiprocessing
	d. Uses the client-server architecture for computing
	e. Manages memory through the driver and virtualizes data using the address of there to find the data on the disk
	f. Portable - could go onto any machine
	h. Preemptive scheduling
3. The localhost is the result of client-server computing and lets apps on the same computer communicate between each other
4. The clock provides a measurement of the efficiency of the CPU

# Definitions
- Extensibility: you can change the [[The Kernel and Shell|user interface]]
- Symmetric Multiprocessing - Independent threads can calculate at the same time
- Starvation: A process does not have the resources need to execute

# Additional Resources
- [Symmetric Multiprocessing](https://www.techtarget.com/searchdatacenter/definition/SMP#:~:text=SMP%20(symmetric%20multiprocessing)%20is%20computer,charge%20of%20all%20the%20processors.)
- [Client-Server Architecture](https://www.interviewbit.com/blog/client-server-architecture/)
- [Drivers](https://learn.microsoft.com/en-us/windows-hardware/drivers/gettingstarted/what-is-a-driver-)

# Notes
## What is Windows
- Licensed operating system with inaccessible source code
	- User cannot modify the OS code
	- Key difference for Linux
- System designed primarily for business owners and commercial users

## Core Specificities of Windows
- Supports multiple operating environments
	- Windows works on different hardware
- Portability
	- Operating system can go on any machine
- Extensibility
	- The user is able to change the UI
- [[Multitasking|Preemptive Scheduling]]
	- The scheduler determines which programs get CPU resources and when using a quantum of time

### Symmetric Multiprocessing
- Independent threds can calculate at the same time
- The CPU has many cores which contain a heavy thread
- The heavy thread is what each core is running a software
- The core can be divided into many light threads
- <mark style="background: #FFB86CA6;">Light threads are virtual CPU cores that can run independent calculations in parallel</mark>

### Client-Server Computing
- Allows for 2 machines on the same network to communicate by sending binary data packets
	- Uses the localhost connection
- Allows for the communication between 2 apps on the same computer
- The client is like the mouth and the server is like the ears

### Virtual Memory
- <mark style="background: #FFB86CA6;">Hardware memory is managed through the driver</mark>
- Data is virtualized with the address of where it can be found on the disk
