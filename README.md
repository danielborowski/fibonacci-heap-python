# Usage of Fibonacci heap
Test out the code live on [repl](https://repl.it/Bouq/13)

# Heap functions
- find_min() runs in O(1) time
- extract_min() runs in O(log n) time
- insert(k) runs in O(1) time
- merge(h) runs in O(1) time
- decrease_key(x, k) runs in O(1) time

More info on the amortized analysis and running times can be found [here](http://bit.ly/1ow1Clm).

# Example

```python
f = FibonacciHeap()

f.insert(10)
f.insert(2)
f.insert(15)
f.insert(6)

m = f.find_min()
print m.data # 2

q = f.extract_min()
print q.data # 2

q = f.extract_min()
print q.data # 6

f2 = FibonacciHeap()
f2.insert(100)
f2.insert(56)

f3 = f.merge(f2)
x = f3.root_list.right # pointer to random node
f3.decrease_key(x, 1)

# print the root list using the iterate class method
print [x.data for x in f3.iterate(f3.root_list)]

q = f3.extract_min()
print q.data # 1
```

# Results
Quote from the [original](http://www.cs.cmu.edu/~sleator/papers/pairing-heaps.pdf) paper:
> They are complicated when it comes to coding them. Also they are not as efficient in practice when compared with the theoretically less efficient forms of heaps, since in their simplest version they require storage and manipulation of four pointers per node, compared to the two or three pointers per node needed for other structures

> Although the total running time of a sequence of operations starting with an empty structure is bounded by the bounds given above, some (very few) operations in the sequence can take very long to complete (in particular delete and delete minimum have linear running time in the worst case). 

I decided to test out my implementation of the Fibonacci heap vs. the [heapq](https://docs.python.org/2/library/heapq.html) algorithm module in Python which implements a basic binary heap using array indexing for the nodes.
