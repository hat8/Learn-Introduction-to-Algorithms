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
