|           Course Name           |      Topic      | Professor |      Date      |     Tags     |
| :-----------------------------: | :-------------: | :-------: | :------------: | :----------: |
| **Software Engineering Part 1** | Data Structures | Sebastien | 21-22 May 2024 | #Programming |

[Class Video Link](URL)

# Summary
*In computer science, there are two main data structures, arrays, which are <mark style="background: #FFB86CA6;">contiguous block of memory in RAM,</mark> and linked lists, which are discontiguous and connected via [[Pointers & References|pointers]]. From an organization standpoint, data structure definitions should be defined in the header file of a compiled program. Arrays can either be [[Pointers & References|stack-based]] or a vector allocated in heap memory, but a linked list can ONLY be in [[Pointers & References|heap memory]].* 

# Key Takeaways
1. The memory in any array (stack or heap based) must be contiguous
2. The main criterion between arrays and linked lists is the resizing component
3. Linked lists are separated *minimally* into two parts: the data and the link between the elements
4. Each element in a linked list is dynamically allocated
	a.  Time complexity for a new element at the head of the list is constant O(1)
5. It is impossible to directly index a list because they are discontiguous in memory
6. Recursive functions are handled by a stack array that keeps track of function calls. That is why we can get "greater than recursive stack" errors

# Definitions
- Vector: A dynamically sized array 
	- NumPy arrays in Python are vectors
	- Everything in R is a vector
- Collection: A data structure that contains multiple values of the same data type
- Single vs Double Entry: In a linked list, this determines whether we can enter the list from only one (the head) or two (head and tail) of the list
- Forward-Only vs Bidirectional: In a linked list, this specifies if we are able to traverse the list in only one direction or if we can go in multiple directions

# Additional Resources
- [List vs Array](https://www.geeksforgeeks.org/linked-list-vs-array/)
- [Vectors in C & C++](https://www.mygreatlearning.com/blog/vectors-in-c/)

# Notes
## Arrays and Linked Lists
- Arrays
	- Contiguous in memory
	- Direct access to each element with an index
	- Nontrivial resizing (see pushback function below)
	- Only collection data structure that can exist either in stack or heap
	```c
	BOOL push_back(OurVector* pVector,
	int aNumber)
{
	BOOL success = FALSE;

	// Advice from Sebastien: Start writing code with the "easy cases" and then adjust/refactor from there to make it more elegant

	// Easy case: we do not need to expand the array

	// Add to any test with a pointer. The input param CANNOT be null
	if (pVector != NULL) {
		if (pVector->pBaseArray != NULL && pVector->nMemory_Size > 0) // Condense this into a function to check if the vector is indeed allocated, returning a BOOL
		{
			// Simple Case Check: The array does not need to be expanded. Less elements than remaining memory allocated
			if (pVector->nNumber_Elements < pVector->nMemory_Size)
			{
				// We do have space, no need to increase the array size
				// The next available index is at the current value of the number of elements
				int atIndex = pVector->nNumber_Elements; // Local var for clarity, will likely be removed from the stack by the compiler optimizer
				pVector->pBaseArray[atIndex] = aNumber;
				pVector->nNumber_Elements++;
				success = TRUE;
			}
			else
			{
				// Expansion of the Array

				// Need to create a new array of the expanded size w/o touching the current array
				// All kinds of HEURISTICS (known principles) are imaginable to determine by how much we should increase the size
					// Examples:
						// Double the size at every expansion (okay at the beginning but it'll grow fast)
						// Constant size value
						// Complex set of heuristics: Double until 1000 in size and then expand by steps of steps of constant or by half/third of size
				int* pNewArray = (int*)malloc(sizeof(int) * pVector->nMemory_Size + EXPANSION_SIZE);
				if (pNewArray != NULL)
				{
					// At this precise point, both arrays are allocated in memory
					// We need to copy the data from old to new
					for (i = 0, i < pVector->nNumber_Elements, i++)
						pNewArray[i] = pVector->pBaseArray[i];

					// Deallocate the old array
					free(pVector->pBaseArray);
					
					// Reset the pointer
					pVector->pBaseArray = pNewArray;

					// Update the metadata
					pVector->nMemory_Size += EXPANSION_SIZE;

					// TODO - Refactor. We copied the code from above which is not good
					// We do have space, no need to increase the array size
					// The next available index is at the current value of the number of elements
					int atIndex = pVector->nNumber_Elements; // Local var for clarity, will likely be removed from the stack by the compiler optimizer
					pVector->pBaseArray[atIndex] = aNumber;
					pVector->nNumber_Elements++;
					success = TRUE;
				}

			}
		}
	}

	// Should always engineer code to have return  
	return success;
};
```
- Linked Lists
	- Discontiguous in memory
	- Therefore, indirect access
	- Trivial resizing since each element is dynamically allocated
	- Can ONLY exist in heap
	- Contains minimally two parts: data and the chaining
	- Adding a new element
		- Set a chain of NULL and resetting the last element in the chain
	- All python lists are linked lists that are double-entry and bidirectional

## Vectors
- Vectors are dynamically sized arrays
	- These MUST exist in heap memory since stack memory size must be deterministic
- In C, arrays must be stack-based, so we need to make a call to the OS memory manager to request additional space for the dynamic sizing
- Useful because manually managing array size is annoying and error-prone. A vector allows us to have a data structure with a base pointer, memory size, and number of elements (metadata) to better handle array management
- We could *attempt* to use the `realloc` function, but it is highly unlikely that this will succeed since it requires that the next *n* spaces next to the existing array in memory are available
	- This is because many programs share the RAM space and the <mark style="background: #FFB86CA6;">OS address space layout randomization</mark>