#misc
# Morning Session

Funded by Glasgow city innovation district.
## Structure of LLMs
- Break words into semantics, a word is on averge 2.5 tokens
- Bi Directional Model, every token can interact with every other token
	- Better for ..
- Each token is influenced by the one before it.
	- Better for text gen.

## Training
- Pre-training
	- Give it a token the model will try to predict it.
	
- Fine Tuning (optional)
	- Training for a specific domain, give claude code or a medical language model medical questions.
	
- Reinforcement learning
	- Increase reward based off human feedback.
	- RLHF - Reinforcement Learning with Human Feedback
	- If only had training then it would almost just try to predict what you're saying
	
- Retrieval Augmented …

## Hype vs. Reality
- Hallucinations can happen
- Don't plan your diet based off chatGPT.
- Like Thijs mentioned, think about Geminis AI Suggestions, "Can you eat rocks?" it then replies with "You can eat" and is like dang I'm past the point of return, then it'll just continue on.

## The (Not so Hidden) Cost
- LLMs are very expensive to train,
- Remember how the CEO of chatGPT was saying nobody could beat him since it would cost hundreds of millions to train something as large as GPTo4.
- Deepseek was still 5mill.

## Retrieval Augmented Generation (RAG)
- Separate your dataset into chunks and load it depending on the qustion?

## Fine-Tuning
- We can fine tune it ourself, a lot of these are open source so we can download the base model and fine tune it ourself to match our needs.
- This has been used across multiple companies, you've heard from Morgan Stanley and Barclays about them training their local models on business logic.
- We can do this.

## Prompt Engineering
- Response is equal to the quality of the prompt.
- AI Agents have demonstrated a surprising ability known as in context learning. Typical AI models can only perform tasks on which they were specifically trained, but if an LLMs prompt is correctly crafted it can generalise previously learned tasks to provide quality solutions

## Examples

### Financial News Classification
- Uses Hugging Face, imagine a GitHub for open source models. Look here to see if a model exists.
- You could see forking here linking into Fine Training.
- Classify financial news headings to specific topics.
- Lots of text data we could do some aggregation on our current data and group, maybe flagging harmful posts.
- Could come into calendar, mail integrations.

First we need to load in the dataset:

```python
data = load_dataset('yada yada')

# This will access the train side of the dictionary, it's suggested there's a split of 80% train data and 20% validation data. It'll return the first training dataset.

# {'text': 'data data data', 'label': 0}
data['train'][0]
```

Then we need to import a few things to help us out:

```python
import torch
from torch.utils.data import Dataset
from transformers
```

In this we are using the [bert](https://en.wikipedia.org/wiki/BERT_(language_model)) package, no idea what it means take a gander later.

For training the model, we use `AdamW`, this is based off the `Adam` optimiser that came out in 2014 but there was a bug that ended up making the making the optimiser less optimal? The W stands for Weight which is the bug that was fixed.

```python
from torch import nn

LIMITING_RATE = 5e-5

# If weight decay is too low it can increase hallucinations, this essentially reduces the randomness.
WEIGHT_DECAY = 0.01

opt = torch.optim.AdamW(model.parameters(), LEARNING_RATE, WEIGHT_DECAY)
criterion = nn.CrossEntropyLoss()
```

For training we loop through every training item and every batch, first off we set the gradient to zero, get logits then we clip the training to make sure it doesn't get out of hand, and apply the optimser, validate data and store prediction and labels then we can print results.

After running multiple rounds of testing we can see the accuracy going up but if you overfit this accuracy can go down.

After every round of testing we save a checkpoint.

There's ton more we can do to increase efficiency:
- Hyper-parameter tuning
- Data augmentation
- Label smoothing (or some other method of regularisation)

# Afternoon Session

## Colours

- The task with colours was to extract the colours based on the role they play.
- Takes a list of colours classifies it based on 5 categories, this allows them to split it into primary, secondary etc.

### Randrom Transforms and LAB

LAB colours space is specifically built for human perception - <https://en.wikipedia.org/wiki/CIELAB_color_space>.


## Logos

- Given a company get the logo.
- Two approaches both aren't perfect:
	- OCR with Fuzzy. - <https://cloud.google.com/use-cases/ocr>
		- Rates each text based on a set of data, say we know the name of the company and the accuracy would be higher.
		- This fails when a logo doesn't have any text.
		- 80% accuracy without any extra keys.
	
	- Manually gathered data.
		- Trained a model to pick out logos based on vision, what looks most like a logo.
		- 64% accuracy.

- Discussion of a hybrid model which would implement both.

## Fonts

- Fonts are complicated 
- Representation Learning to learn a vector graphic of a font.
- They have a dataset setup with free and paid fonts
- The goal of the model is to fetch similar free fonts. Vector Search.

### [CLIP](https://openai.com/index/clip/)

- Rather than using image recognition they used text comparison. We compare based on the text description.

