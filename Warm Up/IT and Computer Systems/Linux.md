|       Course Name        |          Topic           | Professor |      Date      |  Tags  |
| :----------------------: | :----------------------: | :-------: | :------------: | :----: |
| **Computer System Labs** | Linux and Bash Scripting |  Clément  | Date of course | #Linux |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/ronald_fisher_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fronald%5Ffisher%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FS24%2DWarmUp%20%2D%20One%2DTime%2DLink%2D20240417%5F092420%2DMeeting%20Recording%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0%3D&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0=&ga=1)

# Summary
*Linux is an open source [[The Kernel and Shell|kernel]] that supports many different distributions. Everything in Linux is a file, and these files are organized into a standard structure that is hardware-agnostic.*

# Key Takeaways
1. Unlike [[Windows|Windows]], Linux is a unified file management system meaning that the storage devices are abstracted from the file location
2. Linux is a kernel and there are many distributions available since it is open-source
	a. This means there is a large community to assist with features and bugs
3. Sending a file or operation to the /dev/null location is how it is deleted
4. File permissions are organized into the user's permissions, the group's permissions, and other's permissions
5. Possible file permissions are read, write, and execute
6. Unlike [[Powershell]], piping sends text as output to the next command
7. Bash Scripts always start with "#!/bin/bash"

# Definitions
- Execute: The execute permission gives the relevant user the ability to run a file OR in the case of directories, to cross through the directory to get to a file or subdirectory
	- INSIGHT SFTP root folder

# Additional Resources
- [Bash Cheat Sheet](https://devhints.io/bash)
- [Linux Command Line Cheat Sheet](https://learn.dsti.institute/pluginfile.php/19586/mod_resource/content/0/linux-command-line.pdf)

# Notes
## Root Directory Folders
- <mark style="background: #FFB86CA6;">bin</mark>: all programs that run on the system
- <mark style="background: #FFB86CA6;">dev</mark>: files for device drivers
- lib: shared library used across the whole system
	- Example: the python installation
	- Also includes lib32, libx32, and lib64
- <mark style="background: #FFB86CA6;">mnt</mark>: mounted hardware
	- The C drive and wsl
- proc: files that interact with the default processes on the OS
- run: saves the state of an app
- snap: allows you to manage apps
- sys: all system files
- usr: saves user info (especially important on multi-user apps)
- boot: how the system [[Operating System|boots]] at the beginning
- <mark style="background: #FFB86CA6;">etc</mark>: application configuration files
- init: initialization of the system
- <mark style="background: #FFB86CA6;">media</mark>: CD, Blu-Ray, and USB
	- any storage that is not the hard drive
- <mark style="background: #FFB86CA6;">opt</mark>: optional (third-party-software)
	- ProgramFiles on Windows
- root: super user of the system
- sbin: system binary (executable for running the OS)
- srv: data file used to run the system
- <mark style="background: #FFB86CA6;">var</mark>: variable file for content that is permanently being evaluated
	- Log files
- <mark style="background: #FFB86CA6;">home</mark>: home directory

## Files and File Permissions
- <mark style="background: #FFB86CA6;">Everything in Linux is a file</mark>
	- Naming is case sensitive
	- There is no need for extensions, any that are added are only for human convenience
- Arranged into 3 groups of permissions
	- User
	- Group
	- Other
- Within each of the groups, we see either a dash or an activated read/write/execute permission
	- Example: rwxrw-r-- would give the user all permissions, the group read and write permissions, and others would only have read permissions
- Groups
	- <mark style="background: #FFB86CA6;">Each file has one and only one group</mark>
	- Users are assigned a primary group by default that can be changed
	- Users can also be assigned to many groups
	- chown command changes the file's ownership
	- chgrp command changes the file's group assignment
- Changing permissions
	- Method 1: chmod command and then the relevant party +/- the change
		- Ex: chmod u+x myFile ~ Adds execute permissions to myFile
	- Method 2: chmod command and then numbers to specify binary permissions
		- Execute = 1
		- Write = 2
		- Read = 4
		- For each group, the permissions are additive, so all 3 is 7 but read and execute is 5
		- Ex: chmod 754 myFile ~ gives the same permissions seen above
## Bash Scripting
- Bash scripting is an old and unforgiving language that allows users to stack linux commands
- These are run directly from the command line
	- Starting the file with "#!/bin/bash" sends it to the execution environment
- Parameters are numbered and accessed using "$param_name"
- The read command allows user input to be provided
