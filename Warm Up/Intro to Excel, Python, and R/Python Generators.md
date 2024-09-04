| Course Name |        Topic        |    Professor     |  Date  |              Tags               |
| :---------: | :-----------------: | :--------------: | :----: | :-----------------------------: |
| **Python**  | Introductory Python | Dominique Mariko | 4/9/23 | #Python #Programming #Iteration |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/ted_codd_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fted_codd_nuc_dsti_institute%2FDocuments%2FRecordings%2FS23-%20DS%20%26%20Common%20LINK%20DS_DA_DE-20230323_095916-Meeting%20Recording%201.mp4&ga=1)

# Summary
*A generator is a python iterable that optimizes memory consumption by creating a pointer to the function to execute without saving the result in memory. This allows us to calculate each element of the iterable when desired. These functions can be called with keywords or similarly to a list comprehension.*

# Key Takeaways
1. The results of a generator are not stored in memory at once (more efficient)
2. Generators can be created similarly to a list comprehension but with using parentheses instead of brackets
3. Once a generator has been called for a given element, the value is removed from memory
4. The state of the function is remembered after each execution of a generator

# Definitions
- yield: Python keyword that allows for creating a generator from a user-defined function
- next: Python keyword that allows the user to calculate and access the result of the next element of the generator iterable


# Additional Resources
- [How to use Generators](https://realpython.com/introduction-to-python-generators/)

# Notes
## Generators Initialization and Usage
```
# This function creates a generator using the yield keyword
def example_function(x: list):
	for element in x:
		yield(x ** 2)

# This creates a generator object in python
example_output = example_function([1, 2, 3])

# This also creates the object
example_output = (x ** 2 for x in [1, 2, 3])

# This calls the calculation for the first element and returns 1. That element is no longer a part of the iterable
next(example_output)
```

