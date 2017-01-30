### 6.2-2

Starting with the procedure MAX-HEAPIFY, write pseudocode for the procedure
MIN-HEAPIFY.A which performs the corresponding manipulation on a minheap.

How does the running time of MIN-HEAPIFY compare to that of MAXHEAPIFY?

```
MIN_HEAPIFY(A,i)
	r = RIGHT(A[i])
	l = LEFT(A[i])
	if l <= A.heapsize and A[l] < A[i]
		min = l
	else min = i
	if r <= A.heapsize and A[r] < A[min]
		min = r
	if min != i
		exchange A[i] with A[min]
		MIN_HEAPIFY(A, min)
```

### 6.5-3

Write pseudocode for the procedures HEAP-MINIMUM, HEAP-EXTRACT-MIN,
HEAP-DECREASE-KEY, and MIN-HEAP-INSERT that implement a min-priority
queue with a min-heap.

```
HEAP-MINIMUM(A)
	return A[1]

HEAP-EXTRACT-MIN(A)
	if A.heap-size < 1
		error "heap underflow"
	min = A[1]
	A[1] = A[A.heap-size]
	MIN-HEAPIFY(A, 1)
	return min

HEAP-DECREASE-KEY(A, i, key)
	if key > A[i]
		error "the new value is greater than A[i], it should be smaller"
	A[i] = key
	while i > 1 and A[Parent(i)] > A[i]
		exchange A[Parent(i)] and A[i]
		i = Parent(i)

MIN-HEAP-INSERT(A, key)
	A.heap-size = A.heap-size + 1
	A[A.heap-size] = +inf
	HEAP-DECREASE-KEY(A, A.heap-size, key)
```

### 6.5-6
Each exchange operation on line 5 of HEAP-INCREASE-KEY typically requires
three assignments. Show how to use the idea of the inner loop of INSERTIONSORT
to reduce the three assignments down to just one assignment.

```
HEAP-INCREASE-KEY(A, i, key):
    if key < A[i]
        error "new key is smaller than current key"
    A[i] = key
    while i > 1 and A[PARENT(i)] < key
        A[i] = A[PARENT(i)]
        i = PARENT(i)
    A[i] = key
```

### 6.5-8
The operation HEAP-DELETE(A, i) deletes the item in node i from heap A. Give
an implementation of HEAP-DELETE that runs in O(lg n) time for an n-element
max-heap.

```
HEAP-DELETE(A, i):
	if A[i] < A[A.heap-size]:
		HEAP-INCREASE-KEY(A, i, A[heap.size])
		A.heap-size -= 1
	else:
		A[i] = A[A.heap-size]
		A.heap-size -= 1
		MAX-HEAPIFY(A, i)

```

### 6.5-9
Give an O(n lg(k))-time algorithm to merge k sorted lists into one sorted list,
where n is the total number of elements in all the input lists. (Hint: Use a min-heap
for k-way merging.)

Solution [here](http://www.bowdoin.edu/~ltoma/teaching/cs231/fall09/Homeworks/old/rest/H5-sol.pdf):

> The straightforward solution is to pick the smallest of the top elements in each list, repeatedly. This takes k − 1 comparisons per element, in total O(kn).
> As the hint suggests, the idea for the “improved” solution is to keep the smallest element from each list in a heap; each element is augmented with the index of the lists where it comes from. We can perform a DeleteMin on the heap to find and delete the smallest element and insert the next element from the corresponding list.
> Analysis: It takes O(k) to build the heap; for every element, it takes O(lg k) to DeleteMin and O(lg k) to insert the next one from the same list. In total it takes O(k + n lg k) = O(n lg k).
