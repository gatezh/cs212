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


##Suits of cards

Red       | Black  
----------| --------
♥ Hearts  | ♠ Spades  
♦ Diamonds| ♣ Clubs 


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

`assert` statement asserts that the following thing must be True. If it's not true a program will stop and print an error message. And if it's true a code will run and in our case will print "tests pass".

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

Using just an integer to rank a hand won't allow to brake a tie. Using a float number as a rank is possible solution, but a bit difficult.  
That's why in this program rank will be represented as a `tuple`. 

```python
(7, 9, 5) > (7, 3, 2)
```


##Wild West Poker

####`8` Straight Flush. Jack high

hand: `JC | 10C | 9C | 8C | 7C`

tuple: `(8, 11)` <== 11 for Jack


####`7` Four Aces and A Queen Kicker

hand: `AH | AS | AD | AC | QH`

tuple: `(7, 14, 12)` <== 14 for Ace, 12 for Queen

####`6` Full House. Eights over Kings

hand: `8S | 8H | 8D | KS | KC`

tuple: `(6, 8, 13)` <== 8 for 8, 13 for King

####`5` Flush. 10-8

hand: `10D | 8D | 7D | 5D | 3D`

tuple: `(5, [10, 8, 7, 5, 3])`

####`4` Straight. Jack high

hand: `JC | 10S | 9D | 8C | 7C`

tuple: `(4, 11)` <== 11 for Jack

####`3` Three Sevens

hand: `7H | 7D | 7C | 5C | 2C`

tuple: `(3, 7, [7, 7, 7, 5, 2])`

####`2` Two Pairs. Jack and Threes

hand: `7D | JC | 3S | 3H | KH`

tuple: `(2, 11, 3, [13, 11, 11, 3, 3])` <== 11 for Jack, 13 for King

####`1` Pair of Twos. Jack high

hand: `2H | 2S | JD | 6H | 3C`

tuple: `(1, 2, [11, 6, 3, 2, 2])` <== 11 for Jack

####`0` Got nothing

hand: `7C | 5C | 4C | 3C | 2D`

tuple: `(0, 7, 5, 4, 3, 2)`


##card_ranks function

`ranks` is generated list by returning index of each element (which is an integer) and making list out of that.  
There are some other ways to get the same result by using dictionary or `for` statemens, but this solution is much smaller and easier to understand.

```python
def card_ranks(cards):
    "Return a list of the ranks, sorted with higher first."
    ranks = ["--23456789TJQKA".index(r) for r,s in cards]
    ranks.sort(reverse=True)
    return ranks
```