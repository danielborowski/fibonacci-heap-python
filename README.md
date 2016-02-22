# Usage of Fibonacci heap
Test out the code live on [repl](https://repl.it/Bouq/13)

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

```
