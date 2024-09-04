|          Course Name          |         Topic          | Professor |     Date     |     Tags     |
| :---------------------------: | :--------------------: | :-------: | :----------: | :----------: |
| **Software Engineering Pt 1** | Object-Oriented Design | Sebastien | 22 May 2024  | #Programming |
|   Software Engineering Pt 2   | Object-Oriented Design |   Hanna   | 30 July 2024 |   #Python    |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/ted_codd_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fted%5Fcodd%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FS24%2D%20DS%20%26%20Common%20LINK%20DS%5FDA%5FDE%2D20240522%5F095311%2DMeeting%20Recording%201%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E0a8251c0%2Db625%2D4cf9%2Dba1c%2D920870a3f403)

# Summary
*Object-oriented design is based on the concept of encapsulation which states that data and functions relevant to that data should be tightly bound in a class. Objects are the instantiated and executable version of classes. Within a class, we have constructor functions that are called at instantiation to build the object provided a set of inputs. There is always a default constructor, but we can implement others via overloading.*

# Key Takeaways
1. OOP was designed to ensure that structure metadata and functions are well-written and safe to use
2. Classes are merely definitions (like `struct` in [[C Programming Basics|C]]), not executable code
3. Objects are instances of classes and are therefore executable and hold real/concrete data in their attributes (Objects are "instantiated from a class")
4. In OOP, anything, even operators, can be overloaded
5. In all OOP languages, there is a hidden first parameter in every class method called "this" or "self" (not hidden in python. Programmer must explicitly write this)
6. OOP is centered around identifying behaviors that should be reproducible when interacting with an object of a specific class (e.g., when interacting with objects of class `Cat`, we expect to hear it meow and not bark)

# Definitions
- Attribute: Each piece of data in a class object
- Method: Functions in a class object
- Encapsulation: The data of a class should not be accessible outside the class
	- This is the "absolute rule" of OOD. -> Only the methods of a class can read/write attributes of said class (it is arbitrary)
- Right of Access (public vs private): private attributes/methods are fully constrained by encapsulation but public attributes/methods are released  from encapsulation
- Constructor: Method that tells the object how to build upon instantiation
	- `__init()` in Python
- Overloading: Changing the behavior of a class method based on different signatures
	- "in C++, Operator overloading is a compile-time polymorphism. It is an idea of giving special meaning to an existing operator in C++ without changing its original meaning."

# Additional Resources
- [Overloading](https://learn.microsoft.com/en-us/cpp/cpp/function-overloading?view=msvc-170)
- [Operator Overloading](https://www.geeksforgeeks.org/operator-overloading-cpp/)
- [Encapsulation](https://www.boardinfinity.com/blog/a-quick-guide-to-encapsulation-in-c/#:~:text=Encapsulation%20is%20a%20fundamental%20concept,being%20accessed%20by%20other%20classes.)
- [Access Specifiers](https://www.w3schools.com/cpp/cpp_access_specifiers.asp#:~:text=In%20C%2B%2B%2C%20there%20are,be%20accessed%20in%20inherited%20classes.)

# Notes
## Object-Oriented Design and Vocabulary
- OOD is built on the <mark style="background: #FFB86CA6;">fundamental principle of encapsulation</mark> meaning that data and applicable functions should be bound together tightly (opposite of classical design -- C)
	- Python does not implement any encapsulation: Von Rossum didn't believe in it because of getters and setters being so prevalent in OOP
- No math to back this unlike the relational model. Only goal is to encapsulate data & functions together into *semantically-relevant* classes
- A class is a custom-made data structure (like `struct` in C)
	- Within a class, the data elements are called attributes and the functions on that data are called methods
	- These classes also define a data type
- An object is an instance of a class and are executable, unlike class definitions
	- Each object is, by definition, unique with an ID of the pointer address
- Right of access
	- Determined by the programmer
	- private attributes and methods are only accessible by instances of that particular class
	- protected attributes and methods are accessible to [[Inheritance|child objects]] as well
	- public attributes and methods are available to any other objects to interact with
- OOP vs Imperative/Declarative
	- Imperative/Declarative programming has logic that is executed line-by-line
	```python
	sum = 0
	for i in range(5):
		sum+=i
	print(sum)
	```
	- In OOP, we create an object that does what we want
		- In the code snippet below, we define a class that will perform the summation. This means that any time we do a sum calculation, it will always be done the same way
```python
class Summer:
	def sum():
		...

mySummer = Summer()
mySummer.sum(5)
```
## Overloading
- Class methods can have different implementations based on differing function signatures that then also have different implementations
	- Same name, same algorithmic intent, different inputs and (possibly) different outputs
- It is common to see this with constructor functions (the function that is called when an object is instantiated)
	- This is required in OOP because without it, we couldn't change the constructor
	- Constructors always maintain the same name as the class since the code is actually calling {objectName}.{objectName}(function signature)
- Operators are essentially just methods as well and can be overloaded
	```c
	double& Point2D::operator[](int index)
{
	// This index value can only be 0 (for X) or 1 (for Y)
	double value = NAN; // Default to "Not a Number" -- defined in the real number space, not an integer because the mantissa exponent makes it easier
	if (index == 0)
	{
		value = m_X;
	}
	else if (index == 1)
	{
		value = m_Y;
	}
	else
	{
		// This is an EXCEPTION -- signals an error
		// We don't need to stop the program but it is worth signaling

		// An anonymous object of the class exception is created with a constructor of a single overload that takes a string for the message
		throw exception("Index out of bounds");
	}

	return value;
}
```
- The example above shows an operator overload on the `[]` operator allowing us to index into our object via a custom definition