[solved-with-iteration]

## Unsolved
#### 4. Median of Two Sorted Arrays
Key points:
- Search in one array for left partition of size x(other has partition (all elements) // 2 - x elements) (We can know how many elements other one has as we know how big the left partition needs to be. "left-partition" - elements to the left of median!)
- Main condition, in arrays A, B, for maximum value in left partition in A is smaller than minimum in right partition in B and vice versa.

#### [287. Find the Duplicate Number](https://leetcode.com/problems/find-the-duplicate-number/)
Key points:
- Treat a list as linked list network (indexes are current nodes and values are next nodes)
- Floyd's algorithm to find start of cycle:
	- Find first intersection of *fast* and *slow* pointers.
	- Put *slow2* at the start of the array again.
		- once the pointers intersect, you found the start of the cycle
	-  Why does it work?
		- The fast does at least a loop (hence 2C) until it meets slow (but no more) ![[Pasted image 20240930201039.png]]