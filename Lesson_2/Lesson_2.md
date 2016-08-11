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


##Measure time of running

To figure out how much time your app is running we can use standard `time` module which has a `clock` function

```python
import time

def timedcall(fn, *args):
    """Call function and return elapsed time."""
    t0 = time.clock()
    result = fn(*args)
    t1 = time.clock()
    return t1 - t0, result
```

The problem with this solution is that it gives us timing for just one run. To be more accurate we need to have an avarage of that number. So lets make a function that measures time for **n** runs of a function.

```python
import time

def timedcall(fn, *args):
    "Call function with args; return the time in seconds and result."
    t0 = time.clock()
    result = fn(*args)
    t1 = time.clock()
    return t1-t0, result

def average(numbers):
    "Return the average (arithmetic mean) of a sequence of numbers."
    return sum(numbers) / float(len(numbers)) 

def timedcalls(n, fn, *args):
    """Call fn(*args) repeatedly: n times if n is an int, or up to
    n seconds if n is a float; return the min, avg, and max time"""
    if isinstance(n, int):
        times = [timedcall(fn, *args)[0] for i in range(n)]
    else:
        times = []
        while sum(times) < n:
            times.append(timedcall(fn, *args)[0])
    return min(times), average(times), max(times)
```


##Translation Tables

In the code below we have a regular expression search that prevents situation when number starts with zero (0).

>It is important because number `012` in Python means `10`.  
>In C-based languages numbers starting with 0 are `octal` numbers with base of 8.

```python
import string, re

def valid(f):
    "Formula f is valid if it has no numbers with leading zero and evals true."
    try:
        # re.search - regular expression search
        # b stands for 'boundary'
        # looking for 0 followed by any number [0-9] in f
        return not re.search(r'\b0[0-9]', f) and eval(f) is True
    except ZeroDivisionError: # ArithmeticError is more powerful in this case
        return False
```


##Solving formula puzzle

In this example we make a function that replaces letters with numbers so the formula expression stay valid.  
Check Lines 14-17 and 26 for examples of `regular expression` use.

```python
from __future__ import division
import string, re, itertools


def solve(formula):
    """Given a formula like 'ODD + ODD == EVEN', fill in digits to solve it.
    Input formula is a string; output is a digit-filled-in string or None."""
    for f in fill_in(formula):
        if valid(f):
            return f


def fill_in(formula):
    "Generate all possible fillings-in of letters in formula with digits."
    letters = "".join([i for i in formula if i.isalpha()])  # should be a str
    # or can be implemented using regular expressions
    # letters = "".join(set(re.findall("[A-Z", formula)))
    for digits in itertools.permutations('1234567890', len(letters)):
        table = string.maketrans(letters, ''.join(digits))
        yield formula.translate(table)


def valid(f):
    """Formula f is valid if and only if it has no
    numbers with leading zero, and evals true."""
    try:
        return not re.search(r'\b0[0-9]', f) and eval(f) is True
    except ArithmeticError:
        return False
```


##Future Imports

In Python 2.X a result of division of integer numbers is **always** an integer.  
In Python 3.X a result of division may be float as well.  
To get Python 3.X kind of behaviour in Python 2.X we can import from `__future__` module.

```python
from __future__ import division
```


##Tracking Time

To analyse how much time it takes for your application to run it's different components we can use `cProfile` module.  

```python
$python -m cProfile crypt.py
```

So we can concentrate out efforts to change parts where most of the time is.  

And it's not just a good idea – it's a low.

**Law of Diminishing Returns**  
