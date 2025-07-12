|       Course Name        |    Topic    |       Professor       |        Date        |       Tags       |
| :----------------------: | :---------: | :-------------------: | :----------------: | :--------------: |
| **SAS Base Programming** | Data in SAS | Jean-Francois Derenty | 07-08 juillet 2025 | #Data_Management |

[Class Video Link 1](https://dstisas-my.sharepoint.com/personal/blaise_pascal_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fblaise%5Fpascal%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FS25%20%2D%20Common%20Link%20DSDEDA%2D20250707%5F085143%2DMeeting%20Recording%201%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E88acc5d2%2Dfc4f%2D475a%2Dbc51%2De1cf29410e87)
[Class Video Link 2](https://dstisas-my.sharepoint.com/personal/blaise_pascal_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fblaise%5Fpascal%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FS25%20%2D%20Common%20Link%20DSDEDA%2D20250708%5F085016%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E63976145%2D234f%2D4912%2Daf63%2D0ac8881e8409)

# Summary
*SAS datasets are tabular objects made up of observations and variables which are stored on disk at physical locations known as libraries. The data within is either of type character or numeric and can only be stored as such, but for reporting, the display values can be changed by using either SAS predefined or custom user-defined formats.*

# Key Takeaways
1. SAS must work with tabular data. Any non-tabular data coming in must be structured but can be read by the system
2. Variable names are case insensitive
3. All SAS datasets are organized into a library on disk (either temporary or permanent)
4. There are only two datatypes in SAS: character and numeric
5. SAS formats will ALWAYS fit the value to the specified length even if that means removing other elements of the formatting like decimals, currency symbols, or commas. This also could truncate strings
6. Overlapping ranges in a user-defined format will cause an error

# Definitions
- SAS Data (Datasets/Tables): Structured data file that SAS creates and only SAS can read which contains observations (rows) and variables (columns)
- SAS Library: Collection of SAS tables that are stored together at the same location on disk
- Temporary Library (`work`): The temporary library is a storage location for intermediate SAS datasets which is maintained only for the duration of the SAS session
- Byte: In SAS, bytes are either the number of characters for a character variable or the actual byte count for numeric variables (default is 8)

# Additional Resources
- [Documentation - SAS Formats](https://documentation.sas.com/doc/en/pgmsascdc/9.4_3.5/leforinforref/n0p2fmevfgj470n17h4k9f27qjag.htm)

# Notes
## SAS Datasets/Tables
- All data in SAS is managed through SAS datasets
	- These are disk tables that only SAS can read and must be organized into observations (rows) and variables (columns)
- Descriptor Portion
	- Displayed used `proc contents data={dataset name};`
		- General properties: name and number of observations
		- Variable properties: name, type, length (number of bytes)
			- Names are 1-32 characters long and contain letters, underscores and numbers (start with letters and underscores only)
- Data Portion
	- Displayed using `proc print data={dataset name};`
	- Contains the actual numeric or character contents/values
## Data Types
- Character
	- Any value ranging from 1-32,767 characters
	- <mark style="background: #FFB86CA6;">Each character is one byte</mark>
	- Missing values are blank
- Numeric
	- Floating point or binary with 8 bytes of storage by default
	- 16-17 significant figures
	- Missing values are `.`
- Dates
	- Stored as a numeric
	- Number of days (positive or negative) <mark style="background: #FFB86CA6;">since January 1, 1960</mark>
- The `input` command allows us to define a schema
	- We can manually create individual observations and write to a SAS dataset using `datalines`
## SAS Libraries
- At startup, SAS creates one temporary (`work`) and one permanent (`sashelp`) library which are open and ready to use
	- SAS datasets can be stored in either of these though `work` is ephemeral
- In [[Basics of SAS and SAS Programs|SAS programs]], we can refer to libraries by their logical name called the "libref"
	- `libref.datasetname`
- There is only one temporary library (`work`) but the user can define any number of permanent libraries using the `libname` command
	- User-defined libraries are not immediately available in the SAS session like `sashelp`. They must be created/activated
		- User creates libraries programmatically using `libname {libref} "physical filepath";`
		- User interfaces provide an option to automatically open these libraries on startup
		- User-defined libraries can be deleted using `libname {libref} clear;`
- We can access all datasets in a library by using `_all_` as the 
	- In a `proc contents {libref}._all_` command, we can add the option `nods` to only see the descriptor portion and suppress the actual data
- A libref may have up to 8 characters and must start with a character or underscore
## Data Formats
- SAS supports only two data formats: character and numeric
- We can however, use the `format` statement to <mark style="background: #FFB86CA6;">change how data is displayed</mark> in reports
	- The underlying data does not change
	- Used in `proc` steps
	- The format statement specifies the variable name then the format all separated by spaces
		- `format Salary dollar8. Hire_Date date9. Term_Date mmddyy10.;`
- SAS format options: `<$>{name}<w>.<d>`
	- `$`: signifies a character format (optional)
	- `{name}`: The name of the SAS or user-defined format
	- `w`: The width (in bytes) of the format
	- `.`: The period is mandatory for all formats
	- `d`: Number of decimal places for numeric variables
- Available formats
	 ![[Pasted image 20250712121519.png]]
	- `Zw.d` is a special format that writes numeric data with leading zeros
- Date Formats
	 ![[Pasted image 20250712121702.png]]
	 ![[Pasted image 20250712121720.png]]
## User-Defined Data Formats
- User-defined formats are created using the `proc format` command
	```sas
	proc format;
		value {format name} range1 = 'label'
							range2 = 'label';
	run;
	```
- Format names
	- The format name should NOT have a period when being defined, unlike during its use
	- Character format names must with a `$`
	- Format names must not end in a number
- Format Ranges (bucket values, tiers, etc)
	- Can be defined using a dash (`-`) inbetween the <mark style="background: #FFB86CA6;">inclusive</mark> lower and upper limits of the range
		- Non-inclusive ranges can be created by putting a `<` either before or after the `-` (though `>` is not used)
	- Numeric ranges support `low` and `high` as keywords which uses the smallest and largest system values respectively
	- Can provide lists of values with the `in` operator
	- Can set labels for missing values
	- Provides an `other` range value
- If a value is not found in any of the ranges, the original value is preserved and displayed