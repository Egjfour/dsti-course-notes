|       Course Name        | Topic |       Professor       |        Date        |       Tags       |
| :----------------------: | :---: | :-------------------: | :----------------: | :--------------: |
| **SAS Base Programming** | Topic | Jean-Francois Derenty | 09-10 juillet 2025 | #Data_Management |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/blaise_pascal_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fblaise%5Fpascal%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FS25%20%2D%20Common%20Link%20DSDEDA%2D20250709%5F084946%2DMeeting%20Recording%201%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E0e4a1d83%2Dfd52%2D4689%2D8889%2D6e0ca6bc6685)

# Summary
*SAS offers many functionalities to manipulate data beyond simple row-level operations. We can group, merge, and accumulate data. SAS datasets can also be concatenated together. While SAS offers many of these functionalities, some (particularly match merging) are complicated and clunky, so the `proc sql` procedure allows for more simple data processing.*

# Key Takeaways
1. Functions can be used in any SAS expression and can be composite functions
2. Conditional statements on string comparisons are case sensitive. `upcase()` and `lowcase()` functions can align mismatched casing
3. Match merging works like a full outer join in SQL
4. Match merges require a common variable that is sorted in both datasets
5. When we specify any number of explicit outputs, there is no longer an [[Reading, Writing, and Processing Data (SAS)|implicit output]]
6. SAS automatically converts from character to numeric when a character variable is used in a numeric context

# Definitions
- `Do` Processing: Combining multiple statement in the same branch of a conditional logic flow

# Additional Resources
- [SAS Merging Tutorial](https://www.listendata.com/2015/01/sas-merging.html)

# Notes
## Basic Data Wrangling Functions
- Usage of SAS functions
	- Can be used with assignment operator
	- Enclosed with parentheses with arguments separated by commas
- `sum` function
	- Calculates a sum for an observation <mark style="background: #FFB86CA6;">across variables</mark>
	- Ignores missing values by default (unlike `+`)
- Date functions (`month`, `day`,  `year`, `qtr`, `mdy`)
	- `mdy` function creates a [[SAS Data, Formats, and Libraries|SAS date]] from a integer month, day, and year values
- Conditional Logic
	- Basic format: `if {statement} then {action} <else if ...> <else ...>;`
	- Will create missing values if action is assignment and no condition is true
- Multiple-Action Conditional Logic
	- We can use a `do` group to have multiple actions for a condition
	- Requires that we specify an `end` for the `do` block
	- <mark style="background: #FFB86CA6;">Length of character variables should be specified first</mark> since it would otherwise be set at [[Reading, Writing, and Processing Data (SAS)|compile time to add to the PDV]] using the first value seen in assignment
	```sas
	data work.sales_summary;
		/* MUST set length otherwise the compiler would choose 5 ("Large") */
		length OrderSize $6.;
		set work.sales;
		/* Only need to add approval for large orders */
		if Revenue >= 10000 then do;
			OrderSize = "Large";
			ApprovalNeeded = 1;
		end;
		* Set order size for reporting;
		else if Revenue >= 5000 then
			OrderSize = "Medium";
		else OrderSize = "Small";
	run;
	```
## Concatenation and Joining
- Two tables can be concatenated in the `data` step by listing them both in the `set` statement
	- This will read the observations from each table in the <mark style="background: #FFB86CA6;">order that the tables are listed</mark>
	- The datasets don't have to have the same data. Columns not present in one dataset which are in another are filled with [[SAS Data, Formats, and Libraries|missing]]
	- Can rename columns as necessary with the `rename` dataset option
		 ![[Pasted image 20250713170511.png]]
- Match Merging
	- Instead of the `set` keyword, we use `merge` and specify a `by` statement
	- Acts as a full outer join and requires a matching variable in each dataset
	- The merge variable must be sorted in each dataset
	- In practice, `proc sql` is far easier for joining
		- Must put a `quit;` statement after the query
## Splitting Data
- Data can be divided into multiple [[SAS Data, Formats, and Libraries|SAS datasets]] by writing outputs explicitly in a data step
	- This will mean there is no more implicit output
- We can specify which dataset to write to among the ones declared at the top of the `data` step
	- If there are no explicit outputs, we <mark style="background: #FFB86CA6;">output implicitly to all declared datasets</mark>
- Conditional logic for dataset writing
	- A switch-type function can be used with the `select({var name}) when {value(s)} output {SAS dataset} <otherwise>`
- We can use the `obs` and `firstobs` arguments to control the upper and lower limits (respectively) for which observation numbers are read
	- Only applies to the input dataset
## Multi-Row and Grouped Calculations
- Accumulation Across Observations
	- Recall that SAS reads data one row at a time and the PDV has only enough data to hold one record at a time
	- The `retain` statement lets us remember the current value of a variable in the next observation instead of re-initializing on return by changing the PDV at compile time
		- Must be initialized to a value and stated before the first use of the variable
		- If a retain runs into a missing value, it will become missing
		- OR we can state the variable and the addition and <mark style="background: #FFB86CA6;">it will be created, retained, and ignore missing values</mark>
			 ![[Pasted image 20250713172814.png]]
- Grouped Values
	- By-group processing requires [[Creating Reports & Logical Operations in SAS|sorted data]]
		- If sorted by multiple variables, we can group by multiple variables
	- Grouped operations keep track of a `First` and `Last` within each group
		- Automatically updates when higher level group updates
		- We can check if something is the first or last observation in a conditional by using `{groupby var name}.First` or `{groupby var name}.Last`
## SAS Functions
- Many functions for data manipulation and statistical procedures
- Selecting many columns with variable lists
	- Requires the `of` keyword inside the SAS function
	- Single dash to specify ranges of names and double dash for ranges of column indices
	- Example: `sum(of Qtr-Qtr4)` - sum of columns alphabetically between "Qtr1" and "Qtr4"
- String Functions
	- `substring(var name, start, <length>)`: Substring of a string from the start position
	- `propcase()`: Capitalized first letters of each word (space delimited)
	- `scan(string, n, <charlist>)`: Works like `strsplit` to separate a string (comma by default) and choose an index of the list
		- A missing value is returned if there are fewer than n words in the string.
		- If n is negative, the SCAN function selects the word in the character string starting from the end of string.
		- The length of the created variable is the length of the first argument starting in SAS release 9.4.
		- The length of the created variable is 200 bytes in SAS release 9.3 and earlier.
		- Delimiters before the first word have no effect.
		- Any character or set of characters can serve as delimiters.
		- Two or more contiguous delimiters are treated as a single delimiter
	- `catx()`: Concatenates strings using a separator and trims whitespace
- Numeric Functions
	- Can apply [[SAS Data, Formats, and Libraries|informats]] using the `input()` function
	- SAS converts strings to numeric when used in a numeric context (assignment to numeric, arithmetic operation, logical comparison with a numeric, or fxn with numeric args)
		- This uses the `w.` informat
		- Automatic numeric to character conversion uses `best12.` format which <mark style="background: #FFB86CA6;">has leading whitespace</mark>
		- Instead, we can use the `put` function to specify the storage format for the data
			```sas
			data conversion;  
			   NVar1=614;  
			   NVar2=55000;  
			   NVar3=366;  
			   CVar1=put(NVar1,3.);  
			   CVar2=put(NVar2,dollar7.);  
			   CVar3=put(NVar3,date9.);  
			run;
			```