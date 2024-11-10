# Complexity Analysis

## Indexing
I've separated indexing into a new class called the index builder, this helps abstract and keeps all the logic separate although it does kind of make this a bit of a pain, I've measured each individual functions complexity below and I'll sub these into the main build function at the end.

### Term Frequency

```python
def __get_term_frequency(
	term_freq: dict[str, dict[str, float]],
	tokens: list[str],
	filename: str,
) -> None:
	"""**Term Frequency (TF).**
    This is stored for each unique word in a given document. Its value will be between 0 and 1, calculated as follows:
    `TF(word) = Number of occurrences of word in a document \ Total number of words in the document`,
    this metric indicates how frequently a word appears in a given document.

    For example:
        - **anna_karenina.txt**:
        - `'the'`: 0.05015589569160998
        - `'project'`: 0.00025793650793650796

        - **second.txt**:
        - `'why'`: 0.0065040650406504065
        - `'said'`: 0.013008130081300813
        - `'the'`: 0.055284552845528454
    """
    total_tokens = len(tokens) # o(1)
    count = {} # o(1)

    for token in tokens: # o(n)
        count[token] = count.get(token, 0) + 1 # 4o(n)

    term_freq[filename] = {} # o(1)
    for token, count in count.items(): # 3o(n)
        term_freq[filename][token] = count / total_tokens # 5o(n)
```
$$o(1) + o(1) + o(n) + 4o(n) + o(1) + 3o(n) 5o(n)$$
$$o(n) + 4o(n) + 3o(n) 5o(n)$$
$$o(n)$$

### Build

```python
def build(filename: str, filepath: str)-> tuple[
	dict[str, list[str]],
	dict[str, list[str]],
	dict[str, dict[str, float]],
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

# Choice of Data Structure

# Extra Feature(s)
## Printer
The `Printer` class is used to print out a cleaner and more detailed view including file name, file size, last modified and the file path (should be clickable in specific views, try in your IDE).