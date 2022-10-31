---
categories: [advanced, oop, ml]
---

# Iterables 

See [here](https://www.w3schools.com/python/python_iterators.asp). 


To create an object/class as an iterator you have to implement the methods `__iter__()` and `__next__()` to your object. You should probably also add a `__init__()` function too to keep track of state. 

The __iter__() method acts similar, you can do operations (initializing etc.), but must always return the iterator object itself.

The __next__() method also allows you to do operations, and must return the next item in the sequence. 

## Example 

```python
class MyNumbers:
  def __init__(self):
  	self.a = 2
    
  def __iter__(self):
    return self

  def __next__(self):
    x = self.a
    self.a += 1
    return x

myclass = MyNumbers()
myiter = iter(myclass)


for x in myclass:
	print(x)
```
