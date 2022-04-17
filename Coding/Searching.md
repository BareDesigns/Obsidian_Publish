---
banner_icon: 👓
banner: "![[slide1.jpg]]"
---

# Binary Search

* *O(Log n)*

Works on a **sorted list** by starting in the middle, and the moving left or right until the index/item is found.

<br>
<br>

![[Binary Search.mp4]]

```python
def binary_search(nums, search_num):
	lower = 1
	upper = len(nums) - 1

	while lower <= upper:
		middle = (lower + upper) // 2
		if search_num == nums[middle]:
			return middle

		else:
			if search_num > nums[middle]:
				lower = middle + 1
			else:
				upper = middle - 1

	return False
```

# Linear Search

* *O(n)*

Also can be called **brute force** searching, a linear search simply runs through each element in an array until the item/index is found.

If the array is sorted, Binary Search would be the more efficient algorithm.

```python
a = [1,2,3,4,5,6]
find = 6

def linear_search(nums, target):
	for i in range(len(nums)):
		if nums[i] == find:
			return i
	
	return False
```