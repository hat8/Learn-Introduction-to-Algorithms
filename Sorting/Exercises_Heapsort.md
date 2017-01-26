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
