|          Course Name          |    Topic     | Professor |    Date     |     Tags     |
| :---------------------------: | :----------: | :-------: | :---------: | :----------: |
| **Software Engineering Pt 1** | Aggregations | Sebastien | 23 May 2024 | #Programming |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/gordon_moore_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fgordon%5Fmoore%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FS24%2D%20DS%20%26%20Common%20LINK%20DS%5FDA%5FDE%2D20240523%5F094936%2DMeeting%20Recording%201%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E01ab46cc%2Df7c2%2D4f40%2Daf63%2De413d6f10249)

# Summary
*Aggregations are objects that specify two or more other [[Object-Oriented Design|objects]]. There are many things to consider with these to ensure that they are managed well.*

# Key Takeaways
1. We should always declare the object attributes as references to about memory duplication
2. The const modifier is used to ensure that the attributes of the object inside the aggregation are not modified by the aggregation
3. A collection should always be the top most level of an [[Inheritance|inheritance]] hierarchy and should always be filled using pointers since each array element only has the size of the mother class

# Definitions
- Aggregation: Any object that contains two or more other objects as attributes
	- Example: StraightLine2D which has two Point2D objects inside it

# Additional Resources
- [Aggregation](https://www.javatpoint.com/cpp-aggregation)

# Notes
## Aggregation
- Aggregations are objects that are composed of two or more other objects as elements
- To avoid memory duplication, we should always use a pointer to the actual object
```c
// :public Base means that this inherits from Base. Despite saying public, everything is in fact loaded
class StraightLine2D :public Base //Note that this class is an AGGREGATION as it is composed to two OBJECTS, instances of other classes
{
// Initially, this was private, but we will need (or might need) methods of children classes. Notably, LineSegment2D to access these attributes
protected:
	// Declare by address since it will let us pass this as a fxn param and also code duplicate values
	Point2D* point1;
	Point2D* point2;

	double m_gradient;
	double m_intercept;

	bool m_isPointAllocatedInClass;
	bool m_isGradientInfinite;

private:
	// This is for the xtors to use or if we'd ever need a public method to change one or more of the points in the line
	void calculateGradientAndIntercept();

public:
	StraightLine2D() {}; // Default constructor. Necessary for inheritance
	// const modifier means that the reference provided is non-modifiable. In this case, the data within pointA and pointB cannot be modified
	StraightLine2D(Point2D& const pointA, Point2D& const pointB);
	StraightLine2D(Point2D& const aPoint); // Set the origin and a single point
	string toString();

	// == is a binary operator - data types of lest and right operands are both StraightLine2D. We are comparing 2 straight lines
	// The implicit "this" pointer is the first input parameter such as sl1 == sl2 is expanded to sl1.operator==(sl2) which eventually becomes
		// sl1.operator(&sl1, sl2) which is the implicit pass of the address of sl1
	bool operator==(StraightLine2D& const aSL);

	// Observe the syntax here. We are passing both the ostream and our object as input here
	friend ostream& operator<<(ostream& const out, StraightLine2D& const aSL);

	// The class DESTRUCTOR, only one version (w/ no input parameters) is able to be overloaded
	// Desctructor MUST be overloaded, if and only if, any class method proceeds to dynamically allocate objects
	~StraightLine2D();
};
```
## Lifecycle of Objects
- Avoid unnecessary duplication especially when dealing with aggregation and collection classes
- With respect to the previous point, favor pass by address (or reference if there are no specific [[Pointers & References|pointers]] in the OOP language)
- Whoever (as in a class) allocates the memory for the object MUST also deallocate the memory