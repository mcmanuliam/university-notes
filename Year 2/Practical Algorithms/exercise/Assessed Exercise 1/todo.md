- [ ] Practical Algorithms - Assessed Exercise 1 ⏫ 📅 2024-11-25

**Opened:** Tuesday, 5 November 2024, 9:00 AM
**Due:** Monday, 25 November 2024, 10:00 PM

This project-based assessed exercise is worth 10% of the course. The handouts contains all relevant information for completing and submitting project. Some other files are needed to complete the project, and are available in the provided zipped folder.  
  
You are allowed to complete the project in groups of two, but if so, **each student still needs to write their own report**. Both students should submit the full solution along with their own reports, and clearly note in the report if they did the project with another student.

---

This assessed exercise will be marked out of a toal of 60 marks, and accounts for 10% of the course total. The submission deadline would be noted on the course moodle.

**Please note that:** 
1. You can choose to complete this project on your own, or in a group of maximum size, In case of working as a group, the code submitted will be assumed to be the same for both and marked once, but each of the two students must submit separate reports that they write individually, on their own (though you can certainly consult one another when writing it). 

2. You must write your own code. Some skeleton files have been provided to help you get started, but you can choose to ignore them. You are free to refer solutions to problems provided in this course, as well as any online resources or forums, but you should then write your own code (that is: no copy-pasting please). 

3. In a similar vein, feel free to work alongside and discuss the project classmates outside your group, but what you write and submit must have been done entirely by you/your group members. 

4. In general, you should limit your code to using the barebones Python, without using any libraries (other than some obvious ones like time, random, sys). If you have any doubts about use of a particular library, then please ask the instructor. 

5. You are free to use Python's built-in data types like lists and arrays, as well as Python's built-in "sorted" function.

6. You can use generative AI as you would a tutor or a peer; to learn, recall, or understand relevant syntax, or to explain something noted in this handout. You are not allowed to ask it to solve the problem for you. Hopefully this distinction is clear enough, but reach out to your instructor or tutor for any more specific queries. Use of generative AI is not allowed at all for writing the report. 

---
#### Overview of Project
The purpose of this project is to design a small search engine that can search all text files in a given directory for text query entered by the user. 

The query will be entered in the form of a phrase which may be composed of multiple words. When a user enters a phrase, only documents which have each of the words in the phrase (in any sequence) should be returned, ordered by the document rank as explained later. (You are not asked to create more advanced search features like matching of exact phrase if query given in quotes, use of logical operators like +, and, etc.). The search engine should not be case sensitive. 

Multiple approaches can be taken in constructing such a search engine. You are being asked to take a specific approach explained as follow. This approach is a simplified version of the algorithm given in [2], which in turn is based on the original paper for Google search engine [3].

To complete this project, you will be required to implement three main tasks: Crawling, Indexing, and Searching. 

#### Crawling
When the search engine is run, it will first crawl all text files in the target folder, which basically means reading them into memory from the external storage (file) one by one, and indexing them.

#### Indexing
To enable the search to return quickly (that is, you don't want every new search query to search sequentially through all the files), you will create an index. The details are described as follows. While you are reading in the files to create the indices though, you will have to be careful about cleaning up the text to remove special characters and white spaces, and also deal with case sensitivity (recall, the search engine is meant to be case insensitive). 

To create a complete index of your target search folder, you need to create four variables. You should use appropriate data structures to store each of these four crucial variables.

1. **Forward Index.** This index associates all documents with the associated words. E.g. 
	- `anna_karenina.t xt:` 'the', 'project', 'gutenberg', 'ebook', 
	- `second.txt:` 'why', 'said', 'the', 'old', … 
	- `war_and_peace.txt:` 'the', 'project', 'gutenberg', 'ebook', …

2. **Inverted Index.** This is the reverse of the previous index, listing all words with associated documents
	- `'the'` 'anna_karenina.txt', 'divine_comedy.txt', …
	- `project`:'anna_karenina.txt', 'divine_comedy.txt', 'little_women.txt',…
	- `immovability`:'war_and_peace.txt' 

3. **Term Frequency (TF)** is stored for each unique word in a given document. Its value will be between 0 and 1, calculated as follows:
  $$
  TF(wocrd)\frac{\text{Number of occurrences of word in a document}}{\text{Total number of words in the document}}
  $$

	This metric indicates how frequently a word appears in a given document. For example:

	- **anna_karenina.txt**:
	  - `'the'`: 0.05015589569160998
	  - `'project'`: 0.00025793650793650796
	  - …
	
	- **second.txt**:
	  - `'why'`: 0.0065040650406504065
	  - `'said'`: 0.013008130081300813
	  - `'the'`: 0.055284552845528454
	  - …
	
3. **Inverse Document Frequency (IDF)**
	**Inverse Document Frequency (IDF)** is calculated for each unique word across all documents. The value ranges between 0 and 1 and is calculated as follows:
	$$
  IDF(word) =  \frac{\text{Number of documents with word}}{\text{Total number of documents}}
  \
  $$

	For example:
	
	- `'the'`: 1.0
	- `'project'`: 0.6923076923076923
	- `'gutenberg'`: 0.6923076923076923

```python
import re

def clean(text: str):
	text = text.lower()
	text = re.sub(r'[^a-z\s]', '', text)
	return text

def parse_line(line: str):
	stripped = line.strip()
	cleaned = clean(stripped)
	print(cleaned.split())
	
parse_line('Hello my name is liam')
```

```python
def get_term_frequency(
	term_freq,
	formatted_items,
):
	number_of_items = len(formatted_items)
	occurence_map: dict[str, float] = {}
	
	for item in formatted_items:
		if item in occurence_map:
			occurence_map[item] += 1
		else:
			occurence_map[item] = 1
	
	for key, occurence in occurence_map.items():
		term_freq[key] = (occurence / number_of_items)

	return term_freq

term = {}

formatted_list = [
	'the',
	'the',
	'when',
]

print(get_term_frequency(term, formatted_list))
```


#### Document Rank (DR)
To show the result of our search in a particular order, we use metrics like term frequency (TF) and inverse document frequency (IDF) for each of the words in a given query. In addition however, we also use a metric that shows the significance of each document, independent of the specific query. If this were a web search engine, then we would be using something like Google’s page ranking algorithm to calculate this “PageRank” metric. We will keep things simple here though, and use the size of the file, such that the smaller the file, the higher its signficance. This the DocumentRank, calculated as follows: 

𝐷𝑜𝑐𝑢𝑚𝑒𝑛𝑡𝑅𝑎𝑛𝑘(𝑑𝑜𝑐𝑢𝑚𝑒𝑛𝑡) = 1 / 𝑇𝑜𝑡𝑎𝑙 𝑛𝑢𝑚𝑏𝑒𝑟 𝑜𝑓 𝑤𝑜𝑟𝑑𝑠 𝑖𝑛 𝑡ℎ𝑒 𝑑𝑜𝑐𝑢𝑚𝑒𝑛𝑡 

The intuition here is that if our search phrase is in a smaller file, its “presence” is relatively larger. You will need to calculate this rank for each document, and could do so while you are indexing them. This value, along with TF and IDF for the words in the search query, will together be used to calculate the “weight” which you will then use to sort your search results (exact formula for this weight follows).

#### Output Files
All 5 data structures calculated during the indexing and document ranking process (forward index, inverse index, TF, IDF, DR) should be stored in the form of text files. This will enable us to re-use these values in subsequent runs (though you are not asked to implement this reuse feature in this project). The provided main.py script takes care of creating these output files for you. 

#### Searching
The interesting work has happened when you have indexed the files and ranked them. The search is now simply a matter of looking up the data structures you have created in the process.

User will enter their search phrase on the command line, and your program should display an list of all files which contain that search query, ordered based on the values of TF, IDF and DR. There are many ways to use these metrics to order the search results, and we use a simple approach as follows: 

For every document, you can take the product of TF and IDF for each term of the query, and calculate their cumulative product. Then you multiply this value with that documents DocumentRank to arrive at a final weight for a given query, for every document. This weight is then used to sort your results. 

E.g., say the search query is: sunny place The weight of a given document for this given query would be:

$$(𝑇𝐹(sunny) × 𝐼𝐷𝐹(𝑠𝑢𝑛𝑛𝑦)) × (𝑇𝐹(𝑝𝑙𝑎𝑐𝑒) × 𝐼𝐷𝐹(𝑝𝑙𝑎𝑐𝑒)) × 𝐷𝑜𝑐𝑢𝑚𝑒𝑛𝑡𝑅𝑎𝑛$$

