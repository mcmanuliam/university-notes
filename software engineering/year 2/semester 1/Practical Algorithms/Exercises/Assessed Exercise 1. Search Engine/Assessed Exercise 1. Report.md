#pa 

# Practical Algorithms 2024-25, University of Glasgow
Assessed Exercise 1 - *The PA Directory Search Engine*

**Submitted by:**
Liam McManus

# A: Complexity Analysis
Present the following complexity analysis in this report:

+ Big-O complexity of the indexing operation.
+ Big-O complexity of a search operation (given that indexing has been done already).
+ Big-O complexity of a search operation if it were implemented in a brute force fashion (that is, no indexing performed, all search queries go through the entire text of all files every time).

You should be very clear about what you mean by n when presenting your Big-O complexity analysis.

*Note*: You don't have to do a line-by-line code-analysis like we do in certain other problems. Instead, present your analysis as a text description that walks through the relevant operations, comments on their complexity with rationale, and then presents the overall complexity.
## Your Answer

### Indexing
I've split these up into different functions, if you take a look at the code you will see this is all included in the index builder class. I'll detail each helper functions complexity and total it all together for the build function.

#### Helper Methods
##### Term Frequency
This is stored for each unique word in a given document.

- Initialise an empty dictionary for term frequencies. **o(1)**
- Calculate the total number of tokens. **o(1)**

- Iterate over tokens in the file. **o(n)**, where n is the number of tokens.
    - Check if a token exists in the dictionary. **o(n)** worst-case 
    - If not, initialize its frequency. If it exists, update the frequency. **o(n)** for each update or addition.
    
**This means it's o(n) for n, where n is the total number of tokens in a file.**
##### Forward Index
This index associates all documents with the associated words.

- Using `setdefault` to set a default list for the document. **o(1)**
- Add to the document's token list with the current line's tokens. **o(1)**

**This is simply o(1).**
##### Inverted Index
This is the reverse of the forward index, listing all words with associated documents.

- Create a unique set of tokens for the line. **o(n)** - where **n** is the number of unique tokens.

 - Iterate over the unique set of tokens **o(n)**:
    - Check if the token exists in the index. **o(1)** for dictionary lookups.
    - Add the document to the token's list if it's not already there - **o(1)**
        
**This means it's o(n), where n is the amount of unique tokens in a line**

#### Build
Given a file path, name and calculates it's indexes.

- Initialise indeclxes **o(1)** for each index.
- Open file and loop over each line **o(l)** where **l** is the number of lines:
	- Tokenise and Clean every line **o(c)** where **c** is the length of the lines input.
	
	- Accumulate tokens and calculate both the forward and inverted index builders.
		- Forward index: **O(1)**.
		- Inverted index: **O(n)** where n is the total tokens.
	
	- Calculating term frequency for all tokens **o(u)** where **u** is the number of unique tokens.
	- Calculating doc rank which is just **o(1)**

For the loop it's $o(l+n)$ where $l$ is the number of lines and $n$ is the number of tokens. $o(u)$ for calculating the term frequency and in total $o(n)$, as this is the most dominant term out of the three, this means as number of tokens grows with larger datasets so too does the overall complexity.

### Searching
Assuming indexing is already complete.

- Tokenise the search phrase for **o(p)** where **p** is the length of the search phrase.

- Loop over all docs in the forward index, this will be **o(d)** and let's say **d** is the number of documents.
	- Loop over all tokens in the search phrase, this will run for **o(t)** where **t** is he number of tokens. Combined this would be **o(d * t)**
	
- Now sorting is where it gets a bit confusing Pythons [sort](https://www.geeksforgeeks.org/sort-in-python/) function uses the [Timsort](https://en.wikipedia.org/wiki/Timsort) Algorithm, this is on average is $o(r \log (r))$ where r is the list of results.

- I'm not 100% sure about this but I believe it will be:
$$o(p+ d * t + r\log(r))$$
Where $d$ is the total number of documents, $t$ is the number of tokens, where **p** is the length of the search phrase and $r$ is the number of items in the results.

### Brute Force Searching
This means no indexing and just running through all items in the directory.

- Iterating over all documents **o(d)** where **d** is the number of documents.
- Check for search phrase in each documents **o(s * p)** where **s** is the the size of the document and **p** is the length of the search phrase.

In total this should be something along the lines of:
$$o(d * s * p)$$
Where **d** is the number of documents, **s** is the size of the document and **p** is the length of the search phrase.

---

# B: Choice of Data Structures

Explain and justify your choice of data structures.
## Your Answer

I tried my best to make my code a bit more type heavy, which is an absolute pain, I get it's not meant to be typed at all but if they are gonna have implicit typing you'd think it would be a bit easier to work with.
### Indexing

```
indexing: TypeAlias = dict[str, list[str]]
```

I've used one type to represent both the forward index and the inverted index.

- Inverted index maps tokens to the list of documents they are in, allow for quick and simple reverse lookups for search terms.

- Forward index simply maps documents to a list of tokens, which is easy for looking up the tokens in a document.
### Term Frequency (TF)

```
dict[str, dict[str, float]]
```

- This nested dictionary maps document names to another dictionary of tokens and their frequencies in that document. It makes accessing the term frequency for any given token in a document easy and very efficient.

### Inverse Document Frequency (IDF)

```
dict[str, float]
```

- IDF values are stored for each unique token. Using a dictionary where the keys are tokens and the values are their IDF scores allows for easy access during TF-IDF calculation.

### Using a Set to Avoid Dupes

```
for token in set(tokens)
```

- When merging the inverted index, using `set` ensures that duplicate entries are removed without manual checks.

---

# C: Discuss Extra Features, if Any:

If you implemented any extra feature on top of the requirements noted in this handout, briefly describe them here.
## Your Answer

I implemented a pretty printer for the search engine, it's essentially just a class which prints the formatted file with some added metadata and a file path.

***Just a heads up if you read this before testing please change the `BASE_PATH` in `pa_search_engine.py` to the directory where the file is located (no trailing slash pls) this will be used for links in the pretty printer.***

