|     Course Name      |         Topic          | Professor |    Date    |         Tags         |
| :------------------: | :--------------------: | :-------: | :--------: | :------------------: |
| **Computer Systems** | Computer System Basics | Sebastian | 2023-03-26 | #ComputerEngineering |

[Class Video](https://learn.dsti.institute/mod/url/view.php?id=12623)

# Summary
*An operating system is what allows users to interact with the computer. It is stored on the [[Computer Systems Basics|secondary memory]] but could be stored in many places. A bootloader is needed to provide decidability on where to retrieve the OS.*

# Key Takeaways
1. Loading the operating system is a non-decidability problem because we don't actually know where it's located and there could be multiple operating systems
2. The bootloader is the software that initializes a given storage media. It has a known hard-coded area (norm is to be placed at sector 0)
3. Operating systems are made up of thousands of executable programs

# Definitions
- Non-decidability problem: An algorithmic issue where there is not enough data to make a [[Computer Systems Basics|deterministic]] decision
	- Ex: Windows and Linux are both available to use as the OS on a computer, which do you use and from where do you get it
- Protocol: An agreement on a process
- Bootloader: Any piece of code that executes at or near boot time that is used to load and/or execute the main application

# Additional Resources
- [Bootloaders](https://www.youtube.com/watch?v=Jcan8YfLfLs&ab_channel=TexasInstruments) - first 2 minutes

# Notes
## Launching the Operating System
- Operating systems are stored on the <mark style="background: #FFB86CA6;">secondary memory</mark>
- The Non-decidability problem
	- Because an operating system can be stored anywhere (multiple hard drive locations, flash drive, CD, etc), it is impossible for [[Central Processing Unit|BIOS]] to know exactly where to find the OS
	- We need more data and a protocol to achieve decidability

## The Bootloader
- The bootloader is the intermediate step that tells us where to retrieve the operating system
- It is a hard-coded area on each storage media (typically at sector 0) the gives BIOS decidability for how to [[Computer Systems Basics|"change the tape"]]
- Only visible UI is with Linux. On Windows and Mac OS, it is impossible to interact with the bootloader directly
	- Installing linux changes the bootloader to allow for these things
