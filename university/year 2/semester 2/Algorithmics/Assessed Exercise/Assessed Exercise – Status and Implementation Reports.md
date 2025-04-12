#algo

Name: **Liam McManus**
Matriculation Number: **2895711**

March 14, 2025

***AI was not used in creating this.***
# Status Report

I believe the code is working as intended both programs match each others test cases and logically both algorithms seem sound to me.
# Implementation Report

I tried my best throughout this exercise to stick to OOP principles, I've worked quite a bit with Object Oriented but that's more through frontend javascript frameworks rather than pure Java and looking back through I think it turned out really quite clean. Some of the overriding and extending felt a bit dodgy at times, but in the end, everything works as intended.
## Structure

For the structure both tasks are encapsulated in their own Specific Classes, the `WeightedWordLadderGraph` class and the `WordLadderGraph`. These both inherit from the same Graph class from the lab we done in class. Each class is instantiated and operated on through the `main` method, which remains similar across both tasks.

When it comes to handling errors I threw on a few different I/O issues, such as  the word not being in the dataset or the word not being of the correct length. 
## Data Structures

When it comes to data structures I read in the data as an `ArrayList` which might seem like a weird choice at first rather than using a `Set` but through using this we are able to use the index property to efficiently and easily create and navigate the graph.

Then I use a graph for both exercises. For both I use a graph with adjacent nodes which differ in only one character from the parent which allows me to efficiently find word ladders.
## Readability

For readability I added a few comments, mostly just explaining sections that aren't 100% clear why they are implemented a certain way, but I opted to try to keep it to a minimum. In my experience, too many comments can often clutter and obscure otherwise simple logic.

## Challenges

The biggest hurdle was getting comfortable with Java. I understood the theory behind the data structures and algorithms, but translating that into Java was tricky. One surprisingly frustrating issue was trying to return `null` from the `dijkstras` method, only to learn a few hours later you can't do that with a primitive type.

## `wordladder`

For the first half I use a **Breadth First Search** through the graph, which I then early return from when we find the target, then backtrack to the root creating a word ladder in the process. I think it's a really clean and simple way to handle it. 

I initially implemented it as a **Depth First Search** which ended up never actually returning the shortest path, it would just return the first deep path to it which could be **MASSIVE**, I remember doing something along the lines of Bread to Broad and it returning a word ladder of 20 odd steps.

Here's a screenshot from designing this algorithm:

![[Screenshot 2025-04-06 at 21.23.35.png]]

## `dijkstras`

For the second task I used the same graph from before but added in the weightings, then I looped through every child adding the parent weight to the children weight in a key value, then once the target is found I returned the new weight for that node. 

I find this quite a simple and efficient way to go about it.

Once again a screenshot from designing this (please ignore my counting here - it's not my strong suit):

![[Screenshot 2025-04-06 at 21.36.31.png]]

# Empirical Results

Both programs run efficiently and seem to match all test cases.
## `wordladder`

```
print paint
forty fifty
cheat solve
worry happy
smile frown
small large
black white
greed money
```

```
from: print
to: paint
print -> paint

Elapsed time: 54 milliseconds
```

```
from: forty
to: fifty
forty -> forth -> firth -> fifth -> fifty

Elapsed time: 58 milliseconds
```

```
from: cheat
to: solve
cheat -> chert -> chart -> charm -> chasm -> chase -> cease -> lease -> leave -> heave -> helve -> halve -> salve -> solve

Elapsed time: 54 milliseconds
```

```
from: worry
to: happy
no word ladder could be found

Elapsed time: 54 milliseconds
```

```
from: smile
to: frown
smile -> stile -> stale -> stalk -> stack -> shack -> shock -> chock -> crock -> crook -> croon -> crown -> frown

Elapsed time: 55 milliseconds
```

```
from: small
to: large
small -> shall -> shale -> share -> shard -> chard -> charm -> chasm -> chase -> cease -> tease -> terse -> verse -> verge -> merge -> marge -> large

Elapsed time: 55 milliseconds
```

```
from: black
to: white
black -> slack -> shack -> shark -> share -> shale -> whale -> while -> white

Elapsed time: 54 milliseconds
```

```
from: greed
to: money
no word ladder could be found

Elapsed time: 55 milliseconds
```

## `dijkstras`

```
blare blase
blond blood
allow alloy
cheat solve
worry happy
print paint
small large
black white
greed money
```

```
from: blare
to: blare
shortest path is of length: 0

Elapsed time: 58 milliseconds
```

```
from: blond
to: blood
shortest path is of length: 1

Elapsed time: 60 milliseconds
```

```
from: allow
to: alloy
shortest path is of length: 2

Elapsed time: 60 milliseconds
```

```
from: worry
to: happy
no path found

Elapsed time: 59 milliseconds
```

```
from: print
to: paint
shortest path is of length: 17

Elapsed time: 60 milliseconds
```

```
from: small
to: large
shortest path is of length: 118

Elapsed time: 63 milliseconds
```

```
from: black
to: white
shortest path is of length: 68

Elapsed time: 60 milliseconds
```

```
from: greed
to: money
no path found

Elapsed time: 58 milliseconds
```