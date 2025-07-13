|       Course Name        |    Topic     |       Professor       |        Date        |       Tags       |
| :----------------------: | :----------: | :-------------------: | :----------------: | :--------------: |
| **SAS Base Programming** | Data Sources | Jean-Francois Derenty | 09-10 juillet 2025 | #Data_Management |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/blaise_pascal_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fblaise%5Fpascal%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FS25%20%2D%20Common%20Link%20DSDEDA%2D20250709%5F084946%2DMeeting%20Recording%201%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E0e4a1d83%2Dfd52%2D4689%2D8889%2D6e0ca6bc6685)

# Summary
*The `data` step is the main way that we process data in SAS. It reads data one observation at a time from disk into the program data vector (PDV) for processing. We can also read from many other sources using engines or the `infile` statement including databases, spreadsheets, and raw text/csv files. Reports can be written to many sources as well including HTML, PDF, and rich text format (RTF) using the Output Data System commands to sink report commands into files. We can also apply logic iteratively in the data steps using do-loops to create and process SAS statements multiple times.*

# Key Takeaways
1. Data in SAS is not stored in [[Computer Systems Basics|RAM]]; it is stored on disk and read in one observation at a time
2. A `keep` statement must have ALL desired fields including newly created fields
3. SAS is an **interpreted language** compiled and executed in small chunks is a fundamental concept in SAS
4. `where` statements are executed before all other steps
5. Because of execution order, we cannot reference newly created variables in a `where` statement, but we can use an `if` statement instead
6. All variables are included in the PDV even if there is a `keep` or `drop` statement
7. The default delimiter for reading raw data files in SAS is a space
8. By default, multiple separators in a row are not read as missing values. To create that behavior, we must specify the `dsd` option in the `infile` statement
9. Since it is part of the PDV, a `length` must come before an `infile` statement
10. When an explicit output is used in a `data` step, there is no longer an implicit output
11. It is possible to drop variables from the input dataset by using a `drop=` option in parentheses when declaring the dataset. This removes the field from the PDV

# Definitions
- [[The Compiling Process|Compilation]]: Scanning of code for syntax errors and translation to machine code
- Program Data Vector (PDV): A [[Data Structures|vector]] initialized during compilation with knowledge of all variables existing and created and their data types
- Execution Phase: The portion of the SAS program which executes the statements one observation at a time using the PDV
- Informat: A format that is applied when reading data from a source
	- Date formats in csv files or currency symbols in numeric fields

# Additional Resources
- [Where vs If](https://www.listendata.com/2013/09/sas-where-vs-if-statements.html)
- [Documentation - Reading Raw Data](https://documentation.sas.com/doc/en/pgmsascdc/9.4_3.5/lepg/p1vahis9wkdkvin17obs1381xenf.htm)
- [Documentation - Iterative Processing](https://documentation.sas.com/doc/en/pgmsascdc/9.4_3.5/lestmtsref/p1cydk5fq0u4bfn1xfbjt7w1c7lu.htm)

# Notes
## Reading and Manipulating SAS Datasets
- We use a `data` step to tell us that we are reading data and to specify the name of the SAS output dataset (`data work.{dataset name}`)
	- The `set` statement of the `data` step tells us from which SAS dataset we want to read
	- We can read/write to either [[SAS Data, Formats, and Libraries|permanent or temporary libraries]]
- Data from SAS datasets is read once observation at a time
- Creating new fields
	- Assignment is one of few statements which has no keyword
	- We simply set the new variable name equal to a statement
		- These can be [[Data Manipulation - SAS Functions|functions]], constants, etc.
- Fields can be selected or dropped with the `keep` and `drop` keywords
## Data Step Processing (Under-the-Hood)
- Two main phases: compilation and execution
- Compilation
	- Scans for syntax errors and translates to machine code
	- Creates the PDV to save each observation in RAM as it is processed
	- Creates the [[SAS Data, Formats, and Libraries|descriptor portion]] of the output dataset
	- <mark style="background: #FFB86CA6;">If a step fails to compile, SAS moves onto the next step</mark>
- Execution (for each observation)
	- Initialize the PDV to missing
	- Execute `set` statement to get the data
		- If EOF, move onto next step
	- Execute other statements
	- Output to SAS dataset implicitly and return implicitly
- Filtering operations
	- Either `where` statements can be used or `if` statements with no `then`
		- `where` statements require the data come from the `set` statement (no newly created fields) but are more performant since no other calculations are performed when a `where` statement is not satisfied
		- `if {condition};` has the same effect, but is less performant since other calculations still must be computed
	 ![[Pasted image 20250713123825.png]]
- The `data` step also allows for assigning permanent labels and formats
	- These will remain in place for any reports using this dataset unless overridden by labels and/or formats specified in the `proc print`
## Reading From Spreadsheets
- Reading from Excel spreadsheets requires an engine. Several exist, but the most robust and easy-to-use is `xlsx` which requires `.xlsx` files
	- Other include `excel` (oldest with many issues) and `pcfiles`
	- The `excel` engine requires the same bitness between the engine and the Excel file
	- `excel` and `pcfiles` are limited to 255 columns since they must support `.xls` files
- The global option `options validvarname='v7'` controls how special characters in column headers are handled
	- V7 converts all spaces/spec. chars to underscores
	- SAS studio and enterprise guide do not enable this by default, so we would need to <mark style="background: #FFB86CA6;">use SAS literals to handle the invalid characters in variables names</mark> (string with an "n" after)
		- Example: 'Job Title'n
- Storage
	- Each sheet is saved as its own SAS dataset inside a [[SAS Data, Formats, and Libraries|library]] that we declare at process time
		- Each named range is also saved separately as its own dataset
		- Declaring the library is actually how the data is read
	- Sheet names are saved with a `$` at the end of the name in the `excel` and `pcfiles` engines, so we must use SAS literals to access them
## Database Data
- SAS can read any [[Relational Database Management System|RDBMS]] (Oracle, MSSWL, SQLite)
- Like spreadsheets, we save into a libref and use an engine
	- Options include `user`, `pw`, `path` (to the db), and `schema`
- Need to pay extra for access to database engines
## Reading Raw Data Files (csv, txt)
- SAS supports reading from both fixed-width and delimited files
	- Default delimiter is a space
	- Can change delimiter using the `dlm=''` option with `infile`
- The `infile` statement (where) provides the file path to the raw data file as a string
- `input` statement (what) is paired with `infile` to specify field names and data types
	- Defines characters by putting a `$` after them
- If using [[Data Storage (S3 and Caching)|cloud storage]], it must be mounted or synchronized via the [[Windows|Windows filesystem]]
	- Cannot provide a SAS token as a file path for example
- The compilation phase for reading raw data creates an input buffer to hold a single observation
- All subsetting (`keep`, `drop`, `label`, `format`, and `if`) is supported EXCEPT `where`
- Missing records must be specified with the `dsd` and `missover` options
## Data Output
- Many data output formats exist for reports (though many are interface-specific)
	- We can choose which destination we write to (HTML, PDF, RTF) using the <mark style="background: #FFB86CA6;">output delivery system (ODS)</mark>
		- Cannot use ODS for Excel. Need the xlsx engine
	- We specify the filepath and format with an `ods` command. Then, we run [[Creating Reports & Logical Operations in SAS|reporting steps]] which will all be added to the report until we call `ods close;`
	```sas
	ods html file="&path\example.html";
	ods pdf file="&path\example.pdf";
	ods rtf file="&path\example.rtf";
	
	proc freq data=orion.sales;
	   tables Country;
	run;
	
	proc means data=orion.sales;
	   var Salary;
	run;
	
	ods html close;
	ods pdf close;
	ods rtf close;
	```
## Iterative Data Processing
- `Do-loop` performs basic iteration and allows us to repeat code operations
	- We either provide a `start`, `stop`, and (optional) `by` options or an item list to iterate through
	- Must have an `end;` statement
	```sas
	data forecast;
	   set orion.growth;
	   do Year=1 to 6;
	     Total_Employees=Total_Employees*(1+Increase);
	     output;
	   end;
	run;
	```
- We can also process until a condition is met (a `while` loop)
	- `do-until` evaluates the condition at the bottom of the loop
		- If the condition is true, one iteration will occur
	- `do-while` evaluates the condition at the top of the loop
		- If the condition is true, zero iteration will occur
	 ![[Pasted image 20250713175558.png]]
- Loops may also be nested