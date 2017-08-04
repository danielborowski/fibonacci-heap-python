# Fibonacci heaps

> Using Fibonacci heaps for priority queues improves the asymptotic running time of important algorithms, such as Dijkstra's algorithm for computing the shortest path between two nodes in a graph, compared to the same algorithm using other slower priority queue data structures.

<img src="http://i.imgur.com/069fuCV.png" width="600">

# Heap functions
- `find_min()` runs in O(1) time
- `extract_min()` runs in O(log n) time
- `insert(k)` runs in O(1) time
- `merge(h)` runs in O(1) time
- `decrease_key(x, k)` runs in O(1) time

More info on the amortized analysis and running times can be found [here](http://bit.ly/1ow1Clm) or on [Wikipedia](https://en.wikipedia.org/wiki/Fibonacci_heap#Summary_of_running_times).

# Example

Test out the code live on [repl.it](https://repl.it/Bouq/13)

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
print [x.data for x in f3.iterate(f3.root_list)] # [10, 1, 56]

q = f3.extract_min()
print q.data # 1
```

# Results
Quote from the [original](http://www.cs.cmu.edu/~sleator/papers/pairing-heaps.pdf) paper:
> They are complicated when it comes to coding them. Also they are not as efficient in practice when compared with the theoretically less efficient forms of heaps, since in their simplest version they require storage and manipulation of four pointers per node, compared to the two or three pointers per node needed for other structures

I decided to test out my implementation of the Fibonacci heap vs. the [heapq](https://docs.python.org/2/library/heapq.html) algorithm module in Python which implements a basic binary heap using array indexing for the nodes. 

The Fibonacci heap did in fact run more slowly when trying to extract all the minimum nodes. You can see the comparison run times on [repl.it](https://repl.it/BouR/13) for yourself. 

Note: I performed some basic inserts and extracted the minimum several times to see which data structure was more efficient, which isn't the best test for analyzing the running time. For a more thorough analysis on applying the Fibonacci heap to the shortest path algorithm, check out this [answer on Stack Overflow](https://stackoverflow.com/questions/504823/has-anyone-actually-implemented-a-fibonacci-heap-efficiently/508221#508221).

## Running times
Initilaze both heaps with some data:
````python
from heapq import *
from random import randint

f = FibonacciHeap()
h = []
n = 100
for i in xrange(0, n):
    r = randint(1, 1000)
    f.insert(r)
    heappush(h, r)
````

The code to extract the min from both heaps and print the running time:
````python
import time

# test fib heap running time 
start_time = time.time()
while f.total_nodes > 0:
    m = f.extract_min()
print "%s seconds run time for fib heap" % (time.time() - start_time)

# test heapq running time 
start_time = time.time()
while h:
    m = heappop(h)
print "%s seconds run time for heapq" % (time.time() - start_time)
````

### n = 100
````
0.0109820365906 seconds run time for fib heap
0.000254154205322 seconds run time for heapq
````

### n = 500
````
0.0828540325165 seconds run time for fib heap
0.00195384025574 seconds run time for heapq
````

### n = 1000
````
0.19855594635 seconds run time for fib heap
0.00374603271484 seconds run time for heapq
````

# Note
[Michael Fredman](https://en.wikipedia.org/wiki/Michael_Fredman), one of the creators of the Fibonacci heap, was one of my professors in college. His class was very difficult.
