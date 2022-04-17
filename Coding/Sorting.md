# Sorting Methods

*Tags: [[Python]]*

---

**Table of Contents:**

```toc
style: bullet
```

## Selection

*O($n^2$)*

Sorts original list into two parts, *sorted* and *unsorted*.  
Continuously moves the smallest element from the original(unsorted list) to the sorted list.
Traverses through the list, finds the minimum amount, and adds it to the last minimum location index

**EXAMPLE:**

* [3, 5, 4, 1] -> [1, 3, 5, 4]
* [1, 3, 5, 4] -> [1, 3, 4, 5]

```python
a = [3, 4, 6, 5]

for i in range(len(a)):
	minIndex = i
	for j in range(i+1, len(a)):
		if a[minIndex] > a[j]:
			minIndex = j

	a[i], a[minIndex] = a[minIndex], a[i]
```

## Bubble

*O($n^2$)*

Works by repeatedly swapping the adjacent elements if they aren't in the correct order.

**EXAMPLE:**

* [**3**, **4**, 1, 2] -> [**3**, **4**, 1, 2]
* [3, **4**, **1**, 2] -> [3, **1**, **4**, 2]
* [**3**, **1**, 4, 2] -> [**1**, **3**, 4, 2]
* [1, 3, **4**, **2**] -> [1, 3, **2**, **4**]
* [1, **3**, **2**, 4] -> [1, **2**, **3**, 4]


```python
list2 = [5,3,8,6,7,2]

def bubbleSort(list1):
	for i in range(len(list1)):
		for j in range(len(list1)):
			temp = list1[j]
			list1[j] = list1[j+1]
			list1[j+1] = temp
	return list1
```

## Insertion

*O($n^2$)*

Similar to sorting a hand of poker cards. Divides array into 2 parts, sorted and unsorted.
A value from the unsorted is taken and placed in the proper place in the sorted list.

**EXAMPLE:**
![](https://www.tutorialspoint.com/assets/questions/media/28755/29.jpg)
```python
list1 = [10, 5, 13, 8, 2] 

def insertion_sort(list1): 
	for i in range(1, len(list1)): 
	
	value = list1[i]
	j = i - 1 
	while j >= 0 and value < list1[j]: 
		list1[j + 1] = list1[j] 
		j -= 1 
		list1[j + 1] = value 
	
	return list1 
```

## Heap Sort

O(n * log(n))

Segments list into *unsorted* and *sorted*, converts unsorted segment to a  
**Heap** data structure

```Python
def heapify(nums, heap_size, root_index):
    # Assume the index of the largest element is the root index
    largest = root_index
    left_child = (2*root_index) + 1
    right_child = (2*root_index) + 2

    # If the left child of the root is a valid index, and the element is greater
    # than the current largest element, then update the largest element
    if left_child < heap_size and nums[left_child] > nums[largest]:
        largest = left_child

    # Do the same for the right child of the root
    if right_child < heap_size and nums[right_child] > nums[largest]:
        largest = right_child

    # If the largest element is no longer the root element, swap them
    if largest != root_index:
        nums[root_index], nums[largest] = nums[largest], nums[root_index]

        heapify(nums, heap_size, largest)


def heap_sort(nums):
    n = len(nums)

    for i in range(n, -1, -1):
        heapify(nums, n, i)

    for i in range(n-1, 0, -1):
        nums[i], nums[0] = nums[0], nums[i]
        heapify(nums, i, 0)
```

## Merge Sort

*O(n$log(n)$)*

Splits list in half and keeps splitting until only singular elements remain. Adjacent  
elements become sorted pairs, then merged and sorted with other pairs until complete

```python
def merge(left_list, right_list):
    sorted_list = []
    left_list_index = right_list_index = 0

    # We use the list lengths often, so its handy to make variables
    left_list_length, right_list_length = len(left_list), len(right_list)

    for _ in range(left_list_length + right_list_length):
        if left_list_index < left_list_length and right_list_index < right_list_length:
            # We check which value from the start of each list is smaller
            # If the item at the beginning of the left list is smaller, add it
            # to the sorted list
            if left_list[left_list_index] <= right_list[right_list_index]:
                sorted_list.append(left_list[left_list_index])
                left_list_index += 1
            # If the item at the beginning of the right list is smaller, add it
            # to the sorted list
            else:
                sorted_list.append(right_list[right_list_index])
                right_list_index += 1

        # If we've reached the end of the of the left list, add the elements
        # from the right list
        elif left_list_index == left_list_length:
            sorted_list.append(right_list[right_list_index])
            right_list_index += 1
        # If we've reached the end of the of the right list, add the elements
        # from the left list
        elif right_list_index == right_list_length:
            sorted_list.append(left_list[left_list_index])
            left_list_index += 1

    return sorted_list


def merge_sort(nums):
    # If the list is a single element, return it
    if len(nums) <= 1:
        return nums

    # Use floor division to get midpoint, indices must be integers
    mid = len(nums) // 2

    # Sort and merge each half
    left_list = merge_sort(nums[:mid])
    right_list = merge_sort(nums[mid:])

    # Merge the sorted lists into a new one
    return merge(left_list, right_list)
```


## Quick Sort

*(O($n^2$))*

Partitions the list, picks one value that will be in its sorted place (also called a pivot)  
All elements smaller are moved to the left, everything larger moves to the right

```python
def partition(nums, low, high):
    # We select the middle element to be the pivot. Some implementations select
    # the first element or the last element. Sometimes the median value becomes
    # the pivot, or a random one. There are many more strategies that can be
    # chosen or created.
    pivot = nums[(low + high) // 2]
    i = low - 1
    j = high + 1
    while True:
        i += 1
        while nums[i] < pivot:
            i += 1

        j -= 1
        while nums[j] > pivot:
            j -= 1

        if i >= j:
            return j

        # If an element at i (on the left of the pivot) is larger than the
        # element at j (on right right of the pivot), then swap them
        nums[i], nums[j] = nums[j], nums[i]


def quick_sort(nums):
    # Create a helper function that will be called recursively
    def _quick_sort(items, low, high):
        if low < high:
            # This is the index after the pivot, where our lists are split
            split_index = partition(items, low, high)
            _quick_sort(items, low, split_index)
            _quick_sort(items, split_index + 1, high)

    _quick_sort(nums, 0, len(nums) - 1)
```