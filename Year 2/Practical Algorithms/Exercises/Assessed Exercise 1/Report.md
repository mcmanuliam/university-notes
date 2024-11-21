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
I've separated indexing into a new class called the index builder, this helps abstract and keeps all the logic separate although it does kind of make this a bit of a pain, I've measured each individual functions complexity below and I'll sub these into the main build function at the end.

#### Term Frequency ($o(n)$)

```python
indexing: TypeAlias = dict[str, list[str]]
term_frequency: TypeAlias = dict[str, dict[str, float]]

def get_term_frequency(
    term_freq: term_frequency,
    tokens: list[str],
    filename: str,
) -> None:
    """**Term Frequency (TF).**
    This is stored for each unique word in a given document. Its value will be
    between 0 and 1, calculated as follows: `TF(word) = Number of occurrences o
    word in a document \ Total number of words in the document`, this metric
    indicates how frequently a word appears in a given document.

    For example:
    - **anna_karenina.txt**:
    - `'the'`: 0.05015589569160998
    - `'project'`: 0.00025793650793650796

    - **second.txt**:
    - `'why'`: 0.0065040650406504065
    - `'said'`: 0.013008130081300813
    - `'the'`: 0.055284552845528454
    """
    total_tokens = len(tokens)
    count = {}

    for token in tokens:
        count[token] = count.get(token, 0) + 1

    term_freq[filename] = {}
    for token, count in count.items():
        term_freq[filename][token] = count / total_tokens

```
$$o(1) + o(1) + o(n) + 4o(n) + o(1) + 3o(n) 5o(n)$$
$$o(n) + 4o(n) + 3o(n) 5o(n)$$
$$o(n)$$
---

#### Build ($o(n)$)

```python
indexing: TypeAlias = dict[str, list[str]]
term_frequency: TypeAlias = dict[str, dict[str, float]]

def build(filename: str, filepath: str)-> tuple[
	indexing,
	indexing,
	term_frequency,
	float
]:
	""""
	Given a filepath and name, indexes it by calculating its:
	- forward_index
	- term_freq
	- doc_rank
	- and updates the invert_index (which is calculated across all files)
	"""
	forward_index: dict[str, list[str]] = {} # o(1)
	invert_index: dict[str, list[str]] = {} # o(1)
	term_freq: dict[str, dict[str, float]] = {} # o(1)
	doc_rank: float = 0.0 # o(1)
	tokens_acc: list[str] = [] # o(1)
	
	with open(filepath, 'r', encoding="utf-8") as file: # o(2)
		for line in file.readlines(): # 2o(n)
			tokens = tokenise(line) # 10o(n)
			tokens_acc.extend(tokens) # 2o(n)
			
			IndexBuilder.__get_forward_index(forward_index, tokens, filename)
			IndexBuilder.__get_inverted_index(invert_index, tokens, filename)
		
		IndexBuilder.__get_term_frequency(term_freq, tokens_acc, filename) # o(n)
		doc_rank = 1 / len(tokens_acc) if tokens_acc else 0 # 4o(1)
		
	return forward_index, invert_index, term_freq, doc_rank # o(1)
```

---

# B: Choice of Data Structures

Explain and justify your choice of data structures.
## Your Answer

  
  

# C: Discuss Extra Features, if Any:

If you implemented any extra feature on top of the requirements noted in this handout, briefly describe them here.
## Your Answer