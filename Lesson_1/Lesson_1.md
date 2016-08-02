#Lesson 1


##Outlining The Problem

A general process:

??? --`1`--> problem --`2`--> spec --`3`--> code
  
`1` understanding a problem  
`2` specify  
`3` design
 

>If you need a refresher on the rules of poker, check out this [video](http://www.udacity.com/view#Course/cs212/CourseRev/apr2012/Unit/71001/Nugget/56009), or the [wikipedia article](http://en.wikipedia.org/wiki/List_of_poker_hands) on the ranking of poker hands.


`hand` consist of 5 cards. Each card has a `rank` and a `suite`.  

The main functions in this game will take a list of `hands` and will return the best hand:  
`poker(hands) -> hand`


##Representing Hands

In this game `hands` will be represented as a list of tuples 
 
```python
[(11, 'S'), (11, 'D'), (2, 'S'), (2, 'C'), (7, 'H')]
```


##Poker Function

General idea of Poker Function

```python
def poker(hands):
    "Return the best hand: poker([hand,...] => hand)"
    return max
```

Some small example on how `max` function works

```python
>>>print max([3, 4, 5, 0]), max([3, 4, -5, 0], key=abs)
5 -5
```

[More info](https://docs.python.org/3/library/functions.html#max) on `max` built-in function.


##Testing

The simplest way to test a program is to define and then to call a function with some sample arguments.  

```python
def test():
	"Test cases for the functions in poker program."
	sf = "6C 7C 8C 9C TC".split()
	fk = "9D 9H 9S 9C 7D".split()
	fh = "TD TC TH 7C 7D".split()
	assert poker([sf, fk, fh]) == sf
	return "tests pass"

print test()
```

`assert` statemet asserts that the following thing must be True. If it's not true a program will stop and print an error message. And if it's true a code will run and in our case will print "tests pass".

One of the important things of testing is to test for `extreme values`: 0 players, 1 player, 100 players etc.

```python
def test():
    "Test cases for the functions in poker program"
    sf = "6C 7C 8C 9C TC".split() 
    fk = "9D 9H 9S 9C 7D".split() 
    fh = "TD TC TH 7C 7D".split()
    assert poker([sf, fk, fh]) == sf
    assert poker([fk, fh]) == fk
    assert poker([fh, fh]) == fh
    assert poker([fh]) == fh
    assert poker([fk] + 99 * [fh]) == fk
    return 'tests pass'
```

##Representing rank

In tihs program rank will be represented as a `tuple`.  

```python
(7, 9, 5) > (7, 3, 2)
```

