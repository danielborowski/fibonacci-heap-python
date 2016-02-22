# Usage of Fibonacci heap
Test out the code live on [repl](https://repl.it/Bouq/13)

# Heap functions
- find_min() runs in O(1) time
- extract_min() runs in O(1) time
- insert(k) runs in O(1) time
- merge(h) runs in O(1) time
- decrease_key(x, k) runs in O(log n) time

More info on the amortized analysis and running times can be found [here](http://bit.ly/1ow1Clm).

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
f3.decrease_key(q, 4)

```
