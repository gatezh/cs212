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
```
[(11, 'S'), (11, 'D'), (2, 'S'), (2, 'C'), (7, 'H')]
```

