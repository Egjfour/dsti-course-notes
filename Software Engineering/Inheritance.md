
|          Course Name          |       Topic        | Professor |      Date       |     Tags     |
| :---------------------------: | :----------------: | :-------: | :-------------: | :----------: |
| **Software Engineering Pt 1** | Class Inheritance  | Sebastien |   23 May 2024   | #Programming |
| **Software Engineering Pt 2** | Python Inheritance |   Hanna   | 1-2 August 2024 |   #Python    |

[Class Video Link 1](https://dstisas-my.sharepoint.com/personal/gordon_moore_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fgordon%5Fmoore%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FS24%2D%20DS%20%26%20Common%20LINK%20DS%5FDA%5FDE%2D20240523%5F094936%2DMeeting%20Recording%201%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E73b4737e%2Dfb64%2D48d8%2D8168%2D2ac6f09e915c)
[Class Video Link 2](https://dstisas-my.sharepoint.com/personal/johnny_najjar_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fjohnny%5Fnajjar%5Fdsti%5Finstitute%2FDocuments%2FRecordings%281%29%2FS24%2D%20DS%20%26%20Common%20LINK%20DS%5FDA%5FDE%2D20240801%5F095054%2DMeeting%20Recording%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Ee9de34ff%2D30d4%2D4017%2D82a1%2D8030411d0234)

# Summary
*Inheritance allows us to create classes which inherit attributes and methods from other classes. This is useful because it allows for law enforcement and specialization. An important note is that all child classes are also instances of their parent class (`isinstance(child_class, "ParentClass")` will return true in Python). Inheritance also allows for abstract classes which are templates that help with law enforcement within classes as well as metaclasses which are used to define how a class is constructed (python only)*

# Key Takeaways
1. A child class is both of type ChildClass and MotherClass (represented by an "is-a" relationship)
	a. The data type of the child class is also the data type of the mother class
2. Initialization is not immediate in a child class. We need a `super()` function or initializers for it
3. As soon as a class had one pure virtual method, it becomes abstract (C++)
4. Python supports multiple inheritance where we can have a class that inherits from more than one parent class in different class hierarchies
5. Python resolves multiple overrides first at a given level and then from left to right from the inheritance definition
	a. `mro()` (method resolution order) method shows where methods/attributes come from first
6. The sole purpose of metaclasses is to create other classes
7. Abstract classes <mark style="background: #FFB86CA6;">do not create classes</mark>, they are simply templates

# Definitions
- Inheritance: The ability of a [[Object-Oriented Design|class]] to get methods/attributes from another class
- Law Enforment: Imposing upon a class, through inheritance, an obligation to implement a particular method
	- For example, we can enforce that all children have a `toString()` method
- Abstract Classes: A type of class that cannot be instantiated and exists to serve as a generic "template" of what to do
	- Base classes
- Pure Virtual Method: A method that is defined in a class which cannot provide its code but instead leaves implementation to the child classes
- Dynamic Ascending Transtyping: [[Polymorphism|Virtual methods]] required that are not in the child class but are instead inherited from the mother class

# Additional Resources
- [Inheritance](https://www.geeksforgeeks.org/inheritance-in-c/)
- [Abstract Classes](https://www.ibm.com/docs/en/zos/2.4.0?topic=only-abstract-classes-c)
- [Type Templates](https://learn.microsoft.com/en-us/cpp/cpp/templates-cpp?view=msvc-170)
- [Abstract Classes in Python](https://www.docstring.fr/glossaire/classe-abstraite/)
- [Metaclasses in Python](https://realpython.com/python-metaclasses/)

# Notes
## Inheritance General
- Main goal is to maximize code reusability
- Inheritance creates an "is a" relationship between a child class and a mother class which permits a child class to get methods/attributes from another class
- The child class is BOTH of type ChildClass and MotherClass
	- Corollary: the data type ChildClass is also the data type MotherClass
- In most OOP languages, ALL classes inherit from a "mother of all classes" (not C++)
	- Includes standard modules like toString
- Overloading vs Overwriting vs Overriding
	- Overloading: Explicitly adding multiple behaviors for the same function based on different function signatures
	- Overriding: Replacing the behavior of the parent method in the child method
	- Overwriting: Squashing one thing with another completely such that the old version no longer remains
## Law Enforcement and Specialization
- Impose that all children of a given class "C" implement methods from C
	- Implementation is imposed on the child class
	- These methods are called interfaces
```c
class Base
{
public:
	virtual string toString() = 0;

};
```
- In the example above, we create a base class with a pure virtual method `toString()`
	- Classes that inherit from Base will be required to implement their own `toString()`
- In Python, this is handled with <mark style="background: #FFB86CA6;">Abstract Classes</mark>
	- Abstract classes (in both C++ and Python) cannot be instantiated
	- Python leverages the ABC module to define an abstract class and the `@abstractmethod` decorator to identify pure virtual functions
	```python
from abc import ABC, abstractmethod

class Vehicle(ABC):
    '''This class inherits from (or subclasses) ABC'''
    
    @abstractmethod
    def number_of_wheels(self):
        '''This method is abstract, so the class cannot be instantiated.
        This method will be overridden in subclasses of Vehicle.'''
        pass
        

class Car(Vehicle):
    '''This class inherits from the abstract base class Vehicle'''

    def number_of_wheels(self):
        '''Override the abstract method in the base class'''
        return 4

# create a car called c: SUCCEEDS
c = Car()

# print the number of wheels that c has: SUCCEEDS
print(c.number_of_wheels())
```
## Type Templates
- Construction of classes, attributes, or method signatures with a symbol stating "the type will be provided when used"
## Child Class Initialization
- Attributes are not inherently initialized and <mark style="background: #FFB86CA6;">if we try to call the constructor of the parent w/in the child, it will not work</mark> since the parent initialization will create a new object
- In many OOP languages, there is a `super()` function that explicitly calls the constructor or the mother class. C++ does not have this due to multiple inheritance
- C++ uses initializers to accomplish this
	- General principle: run this BEFORE anything else
```c
LineSegment2D::LineSegment2D(Point2D& const pointA, Point2D& const pointB):StraightLine2D(pointA, pointB)
{
	// How are gradient and intercept being computed. Namely, we need to define how StraightLine2D is constructed w/in the LineSegment

	// No code duplication. We already have a constructor for StraightLine2D with 2 Point2D objects

	// We call the xtor of SL2D with the input params
	// This is actually wrong. It is creating a local, anonymous object of SL2D but nothing is performed in the current LineSegment2D object
			// StraightLine2D(pointA, pointB);

	// Instead we need to use INITIALIZERS which say "Run this BEFORE running anything else"
		// No need to write anything else here. We only write the code specific to line segment!

	//we'll set the norm formula later, NAN for now
	double x1, x2, y1, y2;
	
	// In the initial implementation, we cannot access attributes from StraightLine2D (chiefly the 2 points) even though it has been initialized
	// However, they do exist... We need access level modifiers to get them (private, public, and protected)
	// Protected means that the attributes are accessible to the class itself (like private) AS WELL AS CHILDREN OF THE CLASS

	x1 = this->point1->operator[](0);
	y1 = this->point1->operator[](1);

	x2 = this->point2->operator[](0);
	y2 = this->point2->operator[](1);

	this->m_Norm = sqrt(pow((y2 - y1), 2) + pow((x2 - x1), 2));
}
```

## Python Mother Class
- `type` in Python is what creates classes for us. Everything inherits ultimately from this "mother of all classes"
- When we define a new class with the `class` keyword, Python is actually making a call to `type`
- As a constructor, `type()` has 3 arguments: class name, superclasses (inheritance), and the attribute dictionary
- We can access type directly to create our own class factory (Metaclasses)
	- This is specific in Python and is not supported in many OOP languages
## Python Metaclasses
- Metaclasses
	- In Python, these are classes whose instances themselves are classes
	- Inherit directly from [[Python Classes|type, the mother of all classes]]
		- The call to `type()` is overridden with the metaclass definitions when provided
	- Many uses including:
		- Logging and profiling
		- Interface checking
		- Registering classes at creation time
		- Automatically adding new methods
		- Automatic property creation
		- Proxies
		- Automatic resource locking/synchronization
	```python
class FuncCallCounter(type):
    """ A Metaclass which decorates all the methods of the
        subclass using call_counter as the decorator
    """

    @staticmethod
    def call_counter(func):
        """ Decorator for counting the number of function
            or method calls to the function or method func
        """
        def helper(*args, **kwargs):
            helper.calls += 1
            return func(*args, **kwargs)
        helper.calls = 0
        helper.__name__= func.__name__

        return helper

    def __new__(cls, clsname, superclasses, attributedict):
        """ Every method gets decorated with the decorator call_counter,
            which will do the actual call counting
        """
        for attr in attributedict:
            if callable(attributedict[attr]) and not attr.startswith("__"):
                attributedict[attr] = cls.call_counter(attributedict[attr])

		# Like our alternative constructors, we still need to use the __new__
		# method from type to do memory allocation and other tasks
        return type.__new__(cls, clsname, superclasses, attributedict)

  

class A(metaclass=FuncCallCounter):
    def foo(self):
        pass

    def bar(self):
        pass

  

if __name__ == "__main__":
    print("Initializing class!")
    x = A()
    print("Class initialized!")
    print("foo calls:", x.foo.calls)
    print("bar calls:", x.bar.calls)
    print("Calling foo!")
    x.foo()
    print("foo calls:", x.foo.calls)
    print("bar calls:", x.bar.calls)
    print("Calling foo!")
    x.foo()
    print("Calling bar!")
    x.bar()
    print("foo calls:", x.foo.calls)
    print("bar calls:", x.bar.calls)
	```