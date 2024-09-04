|          Course Name          | Topic | Professor |    Date    |         Tags         |
| :---------------------------: | :---: | :-------: | :--------: | :------------------: |
| **Software Engineering Pt 2** |  OOP  |   Hanna   | 30/07/2024 | #Programming #Python |

[Class Video Link](https://dstisas-my.sharepoint.com/personal/johnny_najjar_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fjohnny%5Fnajjar%5Fdsti%5Finstitute%2FDocuments%2FRecordings%281%29%2FS24%2D%20DS%20%26%20Common%20LINK%20DS%5FDA%5FDE%2D20240730%5F094914%2DMeeting%20Recording%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E4d2826e9%2D9d87%2D4e42%2D8b8a%2D47aa880a85de)

# Summary
*A class in Python is the recipe that defines an [[Object-Oriented Design|object]] (instance of a class). Classes consist of a header and body. In Python, all classes are of equal status, and everything, including base data types, is an object that inherits from a base superclass called `type`.*

# Key Takeaways
1. All classes in Python are of <mark style="background: #FFB86CA6;">equal status</mark> and **everything** in Python is an object

# Definitions
- Class: A Recipe/Blueprint/Formal Definition for an object
- Object/Instance: A representation or manifestation of a class 

# Additional Resources
- [Classes (Python Docs)](https://docs.python.org/3/tutorial/classes.html)

# Notes
## Classes in Python
- In Python, everything is an object that derives from a superclass
![[Pasted image 20240808134533.png]]
- Classes are generally made up of two components, a header (the name and declaration) and a body (the attributes and methods)
```python
class Cat: # Header
	def __init__(self): # Body
		pass
```