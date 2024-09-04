|          Course Name          |    Topic     | Professor |    Date     |     Tags     |
| :---------------------------: | :----------: | :-------: | :---------: | :----------: |
| **Software Engineering Pt 1** | Polymorphism | Sebastien | 24 May 2024 | #Programming |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/gordon_moore_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fgordon%5Fmoore%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FS24%2D%20DS%20%26%20Common%20LINK%20DS%5FDA%5FDE%2D20240524%5F095027%2DMeeting%20Recording%201%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E6b8e88c8%2D8029%2D4ed7%2D99c8%2De25ac3f71216)

# Summary
*Polymorphism is a mechanism for providing an implementation of a particular method within a [[Inheritance|child class]]. Polymorphic methods have the same signature across the inheritance hierarchy but can and often do have very different code/implementations. The correct implementation is identified using dynamic ascending transtyping.*

# Key Takeaways
1. Polymorphic behavior is suited and preserved for pointers but not for objects passed by copy
2. In C++, the developer chooses to activate polymorphism explicitly using the `virtual` keyword unlike in other OOP languages where it is active by default

# Definitions
- Dynamic Ascending Transtyping: There is a required virtual method that is not in the child class but is inherited from the mother class (or another higher level of the inheritance hierarchy)

# Additional Resources
- [C++ Virtual Functions](https://www.geeksforgeeks.org/virtual-function-cpp/)

# Notes
## Virtual Methods
- Virtual methods create abstract classes that can be used to inherit from. In the example here, we have a pure virtual method which indicates that it will be implemented with a polymorphic overload in child class definitions
```c
class Base
{
public:
	virtual string toString() = 0;

};
```

## Example from CoPilot
```c
#include<iostream>
using namespace std;

// Base class
class Shape {
public:
   // pure virtual function providing interface framework.
   virtual int getArea() = 0;

   void setWidth(int w) {
      width = w;
   }

   void setHeight(int h) {
      height = h;
   }

protected:
   int width;
   int height;
};

// Derived classes
class Rectangle: public Shape {
public:
   int getArea() { 
      return (width * height); 
   }
};

class Triangle: public Shape {
public:
   int getArea() { 
      return (width * height)/2; 
   }
};

int main(void) {
   Rectangle Rect;
   Triangle  Tri;

   Rect.setWidth(5);
   Rect.setHeight(7);
   // Print the area of the object.
   cout << "Total Rectangle area: " << Rect.getArea() << endl;

   Tri.setWidth(5);
   Tri.setHeight(7);
   // Print the area of the object.
   cout << "Total Triangle area: " << Tri.getArea() << endl; 

   return 0;
}
```