#Lesson 2


##List comprehension

Quck example of list comprehension

```python
[s for r,s in cards]
```

This is the same as

```python
result = []
for r,s in cards:
    result.append(s)
```


##Generator expression

General structure of generator expression is `( term for-clouse optional )`

```python
>>> def sq(x): print 'sq called', x; return x * x
...
>>> g = (sq(x) for x in range(10) if x%2 == 0)
>>> g
<generator object <genexpr> at 0x1005e3aa0>
>>> next(g)
sq called 0
0
>>> next(g)
sq called 2
4
```

At the end of calculations generator will rases an error `StopIteration`:

```python
...
>>> next(g)
sq called 8
64
>>> next(g)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration
```

You rarely will be calling `next()` directly, rather most of the time we're doing it within a `for` loop 

```python
>>> for x2 in (sq(x) for x in range(10) if x%2 == 0): pass
... 
sq called 0
sq called 2
sq called 4
sq called 6
sq called 8
>>>
```

We can even convert results in the end

```python
>>> list((sq(x) for x in range(10) if x%2 == 0))
sq called 0
sq called 2
sq called 4
sq called 6
sq called 8
[0, 4, 16, 36, 64]
>>> 
```