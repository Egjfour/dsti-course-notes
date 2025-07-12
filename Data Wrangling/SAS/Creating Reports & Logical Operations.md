|       Course Name        |               Topic               |       Professor       |          Date          |       Tags       |
| :----------------------: | :-------------------------------: | :-------------------: | :--------------------: | :--------------: |
| **SAS Base Programming** | Generating and Formatting Reports | Jean-Francois Derenty | 07-08, 10 juillet 2025 | #Data_Management |

[Class Video Link 1](https://dstisas-my.sharepoint.com/personal/blaise_pascal_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fblaise%5Fpascal%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FS25%20%2D%20Common%20Link%20DSDEDA%2D20250707%5F085143%2DMeeting%20Recording%201%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E88acc5d2%2Dfc4f%2D475a%2Dbc51%2De1cf29410e87)
[Class Video Link 2](https://dstisas-my.sharepoint.com/personal/blaise_pascal_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fblaise%5Fpascal%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FS25%20%2D%20Common%20Link%20DSDEDA%2D20250708%5F085016%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E63976145%2D234f%2D4912%2Daf63%2D0ac8881e8409)

# Summary
*SAS allows us to easily create both detail and aggregated reports. For detailed reports, we use the proc print command which has powerful options for changing display values, layouts, and more. For aggregations, SAS offers several procedures which let us generate frequency and contingency tables, [[Descriptive Statistics|descriptive statistics]], and identify outliers and missing values easily.*

# Key Takeaways
1. Sorting operations are done in-place and are unrecoverable if the `out=` option is not specified
2. To apply a by-group in a `proc print`, the variables must be sorted ascending
3. Titles and footnotes apply to all reports once declared until they are overridden or cancelled
4. The `class` argument of `proc means` lets us calculate variable statistics within the class values

# Definitions
- The `[obs]` column: Used as an identifier for observations (mainly for printed reports with many columns)
- Labels: Friendly names (allow invalid characters like spaces) in the column headers of a report
	- Instead of showing variable name `MarginPct`, we would display "Margin %" as a label
- Extreme values: The n-highest and lowest observations of a variable

# Additional Resources
- [proc means Overview and Examples](https://www.listendata.com/2015/01/sas-detailed-explanation-of-proc-means.html)

# Notes
## Basics of Creating Reports
- Command `proc print data={dataset name};` generates a report
	- The default settings returns all observations, variables, and an `[obs]` column on the left
		- We can define a field to be the `[obs]` column using the `id {var name};` statement (this need not be unique but should be)
	- With the `nobs` option, we can suppress the observation column
- Variables to include and their order are given using the `var` statement
	- Like a [[Basic Querying|SQL SELECT]]
	- Variable names are provided as a space-separated list
- Filtering can be done using the `where` statement
	- Operands are used to make logical comparisons to data values
	- `where` statements are the <mark style="background: #FFB86CA6;">first element processed</mark> during the [[Reading, Writing, and Processing Data|execution phase]]
	- We can compare dates by using date constants
		- Always of the format `'ddmmm<yy>yy'd`
- We can generate total rows using the `sum` statement
	- When reports are grouped, the `sun` statement will also produce subtotals
	- The `sum` statement is <mark style="background: #FFB86CA6;">calculated only on observations which are included in any</mark> `where` <mark style="background: #FFB86CA6;">statements</mark>
## Logical Operators for `where` Statements
- Logical operators can either use symbolic or mneumonic operators
	- The `IN` operator is exclusively mnemonic
	 ![[Pasted image 20250712183125.png]]
- The priority of operators is (in order): NOT, AND, OR
	- Where needed, we can put parentheses around conditions to evaluate first
- Additional comparison operators
	- `IS NULL`, `IS MISSING`, `IS NOT NULL`, `IS NOT MISSING`
	- `BETWEEN {value} AND {value}`
		- Can be used for either numeric or character variables
	- `CONTAINS` finds substrings within characters
	- `LIKE` <mark style="background: #FFB86CA6;">matches a patten more precisely within a character variable</mark>
		- Wildcard characters `_` (single) and `%` (multiple) used for fine-grained control
- Multiple `where` statements
	- We can use the operators `or` and `and`
	- Having multiple separate `where` statements is not supported
		- Only the last one written is retained
	- But `where also` and `where same and` are valid and will retain all previous conditions
## Sorting and Grouping
- Sorting (`proc sort data={dataset name} <out={dataset name}>;`)
	- Must provide the `data=` argument
	- If no `out=` argument is provided, the sort is done in-place in an unrecoverable manner
	- Requires a `by` statement that lists space-separated variable names
		- `descending` flag provided<mark style="background: #FFB86CA6;"> BEFORE the variable name</mark>
		- Multiple variables can provided w/in the `by` statement (each would need its own descending flag if relevant)
- Grouped Reports
	- A grouped report is simply a set of records that output as separate tables visually based on the groupby provided
	- Simply adds a `by` statement to the `proc print`
	- Essential that the variables used in the `by` statement are sorted in the data
		- If not, SAS will throw an error
## Titles, Labels, Footnotes
- Titles and footnotes
	- These are declared as global statements and apply to any reports that come after
	- The default title is "The SAS System"
	- Can have up to 10 titles and footnotes and these will display vertically (like subtitles)
		- If we override/cancel a lower-level title/footnote (e.g., `title2`), all higher-level titles/footnotes are cancelled
		- Not including a number is equivalent to `title1` or `footnote1`
	- Titles/footnotes can be cancelled with an empty title/footnote statement
		- `title;` cancels ALL active titles at all levels
		- `footnote3;` cancels the 3rd-level footnote and any levels 4-10
- Labels
	- Used to make user-friendly column headers on reports
	- Up to 256 characters
	- In `proc print`, the `split='{separator}'` option determines what character in the labels/variable names will be used to separate column headers onto new lines
	- If no label is provided for a variable, it retains its logical name as the label
## Aggregated Reports
- Count Data: `proc freq data={dataset name} <nlevels> <order='{metric name}'>;`
	- Generates a one-way frequency table for each variable provided in the `tables` statement
	- Metric options (`nocum`, `nocount`, `nopercent`, etc.)  provided after a `/` in the `tables` statement
	- Crosstab tables can also be created to show metrics for the combination of variables by combining variable names in the `tables` statement with a `*`
		- example: `tables CustomerTier*ProductTier / nocum;` creates a <mark style="background: #FFB86CA6;">crosstab table</mark> with `CustomerTier` as the rows and `ProductTiers` as the columns with no cumulative count
	- The `nlevels` option can also be used to provide <mark style="background: #FFB86CA6;">distinct counts</mark>
	- Count of missing is also provided
	- `proc freq` supports [[SAS Data, Formats, and Libraries|`format` statements]] too
	- The `order=` option lets us sort a proc freq based on one of the metrics
		- This will always be ordered descending
- Summary Statistics: `proc means data={dataset name} <maxdec = {int}> <nonobs> <list of desired metrics>;`
	- `var` statement specifies the numeric columns to aggregate
	- `class` statement specifies any categorical groupings
		- Should be relatively low cardinality features
	- Produces metrics such as the min, max, mean, etc
		- `N` specifies the number of non-missing observations <mark style="background: #FFB86CA6;">(for that metric within the class) </mark>and `NoObs` is the number of total observations
	- Can specify which metrics we want in the options which overrides the default statistics
		 ![[Pasted image 20250712191229.png]]
- Outliers and Missing Data: `proc univariate nextrobs=<int>;`
	- Shows the `nextrobs` highest and lowest observations (default is 5)
	- Also shows missing counts for each variable in the optional `var` statement
	- Can provide an `id` statement to help traceback extreme values to the original data