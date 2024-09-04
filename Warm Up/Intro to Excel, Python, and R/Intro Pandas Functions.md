|     Course Name     |      Topic       |    Professor     |  Date  |             Tags             |
| :-----------------: | :--------------: | :--------------: | :----: | :--------------------------: |
| **Intro to Python** | Pandas Functions | Dominique Mariko | 4/9/23 | #Python #Pandas #Programming |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/ted_codd_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fted%5Fcodd%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FS23%2D%20DS%20%26%20Common%20LINK%20DS%5FDA%5FDE%2D20230324%5F095914%2DMeeting%20Recording%2Emp4&ga=1)

[Notebook Link](http://localhost:8888/notebooks/OneDrive/Documents/DSTI/Warm%20Up/Intro%20to%20Python/Bank%20Data%20-%20Pandas%20and%20Scikit/First_Pandas.ipynb)

# Summary
*Pandas is a flat vectorized data structure that stores data in columns and rows. It allows for indexing, querying, and different aggregation methods. This is the most common package for data wrangling in python.*

# Key Takeaways
1. Pandas data frames are vectorized representations of panel data
2. Pandas comes with many built-in methods that allow for data manipulation and summarization
3. Pandas can import many data types such as CSV, SQL, and parquet formats

# Definitions
- Index: The reference for the row or column (can have a multi-key index)
	- Must be unique

# Additional Resources
- [Pandas Documentation](pandas.pydata.org)
- [Pandas Crosstab](https://pbpython.com/pandas-crosstab.html)

# Notes
## Summarization
- Import Data
	- Pandas can read many datatypes. CSV files will be quite common
	- File encoding methods can sometimes cause data to not import properly (most common is UTF-8)
- Describe method
	- Defaults to only quantitative variables and shows mean, median, and 5-number summary
	- Can be updated to provide counts and distinct counts for categorical variables
	- This can also be called on a series object to return the same output as a series
		```
		df.describe(exclude = [np.number])
		```
* crosstab method
	* Allows for a quick pivot summary of two columns in a dataframe
	* Normalize shows the values as a percentage of the total
	* Margins shows the row and column totals
	```
	df.crosstab(index, columns, values = None, margins = False, normalize = False)
	```
* head
	* Allows you to see the first couple rows of a dataset
* value_counts
	* Lets you see the count by value for a variable

## Indexing and Filtering
- Filter by column name
	- Filters are specified in brackets
	- Multiple filters must be contained within parentheses
	- Uses bit-wise boolean operators (& and |)
	```
	df[(df.column == 'value') & (df.column2 != 'value 2')]
	```

