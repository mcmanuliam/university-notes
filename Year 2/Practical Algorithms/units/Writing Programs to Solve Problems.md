Or in other words, creating an "Algorithm" 

#### Three Main Stages
- Data input
- Data Processing
- Data Output

## How Do We Do the "Data Processing" Bit
Learning syntax and semantics of python (or other languages) is important but…

- The skill we want to learn is: how do we think computationally (emphasize with a computer, so to speak), so that then we can write algorithms that solve a given problem.
- Institutions, guesstimates, gut-feelings, are not going to work on their own (though will likely inform the process)
- So, what does work then?
	- Less of Picard, more of Data??

### Thinking like a Computer?
The key skills we will need to start more "computationally", so that we can write programmatic solutions that computers can solve:
- Algorithmics Thinking, functional thinking, one step at a time (up next)
- Analysis (coming up soon)
- Decomposition, breaking down problems into bitsize chunks (for more complex problems)

We also need to develop general thinking skills, which will reduce code duplication especially in algorithms:
- Abstraction
- Generalization

#### Algorithmics Thinking
'Steps' in an Algorithm

- What is the 'size' of these steps?
	- Think in human terms first:
		- Baking a cake:
			- To a baker:
				- Step 1: Bake a 2lb cake
				- Step 2: Here's your money
			- To me:
				- Step 1: Get a cup
				- Step 2: Open the tap
				- ….

Steps are dependent on the audience we need to break it down to understandable chunks for a machine, get it as simple as assembly level.

#### Universal Building Blocks
Three operations used to construct an algorithm:
- Sequential Operations, one step after another
- Conditional Operations - if something do this step, else do another
- Iterative Operations, looping over steps

#### Sequential Operations
- Input
- Compute (run calculations on input)
- Output

#### Conditional Operations
- 'question asking' operations.

```python
var = 'help'

if var == 'help':
	print('helping')
else:
	print('not helping')
```

#### Iterative Operations
- looping over steps
- Also includes recursion
- Two loops
	- Pre test - for loops
	- Post test - while loops

```python
var = 1

while var < 6:
	print(str(var))
	var += 1
```

#### Problem Set: Algorithmic Thinking
[link](https://moodle.gla.ac.uk/mod/book/view.php?id=4586539&chapterid=162827)

**1a.**
- Input - Name
- Data Processing (Binary Search)
- Output - Location

**1b.**
1. Start in the middle.
2. If the value at the midpoint is less than the name, the list is divided in half, the lower half of the list is ignored and the search keeps to the upper half of the list.
3. Same goes in the other direction
4. The search moves to the midpoint of the remaining items. Steps 2 through 4 continue until a match is made or there are no more items to be found.

**2a.**
- Just loop through without any fancy technique

**3a.** 
- We have another perspective compared to a computer, we can see all data Infront of us, best way would be something similar to a bubble search except you compare with entire array and move directly to it's index.