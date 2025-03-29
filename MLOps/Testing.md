| Course Name |              Topic              |         Professor          |       Date        | Tags |
| :---------: | :-----------------------------: | :------------------------: | :---------------: | :--: |
|  **MLOps**  | Software, Data, and Model Tests | Joe Sanchez & Alexis Marié | 04 & 07 mars 2025 |      |

[Professor Notes Link (Continuous Testing)](https://github.com/adaltas/dsti-mlops-2025-spring/blob/main/04.continuous-testing/index.md)

# Summary
*Testing is a necessary activity in the software and machine learning development and deployment lifecycles as it ensures code quality and prevents regressions over time. MLOps includes code tests like DevOps but expands upon it by incorporating data tests with tools like Great Expectations and model tests.*

# Key Takeaways
1. Unit tests are the lowest level of granularity and should be the majority of all tests written
2. MLOps requires more than just software tests - ML infrastructure, model, and data tests are needed as well

# Definitions
- Continuous Testing: The processing of executing automated tests as part of the software delivery pipeline

# Additional Resources
- [Continuous Testing Overview (IBM)](https://www.ibm.com/think/topics/continuous-testing)
- [Great Expectations Docs](https://greatexpectations.io/)
- [Example Great Expectation Implementation - Lab](https://github.com/Egjfour/dsti_mlops_labs/blob/main/notebooks/data_and_model_testing/testing_initial.ipynb)
- [Continuous Machine Learning (CML) module](https://cml.dev/)

# Notes
## Types of Tests
- Unit Tests: Lowest level to test an individual software unit such as a specific function
- Functional Tests: Higher-level testing to look at outside dependencies
	- Get a specific value from a database or API
- Integration Tests: Assembly of modules and seeing how microservices work together
	- Connection to a database is successful
- End-to-End Tests: Application tests in a real environment w/ prod-like database
	- UI and acceptance testing
- Tests should mostly be focused at the unit test level with very few automated GUI tests
- Testing automation is done on a server with a specific configuration
- ![[Pasted image 20250323132129.png]]
## Unit Testing with PyTest

## Test-Driven Development and Best Practices
- Test-driven development (TDD) involves writing a set of failing tests based on acceptance criteria and then writing the code to make the tests pass
- Benefits include higher quality, development time reduction, and solution reliability
- Tests should avoid anti-patterns
	- test case depending on the system state from the previous test
	- dependencies between test cases
	- don't inspect more than necessary
	- slow running tests
- Test location
	- Unit tests should be separated from the source code
	- Typically, code is organized as 
		- /project_root
			- /src
				- /my_module
					- my_module.py
			- /tests
				- /test_my_module
					- test_my_module.py
## Data Testing
- Types of tests
	- Expected columns appear with expected data types
	- Ranges of values and categories expected are found
- Tools to automate this like Great Expectations or Trumania for synthetic data generation
- The `ProfileReport` class from the `ydata_profiling` module in Python allows for quick inspection of data sources
	 ```python
	from ydata_profiling import ProfileReport
	
	 # Generate the profile report with Pandas Profiling
	profile = ProfileReport(
	    data,
	    title="Example of summarization of wine data"
	)
	
	# For Jupyter
	profile.to_notebook_iframe()
	```
## Model Testing
- Includes testing of the entire ML pipeline
- Experiment tracking, combined with [[Version Control (Code, Data, and Model)|versioning]], to monitor performance during development and over time in production
- Elements to test
	- <mark style="background: #FFB86CA6;">Consistency during many calls to the model</mark> (even for non-deterministic algorithms)
	- Algorithm tests (output length, range, and overfitting)
	- Compare to a baseline model
	- Invariance tests
		- By how much can the input change before outputs are affected
	- Directional and perturbation tests
		- How do perturbations in input affect output
	- Minimum functionality tests
		- Assessment of model on specific cases in the data
- CML module can assist with this using workflows
	- Example: execute a pipeline and add a metrics file as a pull request comment
- Also important during model development to utilize train/validation/test sets
	- ![[Pasted image 20250323134459.png]]