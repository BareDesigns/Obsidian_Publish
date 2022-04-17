---
banner: "![[Algorithms.png]]"
banner_icon: 👾
---

## Floyd's Tortoise and Hare 🐇 🐢

Floyd's tortoise and hare algorithm runs through linked lists using 2 variables,  with var **hare** moving twice as many spaces as var **tortoise**. Once the two meet, we have then found a cycle.

```Python
hare = num[0]
tortoise = num[0]

while True:
	tortoise = num[tortoise]
	hare = num[num[hare]]

	if tortoise == hare:
		break

	ptr1 = num[0]
	ptr2 = tortoise

	while ptr1 != ptr2:
		ptr1 = num[ptr1]
		ptr2 = num[ptr2]
	return ptr1
```

## Manacher's Algorithm $(O(N^2))$
Used to find the longest palindromic substring in a query

To find, one way is to take each possible $(2*N+1)$ centers

* N = character positions
* N-1 Between 2 character positions
* 2 positions at the left and right ends

To understand this algorithm, consider the two strings  
"abababa" & "abaaba"

```python
```