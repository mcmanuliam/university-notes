# 1. Big-O Notation

## Motivation
What characteristics do you want your program to have???

- Correct
- Readable (Doesn't mean insane amount of comments)
- Reusable (Abstraction)
- Testable
- Elegant

- **Efficient**
	- How *long* will it take to run? (execution time)
	- How much *space* (memory) will it take?
		- Not heavily focused on nowadays
		- We have tons of memory, no need to optimize
			- ^ Take a look back at `TunedIn` caching if you don't remember

## Execution time = Number of Steps
If we can assume each `step` uses the same amount of time, then we can use the steps taken as a proxy for execution time.

## Takeaways
 - More than specific performance at specific problem sizes, we are interested in the trends.
	 - How does time complexity scale with the problem size? 

- At small problem sizes, we don't often get a true picture.
	- We should consider large problem sizes for such analysis

## Algorithm Analysis
Analyze the time and space efficiency of an algorithm, without reference to specific implementation details, the way I am thinking right now is just going through specific steps rather than timing exact programs.

> "Algorithm analysis is a way to compare the time and space efficiency of programs with respect to their possible inputs, but irrespective of other context.

### Empirical Vs Analytical Approach

- What is more useful is a more abstract, analytical approach.
	- Uses a high-level description of the algorithm instead of a specific implementation
	- Characterizes running time (and space) as a function of the input size (𝒏)
	- How does my running time 𝑇 𝑛 change, as I increase my input size 𝑛 

- Analytical studies are essential just creating the graphs above without running any code.

| Empirical Studies                                                                                                                                                                                            | Theoretical Analysis                                                              |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------- |
| You need to implement a possibly difficult algorithm                                                                                                                                                         | Uses a high-level description of steps                                            |
| Results may not be indicative of the run time on other inputs not included in the test.<br><br>Imagine a list of numbers being input, the execution time directly relates to how already sorted the list is. | Characterizes run time as function of input size (*n*)                            |
| In order to compare two algorithms, the same hardware and software components must be used                                                                                                                   | Allows us to evaluate the speed of an algo independently of the hardware/software |
| Results may be more accurate                                                                                                                                                                                 | Results will be *indictive*                                                       |

The questions of the analytical approach are:
- What is precisely the property of the algorithm that we want to capture analytically?
- (Time) Complexity, as in: "how many steps will it require"
- But: best case, worst case, average case? • How do we express it?
- How do we calculate it?

## What Does O(f(n)) Represent?
- We make more simplifying assumption in our complexity analyisis: It is only the **Order of Growth** that interests us (rather than the exact expression T(n) of the running time).

- This means we can focus only on the highest-order terms in a formula and ignore others (below this would be 4n^2).

- To give a quick example
	- Given you found T(n) for a particular algo to be
$$
t(n) = 4n^2 + 2n + 10000
$$
	- Then the order of growth is simple n^2
	- this means  𝑇(𝑛) = 4𝑛2 + 2𝑛 + 10000 is of the orde 𝑂(𝑛2)

## Some Common "Orders of Growth" (or "Growth Rates")

#### 0(1) - Constant Run time
Will always be the same amount of time no matter the size of input.

Cleaning house for a party
- No matter how many guests come, cleaning the house prior to their arrival will take the same amount of time

#### O(n) - Linear Growth
Size of input is directly related to the runtime

- Passing the roast around the table at a party
	- If guests are doubled, then wait twice as long to pass it round

- Summing up 𝒏 integers using a loop
	- If you double 𝒏, you will loop 2x more times, and take (roughly) twice as long

#### O(n2) – Quadratic Growth
Everyone in the party gives everyone else a hug
- for 𝑛 guests, it is 𝑛 − 1 + 𝑛 − 2 + ⋯ + 2 + 1
- equal to (𝑛2 − 𝑛) / 2
- the dominant term here is n2 (we will revisit this concept in a bit) • So this is 𝑂(𝑛2)

Multiply two 𝑛-bit numbers

#### O(2n) – Exponential Growth
Doubles size at every step
- "Growth goes completely whack"

Good example of this is the legend of the rice and the chessboard:

>
> *"A wise old ruler wanted to reward his servant for an act of extraordinary bravery. The servant said:*
> 
> 'Master I ask you for just one thing. Take your chessboard and place on the first square one grain of rice. On the first day I will take this grain home to feed my family. On the second day place on the second square 2 grains for me to take home. On the third day cover the third square with four grains for me to take. Each day double the number of grains you give me until you have placed rice on every square of the chessboard. Then my reward will be complete.'
> 
> The wise old ruler replied:_
> 
> This sounds like a small price to pay for your act of incredible bravery, I will ask my servants to do as you ask immediately.'
>

#### 𝑂(log 𝑛) – Logarithmic Growth
The inverse of the exponential function
- You have to double the size of the problem before you need one additional step
- Because every step halves the remaining problem size

Think about a bubble search.

#### 𝑂(𝑛!) – Factorial Growth
Grows real quick, real fast!!

Our initial card shuffling sorting algorithm (Bogo sort) follows this
- There are 52! possible card permutations

# 2. Sets

## Sets - Introduction
- Set theory is a very important area of **mathematics**
- The set is considered the most fundamental notion in all of mathematics!
- The notion of function is built on top of sets, A function assigns to each element of one set, exactly one element of another set.

## Set: Definition
- A set is a collection of objects (called its elements/members) with a key property: membership
	- That is: "is this element a member of this set or not"? 

- Hence a set is an unordered collection of (unique) objects.
	- so, no concept of first element, 𝑛𝑡ℎ element, neighbouring element, etc. 
	- repetition does not matter
		- has no impact on whether or not an element is a member of a set

- A set is said to contain its elements. 

- The notation 𝑎 ∈ 𝐴 denotes that 𝑎 is an element of the set 𝐴.
	- If 𝑎 is not a member of 𝐴, we write: 𝑎 ∉ 𝐴

## Roster Notation

```
S = {a, b, c, d}
```

Just like an object in code, order wont have any effect:

```
S = {a, b, c, d} = {d, b, c, a}
```

Multiplicity is ignored, this is like the reduce function in lodash:

```
S = {a, b, c, d} = {a, a, a, b, c, d}
```

Ellipses (…) may be used to describe a set without listing all its members, when the pattern can be clearly derived from the context:

```
S = {a, b, ..., c}
```

## Set-Builder Notation
Specify the property/properties that characterize its membership:

```python
𝑆 = {𝑥 | 𝑥 𝑖𝑠 𝑎 𝑝𝑜𝑠𝑖𝑡𝑖𝑣𝑒 𝑖𝑛𝑡𝑒𝑔𝑒𝑟 𝑙𝑒𝑠𝑠 𝑡ℎ𝑎𝑛 100}
𝑂 = {𝑥 | 𝑥 𝑖𝑠 𝑎𝑛 𝑜𝑑𝑑 𝑝𝑜𝑠𝑖𝑡𝑖𝑣𝑒 𝑖𝑛𝑡𝑒𝑔𝑒𝑟 𝑙𝑒𝑠𝑠 𝑡ℎ𝑎𝑛 10}
𝑃 = {𝑥 ∈ ℤ+ | 𝑥 𝑖𝑠 𝑜𝑑𝑑 𝑎𝑛𝑑 𝑥 < 10}
# ^ x is in Z and x is odd and x < 10 (this could be on the right but it's normal o do it on the left with set members), the plus is essentially a filter to positive numbers, in the case there is a star that means the zero get's filtered.
```

This works kind of like types in the way that you can specify something like `keyof {{interface}} and string` and through that typing we can determine the values in the set.

- A predicate may be used for succinctness
	- (where a predicate is basically a logical statement that can be True or False, depending on some variable(s).)

```python
𝑆 = {𝑥 | 𝑃(𝑥)}

# | can be read as “such that”
# ∈ can be read as “belongs to” 
# 𝑷(𝒙) here means 𝑃 is a predicate that is True for 𝑥
```

Example: 
- Example: `𝑆 = {𝑥 | 𝑃𝑟𝑖𝑚𝑒(𝑥)}`
- Example: Set of positive rational numbers: 
	`ℚ+ = {𝑥 ∈ ℝ | 𝑥 = 𝑝/𝑞, for some positive integers 𝑝, 𝑞}`


##### Some Pre-requisite Symbols

| Symbol  | Meaning                          |
| ------- | -------------------------------- |
| ∀       | For all                          |
| A → B   | If A is true, then B is true     |
| 𝐴 𝐵 A | is true if and only if B is true |
| ∧       | Logical AND                      |
| ∨       | Logical OR                       |

Examples:
- {1, 3, 5} = {3, 5, 1}
- {1, 5, 5, 5, 3, 3, 1} = {1, 3, 5}
- {1, 3, 7} ≠ {1, 3}

#### Subsets
The set A is a subset of B, denoted by  `𝐴 ⊆ 𝐵`, if and only if every element of A is also an element of B.
- Imagine inheritance, B is a parent of A.

Formally: `𝐴 ⊆ 𝐵` if and only if `∀𝑥(𝑥 ∈ 𝐴 → 𝑥 ∈ 𝐵 ) `

Note that:
- `∅ ⊆ 𝑆` for every set 𝑆.
	- Empty set doesn't contain anything that the parent doesn't.
- `𝑆 ⊆ 𝑆` for every set 𝑆.

#### Equality
Two set are equal if and only if they are subsets of each other:

```
A = B if and only if 𝐴 ⊆ 𝐵 ∧ 𝐵 ⊆ 𝐴
```
***Note: Imagine the full circle.***

![[image17.png]]

#### "Proper" Subset
 We say that 𝐴 is a proper subset of 𝐵, if and only if:
 - 𝐴 is a subset of 𝐵, but 𝐴 is not equal to 𝐵: 
 
 ```
 𝐴 ⊆ 𝐵 ∧ 𝐴 ≠ 𝐵
 ```
#### Set Cardinality
The cardinality of a finite set A, denoted by |A|, is the number of (distinct) elements of A.

***This is essentially the length of the type. How many items are implicitly or explicitly in the set***

Examples: 
- ∅ = 0 
- Let 𝑆 be the set of all letters of the English alphabet. Then |𝑆| = 26
- |{1, 2, 3}| = 3
- |{∅}| = 1
- Set of integers? Infinite 
	- Think about countable infinities
		- numbers including negatives are a larger infinite than the positive integers.
		- What about real numbers they are a larger infinite than integers.

#### Power Sets
The power set of a given set 𝐴, denoted 𝒫(𝐴), is the set of all subsets of 𝐴.

- This is a type that contains a bunch of other types:
	- Object is a Power set of date, 
	
```
Object
├── Array
├── Function
├── Date
```

- Example: If `𝑆 = {𝑎, 𝑏, 𝑐}` then 

```
𝒫 𝐴 = {∅, {𝑎}, {𝑏}, {𝑐}, {𝑎, 𝑏}, {𝑎, 𝑐}, {𝑏, 𝑐}, {𝑎, 𝑏, 𝑐}}
```

- If a set has 𝑛 elements, then the cardinality (i.e. size) of the power set is 2𝑛. That is, 
	- `𝐴 = 𝑛 → 𝒫 𝐴 = 2𝑛`

Let `𝑆 = 𝑎, 𝑏, 𝑐 `. Each subset of `𝑆` can be represented as a bit string of length 𝑆 = 3 , where each component is: 
- 1 if corresponding element is a member of `𝑆` 
- 0 if not a member

## Cartesian Product
The Cartesian product is a way to combine two sets by pairing every element of one set with every element of another set.

### Simple Explanation
If you have two sets, say:

- Set A: `{1, 2}`
- Set B: `{x, y}`

The **Cartesian product** of A and B, written as `A × B`, is the set of all possible ordered pairs where the first element is from A and the second element is from B.

So, in this example, `A × B` would be:

```
A × B = { (1, x), (1, y), (2, x), (2, y) }
```

#### How It Works

1. **Take one element** from the first set (e.g., `1` from A).
2. **Pair it with each element** in the second set (so, `1` pairs with both `x` and `y`).
3. Repeat this for every element in the first set.

#### Visual Example
Think of it like a grid where Set A elements are on one axis and Set B elements are on the other. Each cell in the grid is a unique pairing:

||x|y|
|---|---|---|
|1|(1,x)|(1,y)|
|2|(2,x)|(2,y)|

#### Key Points

- **Order Matters**: `(1, x)` is different from `(x, 1)`, so the order of sets matters.
- **Size of Result**: If Set A has `m` elements and Set B has `n` elements, the Cartesian product will have `m * n` pairs.

#### Everyday Example
If you have two shirts (A: `red` and `blue`) and two pants (B: `jeans` and `khakis`), the Cartesian product would give you all possible outfit combinations:

```
Outfits = { (red, jeans), (red, khakis), (blue, jeans), (blue, khakis) }
```

This is the Cartesian product of your shirts and pants!

```javascript
function cartesianProduct(setA, setB) {
	const product = [];
	
	for (const elemA of setA) {
		for (const elemB of setB) {
			product.push([elemA, elemB]);
		}
	} 

	return product; 
}

const setA = ['a', 'b'];
const setB = ['z', 'y', 'z'];
console.log(JSON.stringify(cartesianProduct(setB, setA)));
```

### Boolean Algebra!
Set theory can be interpreted as an instance of an algebraic system called a Boolean Algebra.

- We will look at another Boolean algebra later called "propositional calculus

The operators in set theory are analogous to the corresponding Boolean operators we have already seen.

Recall the definition of universal set U

- All sets are assumed to be subsets of U

#### Union

- **Definition**: The union of the sets 𝐴 and 𝐵, denoted by 𝐴 ∪ 𝐵, is the set:

```
{x|x ∈ A ∨ x ∈ B} # Analogous to the logical OR
```

- **Example**: What is {1, 2, 3} ∪ {3, 4, 5} ?
- **Answer**: {1, 2, 3, 4, 5}

![image18.png](app://cbd2d3ede902565f3c721020edf2696810d3/Users/liam@veryconnect.com/Desktop/uni/notes/Assets/images/image18.png?1732178025113)

#### Intersection

- **Definition**: The intersection of sets A and B, denoted by A ∩ B, is:

```
{x|x ∈ A ^ x ∈ B} # Analogous to the logical AND
```

- ***Note: if the intersection 𝐴 ∩ 𝐵 is empty, then sets 𝐴 and 𝐵 are said to be disjoint.***
    
- **Example**: What is {1, 2, 3} ∩ {3, 4, 5} ?
    
    - **Answer**: {3}
- **Example**: What is {1, 2, 3} ∩ {4 , 5, 6} ?
    
    - **Answer**: ∅

![image19.png](app://cbd2d3ede902565f3c721020edf2696810d3/Users/liam@veryconnect.com/Desktop/uni/notes/Assets/images/image19.png?1732178025113)

#### Complement

- **Definition**: the complement of 𝐴 (with respect to a given universal set 𝑈), denoted by Ā (or 𝐴𝑐) is the set:

```
Ā = 𝑥 ∈ 𝑈 𝑥 ∉ 𝐴} # Analogous to the logical NOT
```

- **Example**: If 𝑈 is the positive integers less than 100, what is the complement of {𝑥 | 𝑥 > 70} ? Answer: {1, 2, … , 70} ?

```
Negation with: x<=70
```

- **Answer**: {1, 2, …, 70}

![image20.png](app://cbd2d3ede902565f3c721020edf2696810d3/Users/liam@veryconnect.com/Desktop/uni/notes/Assets/images/image20.png?1732178025114)

#### Difference

- Definition: The difference of 𝐴 from 𝐵, denoted by 𝐴 – 𝐵 (or 𝐴 ∖ 𝐵), is the set containing the all elements of 𝐴 that are not in 𝐵.

```
𝐴 − B = {𝑥 | 𝑥 ∈ 𝐴 ∧ 𝑥 ∉ 𝐵} = 𝐴 ∩ Ḃ
```

- 𝐴 − 𝐵 is also called the complement of B with respect to A

![image21.png](app://cbd2d3ede902565f3c721020edf2696810d3/Users/liam@veryconnect.com/Desktop/uni/notes/Assets/images/image21.png?1732178025114)

|**Category**|**Law**|**Symbolic Representation**|**Explanation**|
|---|---|---|---|
|**Identity Laws**|Union with Empty Set||The union of any set with the empty set results in the set itself.|
||Intersection with Universe||The intersection of any set with the universal set results in the set itself.|
|**Domination Laws**|Union with Universe||The union of any set with the universal set results in the universal set.|
||Intersection with Empty Set||The intersection of any set with the empty set results in the empty set.|
|**Idempotent Laws**|Union with Itself||The union of any set with itself is just the set.|
||Intersection with Itself||The intersection of any set with itself is just the set.|
|**Double Complement Law**|Double Complement||Taking the complement twice returns the original set.|
|**Commutative Laws**|Union||The order of sets in a union doesn't matter.|
||Intersection||The order of sets in an intersection doesn't matter.|
|**Associative Laws**|Union||The grouping of sets in a union doesn't matter.|
||Intersection||The grouping of sets in an intersection doesn't matter.|
|**Distributive Laws**|Union over Intersection||Union distributes over intersection.|
||Intersection over Union||Intersection distributes over union.|
|**De Morgan's Laws**|Complement of Union||The complement of a union is the intersection of the complements.|
||Complement of Intersection||The complement of an intersection is the union of the complements.|
|**Absorption Laws**|Absorption of Union||Union of a set with its intersection with another set is just the set.|
||Absorption of Intersection||Intersection of a set with its union with another set is just the set.|
|**Complement Laws**|Union with Complement||The union of a set with its complement is the universal set.|
||Intersection with Complement||The intersection of a set with its complement is the empty set.|
|**Complement Conversion to Difference**|Set Difference and Complement||Intersection with the complement of another set is equivalent to the set difference.|
# 3. Functions and Relations
