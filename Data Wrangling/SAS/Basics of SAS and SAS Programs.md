|     Course Name      |          Topic          |       Professor       |      Date       |       Tags       |
| :------------------: | :---------------------: | :-------------------: | :-------------: | :--------------: |
| **SAS Base Program** | SAS System and Language | Jean-Francois Derenty | 07 juillet 2025 | #Data_Management |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/blaise_pascal_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fblaise%5Fpascal%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FS25%20%2D%20Common%20Link%20DSDEDA%2D20250707%5F085143%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Eb5404a4e%2D7a61%2D42e1%2Daa2e%2De447a5e4e15c)

# Summary
*SAS is a high-level language and execution engine that allows for the ingestion, processing, and reporting of data from a wide variety of sources and formats. It is an enterprise-scale solution which costs a significant amount of money to license, but also has a lot of functionality. The SAS language itself is a 4th-generation language that is divided into steps which contain statements.*

# Key Takeaways
1. SAS is a 4th-Generation language
2. A step always starts with `data` or `proc`
3. If a step has no defined ending, it will simply wait
4. If SAS encounters an error on a step, it will stop executing THAT step but will move on and try to execute the next one

# Definitions
- SAS: A suite of business solution technologies to be used as a statistical decision engine to help solve business problems
- 4th-Generation Language: You say what you want not how to get there
	- The [[Relational Database Management System|SQL execution engine]] or [[Spark|Spark lazy evaluation]]
- SAS Program: A sequence of one or more steps
- Step: A sequence of SAS statements

# Additional Resources
- [SAS Style Guide](https://support.sas.com/resources/papers/proceedings/proceedings/sugi29/258-29.pdf)

# Notes
## Overview
- SAS is a leader in data cleaning which is the most important and time-consuming task of a data scientist
- 3 User Interfaces Available
	- SAS Windowing Environment: Basic editor, log, and output window
		- Oldest and most difficult to use
	- SAS Enterprise Guide
	- SAS Studio
- SAS lets us access and manage data across many sources and perform analysis to deliver information
## SAS Programs
- `data` steps create SAS data and `proc` steps process SAS datasets to [[Creating Reports & Logical Operations in SAS|generate reports]]/graphs and manage data 
- Programs are sequences of steps and steps are sequences of statements
	- Step boundaries are the start of the step which is always either a `data` or `proc` statement and the end of the step which is either a `run`, `quit`, or start of another step
	- If there is no end detected, the step will wait and not calculate or move on
- SAS programs can either be executed in interactive mode (using a UI) or in batch mode for background processing
- Syntax
	- SAS programs are compiled before execution, so syntax errors are found at compile time
	- All statements start with an identifying keyword and <mark style="background: #FFB86CA6;">end with a semi-colon</mark>
	- Syntax is free-format (no rules for tabs/new lines)
	- <mark style="background: #FFB86CA6;">SAS keywords are not case-sensitive</mark>
		- But string comparisons are
	- Comments are denoted either with
		- `* my comment;`
		- `\* My comment *\`
	- Comments are written to the log but not executed
- Recommended Code Formatting
	- Begin each statement on a new line
	- Use white space to separate words and steps
	- Indent statements within a step
	- Indent continued lines in multi-line statements