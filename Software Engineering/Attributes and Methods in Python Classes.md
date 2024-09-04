|          Course Name          |     Topic     | Professor |              Date               |         Tags         |
| :---------------------------: | :-----------: | :-------: | :-----------------------------: | :------------------: |
| **Software Engineering Pt 2** | OOP in Python |   Hanna   | 30-31 July 2024 & 1 August 2024 | #Programming #Python |

[Class Video Link 1](https://dstisas-my.sharepoint.com/personal/johnny_najjar_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fjohnny%5Fnajjar%5Fdsti%5Finstitute%2FDocuments%2FRecordings%281%29%2FS24%2D%20DS%20%26%20Common%20LINK%20DS%5FDA%5FDE%2D20240730%5F094914%2DMeeting%20Recording%201%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E974efbb5%2D9128%2D471f%2Db4ed%2D5bc89a0e963c)
[Class Video Link 2](https://dstisas-my.sharepoint.com/personal/johnny_najjar_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fjohnny%5Fnajjar%5Fdsti%5Finstitute%2FDocuments%2FRecordings%281%29%2FS24%2D%20DS%20%26%20Common%20LINK%20DS%5FDA%5FDE%2D20240731%5F095222%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E389fba66%2D247c%2D465e%2D98c0%2De3b16054cac6)
[Class Video Link 3](https://dstisas-my.sharepoint.com/personal/johnny_najjar_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fjohnny%5Fnajjar%5Fdsti%5Finstitute%2FDocuments%2FRecordings%281%29%2FS24%2D%20DS%20%26%20Common%20LINK%20DS%5FDA%5FDE%2D20240801%5F095054%2DMeeting%20Recording%201%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E1a585aed%2D660c%2D4086%2D8083%2D1e8888cfa57d)

# Summary
*Python has two levels for storing attributes and methods within a class: at the class level or at the instance level. All these methods and attributes are stored in a dictionary which can be accessed. Even "private" attributes are available in this dictionary since Python just uses name mangling in the attribute dictionary. Special methods (magic/dunder) exist that override default behavior in classes such as constructors.*

# Key Takeaways
1. All attributes and methods in a [[Python Classes|python class]] are stored in a dictionary
2. When we create an `__init__()` method for our classes, the implementation in the mother of all classes (type) is preserved and <mark style="background: #FFB86CA6;">our code is added to the steps of execution</mark>
3. Python does not have private attributes. Using the double underscore simply performs a name mangling in the attribute dictionary though it is still very much public
4. Data Hiding: Ability to protect/hide some attributes
5. The main use case for properties is to apply constraints to an attribute when it is being set
6. When you invoke any callable in Python by using parentheses, you're actually calling the `__call__()` magic method for the object being referenced

# Definitions
- Attribute: Characteristics that identify a given object
	- class of Flower would have attributes such as num_petals, petal_color, etc
- Method: Functions that allow objects to perform actions with input/output
	- class of Flower would have a method `Flower.photosynthesize()`
- Magic/"Dunder" (Double-Underscore) Method: Methods that allow for operator overloading
	- The `__init__()` method overload in our defined class adds steps to the default [[Object-Oriented Design|constructor]]
- Static Method: A method that can be called via the class name or instance but does not need a reference instance (`self`) to be passed to it
	- A lot of utility methods will go here. For example, if I have a function that simply adds two numbers x and y, I don't need an object for that.
	- Anything that *could*, in theory, be defined outside of the class because it doesn't use any attributes from an instance of a class

# Additional Resources
- [Magic/Dunder Methods](https://www.geeksforgeeks.org/dunder-magic-methods-python/)
- [__str__ vs __repr__](https://stackoverflow.com/questions/1436703/what-is-the-difference-between-str-and-repr#2626364)
- [Static, Class, and Instance Methods Explained](https://www.youtube.com/watch?v=PIKiHq1O9HQ)
- [__call__ method](https://realpython.com/python-callable-instances/)

# Notes
## Methods and Attributes Overview
- Attributes are object properties that should be defined for each instance but would be different from instance to instance (Nouns: name, age, etc)
- Methods are functions that are identical across all instances of a given class. These define how an object will interact with various input/output
```python
class Person:
	# Class Attributes (Applies to all instances of a given class)
	species = 'Human'
	planet = 'Earth'
	def __init__(self, name, age, gender): # First argument is the object ("self")
		# In the __init__ method, we set the instance attributes
		self.name = name
		self.age = age
		self.gender = gender

	# Now we define other methods that define how a person inteacts with the world
	def speak(self, listener):
		...

	def work(self, job, num_hours):
		...
```
- In Python, all the attributes and methods are saved to a dictionary that can be accessed using the `__dict__()` method. This is why we get an `AttributeError` when we try to access an attribute that does not exist
	- To get around this, Python has a built-in `getattr(obj, '{attribute_name}', {default_value})` method that can be used with a default provided
## Magic Methods and `__init__()`
- The `__init__()` method is the default python constructor that allocates memory and assigns objects (there is no explicit constructor/destructor in Python)
- <mark style="background: #FFB86CA6;">All magic methods use the "dunder" (double-underscore) syntax on both sides</mark>
- When we override a magic method in our classes, we are simply changing the default behavior using a [[Polymorphism|polymorphic overload.]] 
	- For example, the default `__str__()` method on an object would simply print out the class name and memory address (since it inherits this behavior from `object`)
	- Our defined version is then chosen when we call `__str__()` via [[Polymorphism|dynamic ascending transtyping]]
- `__str__()` and `__repr__()`
	- Both of these methods create a string representation of a class
	- When the `print` function is called, the `__str__()` method is what is invoked
		- If there is no `__str__()` method defined for a class, Python will look for a `__repr__()` method definition instead
	- These methods do not call each other. The main difference between them is that `__str__()` is meant to be used to create a user-readable format versus `__repr__()` which is meant to be passed to and then evaluated by the Python interpreter
		- via the `eval()` function
## Data Abstraction
- [[Object-Oriented Design|Encapsulation]] is the defining principle of object-oriented programming
	- Guido von Rossum didn't believe in this, but programming paradigms within Python allow us to simulate encapsulation but it is easy to get around
- Encapsulation is useful in OOP because it allows for data hiding
	- We choose a "setting" for our attributes: public, protected (only can be used in the [[Inheritance|inheritance hierarchy]]), or private
	- "getters and setters" are used to read/modify the attributes
- Python kind of allows this, though private attributes are simply name mangled and are still accessible in the attribute dictionary
## Properties
- Getters (accessors) and setters (mutators) are used to access private attribtes in OOP
	- In Python, these are unnecessary since <mark style="background: #FFB86CA6;">every attribute is public</mark> meaning that there is <mark style="background: #FFB86CA6;">no data encapsulation</mark>
- The `@property` decorator lets us interface with a class and define setters that will be applied
	- We can have validation as we set or change attributes (i.e., attribute is less than a value)
	- This decorator is considered the more pythonic way to do things as opposed to having defined getter and setter methods
```python
class OurClass:
    def __init__(self, a):
        self.OurAtt = a

	# This defines OurAtt as a property and sets a getter
	# Python will use name mangling to set the attribute OurAtt to __OurAtt
    @property
    def OurAtt(self):
        return self.__OurAtt

	# When the value of OurAtt is changed, it will go through the validation
	# which constrains it between 0 and 1000
    @OurAtt.setter
    def OurAtt(self, val):
        if val < 0:
            self.__OurAtt = 0
        elif val > 1000:
            self.__OurAtt = 1000
        else:
            self.__OurAtt = val

x = OurClass(10)
```
## Class Attributes and Methods
- Class attributes are assigned to a whole class and are applied to all instances <mark style="background: #FFB86CA6;">unless a specific instance overrides it</mark>
	- Ultimately, it is a matter of which attribute dictionary Python finds the specified attribute in. The instance level is checked first
	- These are very useful for things like counters and loggers
- Class methods
	- Class methods are a type of static method that is bound to a class but not an instance of that class
	- They always take as the first argument `cls` which passes a reference to the class object, <mark style="background: #FFB86CA6;">NOT any particular instance of the class</mark>
	- These are decorated with `@classmethod`
		- Static methods, by contrast, use the `@staticmethod` decorator
	- They are often used, where we have static methods, which have to call other static methods. To do this, we would have to hard code the class name if we had to use static methods. This is a problem if we are in a use case where we have inherited classes.
	```python
class fraction(object):

    def __init__(self, n, d):

        self.numerator, self.denominator = fraction.reduce(n, d)

	# This is static because it can be used w/ any two numbers
	# In theory, it could be defined outside any class,
	# but that would break encapsulation
    @staticmethod
    def gcd(a,b):

        while b != 0:

            a, b = b, a%b

        return a

	# This is a class method because it doesn't need a specific instance
	# (n1 and n2 are provided as parameters not accessed via self)
	# but to have access to gcd(), we need to have access to the class
    @classmethod
    def reduce(cls, n1, n2):

        g = cls.gcd(n1, n2)

        return (n1 // g, n2 // g)

    def __str__(self):

        return str(int(self.numerator))+'/'+str(int(self.denominator))
```
	-  Class methods can also be used to create alternate constructors (see YouTube above)
		- These do need to be called separately when the object is instantiated
		- Example: `model.from_pretrained()` from Huggingface transformers
		- This is *similar* to [[Object-Oriented Design|constructor overloading]] in C++, though the constructor to call is not resolved by the compiler. We must call the correct one ourselves
```python
from typing import Self # This is used to strong-type the alt. constructor
class Person:
	# Standard Constructor
	def __init__(self, name, age):
		self.name = name
		self.age = age

	# Alternative constructor - define birth year and calculate age
	# This is a class method because we will be returning the class
	@classmethod
	def from_birth_year(cls, name, birth_year) -> Self:
		current_year: int = date.today().year
		age: int = current_year - birth_year
		# We precompute attributes to pass to the real constructor __init__()
		return cls(name, age)

if __name__ == "__main__":
	# Standard constructor where we provide the attributes expected in __init__
	julien = Person(name = 'Julien', age = 24)
	
	# Now we define using the birth year by calling the alt. constructor
	eddie = Person.from_birth_year(name = 'Eddie', birth_year = 1998)
```
## Callables
- Callables are objects that override the `__call__()` method to allow them to have the behavior of a function
- We can check to see if something is able to be called using the `callable()` function
- Use cases for doing this (see link above)
	- Writing stateful callables (remember the value from the last calculation and use it)
	- Caching computed values between calls
	- Creating convenient and user-friendly APIs
```python
class StraightLines():
    def __init__(self, m, c):
        self.slope = m
        self.y_intercept = c

	# We know the line params, so the class can calculate the line internally
    def __call__(self, x):
        return self.slope * x + self.y_intercept

line = StraightLines(0.4, 3)

# We compute the y-value for many provided x values using our callble class
for x in range(-5, 6):
    print(x, line(x))
```