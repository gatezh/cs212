#Lesson 2

##Zebra puzzle

The following version of the puzzle appeared in Life International in 1962:

1. There are five houses.
2. The Englishman lives in the red house.
3. The Spaniard owns the dog.
4. Coffee is drunk in the green house.
5. The Ukrainian drinks tea.
6. The green house is immediately to the right of the ivory house.
7. The Old Gold smoker owns snails.
8. Kools are smoked in the yellow house.
9. Milk is drunk in the middle house.
10. The Norwegian lives in the first house.
11. The man who smokes Chesterfields lives in the house next to the man with the fox.
12. Kools are smoked in the house next to the house where the horse is kept.
13. The Lucky Strike smoker drinks orange juice.
14. The Japanese smokes Parliaments.
15. The Norwegian lives next to the blue house.

    Now, who drinks water? Who owns the zebra?

In the interest of clarity, it must be added that each of the five houses is painted a different color, and their inhabitants are of different national extractions, own different pets, drink different beverages and smoke different brands of American cigarets [sic]. One other thing: in statement 6, right means your right.  

_— Life International, December 17, 1962_


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