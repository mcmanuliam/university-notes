- [x] ⏫ 📅 2024-12-12 Assessed Exercise 2 ✅ 2025-01-02

# Question 1 (40 points)
You want to design an algorithm that solves the following problem: as input you are given a string that may contain only the parenthesis characters 

```
'(' , ')' , '{' , '}' , '[' or ']
```

and you are asked to determine whether the input expression is "valid", i.e., if the parentheses are properly balanced. For example, expression '[{()}]()' is valid, but expressions '[{()]()' , '[{{()})]' and ')(' are not valid.


(a) Discuss how you can use a stack data structure to solve your problem. 

I'd say a stack is probably the easiest way to think about it, due to the first in last out properties we can just loop through all characters in an array 

- If it's one of the closing parenthesis, if so then we compare it against the top element in the stack and if they are a pair you can pop it from the stack.

- If it's not a closing parenthesis add it to the stack.

Once we are done you can check the length of the stack, if it's empty it's valid if not it's invalid.

(b) Implement your algorithm in Python. When run, your code should prompt the user to input the string of parentheses; then, it should correctly output "The expression is valid" or "The expression is not valid" . You may assume that your input string will contain only parenthesis characters, and no other special characters. That is, your code is expected to be able to handle inputs like '[{{()}}]', but you do not need to worry about dealing with inputs like '[,{,{,(,),},},]' or '[ { { ( ) } } ]' .

```python
PARENTHASIS_MAP: dict[str, str] = {
    ')': '(',
    '}': '{',
    ']': '[',
}

def validate_parenthasis(expression: str) -> str:
    STACK: list[str] = []

    for char in expression:
        if char in PARENTHASIS_MAP:
            top_element: str

            if len(STACK) > 0:
                top_element = STACK.pop()

            if PARENTHASIS_MAP[char] != top_element:
                return f"The expression: {expression} is not valid"
        else:
            STACK.append(char)

    if len(STACK) == 0:
        return f"The expression: {expression} is valid"
    else:
        return f"The expression: {expression} is not valid"

print(validate_parenthasis('({()})'))
```

# Question 2 (60 points)
A binary tree is called perfectly balanced, if the left and right sub-trees of all its nodes have exactly the same height. 

(a) Prove that any (non-empty) perfectly balanced binary tree of height ℎ has exactly $$2^{ℎ+1} − 1 \text{ nodes}$$**Hint: Try using mathematical induction.** **(13 points)**

**BASIS STEP**
$$2^{1} - 1 \text{ nodes}$$
$$1 - 1 = 0$$
**INDUCTIVE HYPOTHESIS**

$$\text{Sum of Nodes}=2^{h+1}-1$$

**INDUCTIVE STEP

Add sub in (k+1) to height, to show it will work for another root.

RHS** = $2^{k+1+2} - 1$
**RHS** = $2^{k+2} - 1$

If we can prove it works for a root and two children we can prove it works for everything else:

A root will include:

- Root node = 1
- Left tree = $2^{k+1}-1$
- Right tree $2^{k+1}-1$

**LHS** = $1 + 2^{k+1}-1 + 2^{k+1}-1$
**LHS** = $2(2^{k+1})-1$
**LHS**= $2^{k+2}-1$

**LHS** = **RHS**

(b) Give two different orderings in which we can enter the values $\{1, 2, … , 7\}$ in a (initially empty) binary search tree (BST) so that in the end it is perfectly balanced. For one of these input sequences (whichever you like), draw all intermediate BSTs that arise after each insertion (that is, you have to draw seven BSTs). 

**(10 points)** 

```
## Orderings
	
	[4, 2, 1, 3, 6, 5, 7]
	[4, 6. 5, 7, 2, 1, 3]


## Intermediates

					4

					4
				  /
				2

					4
				  /
				2
			  /
			1 

					4
				  /
				2
			  /   \
			1       3

					4
				  /   \
				2       6  
			  /   \ 
			1      3


					4
				  /   \
				2       6  
			  /   \    /
			1      3  5

					4
				  /   \
				2       6  
			  /   \    /  \
			1      3  5    7

```

(c) Draw two different BSTs whose in-order traversal outputs the sequence $1, 2, 3, 4, 5$. 

**(7 points)**

```
Since there is no mention of it, I'm assuming these aren't meant to be balanced... Which makes this really funny.

## Binary Search Tree One
						
					5
				  /
				4
			  /
			3
		  /
		2
	  /
	1 


## Binary Search Tree Two
		
	1
	  \  
		2
		  \
			3
			  \
				4
				  \
					5
```

(d) Implement the following algorithm in Python: you ask the user to input a positive integer $n$. Then, for each of the $n!$ many different permutations of the values $1, 2, … , n,$ you compute the height of the BST that arises if we insert, at an initially empty BST, that specific sequence of elements. Then, you print a histogram with the frequencies of the different heights than can arise, as well as the average height. Your output should be in the following form (here given for $n = 6$): 

| Height | Frequency |
| ------ | --------- |
| 0      | 0         |
| 1      | 0         |
| 2      | 80        |
| 3      | 400       |
| 4      | 208       |
| 5      | 32        |

**Average height of BSTs: 3.2666666666666666** 

That is, for each possible value of the height $ℎ = 0, 1, … , n − 1,$ at the column "Frequency" we write down how many of the n! permutations resulted in a BST of height equal to ℎ.

For your Python implementation, feel free to import the class permutations from Python's module `itertools`, which you can use to iterate over permutations. In other words, you are allowed to use the following call at the preamble of your Python code 

```python
from itertools import permutations
```

but you are not allowed to import any other additional functionality or any other modules.

**Note on running time**: Since the total number of permutations n! grows exponentially as a function of parameter n, naturally you will observe that your script slows down (dramatically) for larger values of n. This is unavoidable, given the requested implementation, and you don't need to worry too much about optimizing your running time: as long as your script runs within a reasonable amount of time (let's say, 30 seconds), for up to n = 10 you are good to go!

```python
from itertools import permutations

class Node:
    def __init__(self, key=0) -> None:
        self.key: int = key
        self.left: 'Node' = None
        self.right: 'Node' = None

class BinarySearchTree:
    def __init__(self) -> None:
        self.root = None

    def insert(self, key: int) -> None:
        insert_node = Node(key)
        current_node: Node = self.root
        parent_node: Node = None

        while current_node != None:
            parent_node = current_node
            if insert_node.key < current_node.key:
                current_node = current_node.left
            else:
                current_node = current_node.right

        if parent_node == None:
            self.root = insert_node
        elif insert_node.key < parent_node.key:
            parent_node.left = insert_node
        else:
            parent_node.right = insert_node

    def minimum(self) -> int:
        current_node = self.root
        while current_node.left != None:
            current_node = current_node.left
        return current_node.key

    def maximum(self) -> int:
        current_node = self.root
        while current_node.right != None:
            current_node = current_node.right
        return current_node.key

    def search(self, node: Node, key: int) -> Node:
        if node == None or key == node.key:
            return node

        if key < node.key:
            return self.search(node.left, key)
        else:
            return self.search(node.right, key)

    def size(self, node: Node) -> int:
        if node == None:
            return 0
        else:
            return self.size(node.left) + self.size(node.right) + 1

    def height(self, node: Node) -> int:
        if node == None:
            return 0
        if node.left == None and node.right == None:
            return 1

        return max(self.height(node.left), self.height(node.right)) + 1

def calcPermutations() -> None:
    length: int = 6
    permutations_list = permutations(range(1, length + 1), length)
    frequency: dict[int, int] = {}

    for permutation in permutations_list:
        tree = BinarySearchTree()
        for node in permutation:
            tree.insert(node)

        height = tree.height(tree.root)

        if (height in frequency):
            frequency[height] += 1
        else:
            frequency[height] = 1

    formatPrint(frequency)

def formatPrint(frequency: dict[int, int]) -> None:
    print()

    max_height = max(frequency.keys()) or 0
    complete_frequency = {}

    for height in range(1, max_height + 1):
        complete_frequency[height - 1] = frequency.get(height, 0)

    sorted_frequency = sorted(complete_frequency.items())

    print("+ -------- + ----------- +")
    print("|  Height  |  Frequency  |")
    print("+ -------- + ----------- +")

    for height, freq in sorted_frequency:
        print(f"| {height:8} | {freq:11} |")

    print("+ -------- + ----------- +")
    print()

calcPermutations()
```
