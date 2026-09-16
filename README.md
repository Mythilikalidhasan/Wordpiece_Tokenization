# WordPiece Tokenizer from Scratch

A simple implementation of the **WordPiece Tokenization algorithm** using Python. This project demonstrates how WordPiece builds a vocabulary by calculating token frequencies, evaluating adjacent token pairs, selecting the highest-scoring pair, merging tokens, and converting words into token IDs.

## Project Overview

WordPiece is a subword tokenization algorithm commonly used in Natural Language Processing (NLP).

Instead of treating every complete word as a single token, WordPiece can divide words into smaller subword units. This allows NLP models to handle words that were not directly present in the training vocabulary.

This project implements the basic WordPiece process from scratch using a small training dataset.

## How It Works

The implementation follows these steps:

```text
Training Words
      ↓
Initial Word Splits
      ↓
Token Frequency Calculation
      ↓
Pair Frequency Calculation
      ↓
WordPiece Score Calculation
      ↓
Select Best Pair
      ↓
Merge Tokens
      ↓
Updated Vocabulary
      ↓
Tokenize New Words
      ↓
Convert Tokens to IDs
```

## Training Data

The example uses three words:

```python
words = {
    "hug": 2,
    "hugs": 1,
    "pug": 1
}
```

The initial tokenization is:

```text
hug  → h ##u ##g
hugs → h ##u ##g ##s
pug  → p ##u ##g
```

The `##` prefix represents a subword that occurs after the first token of a word.

For example:

```text
hugs → h ##u ##g ##s
```

Here:

* `h` is the first token.
* `##u` is a continuation token.
* `##g` is a continuation token.
* `##s` is a continuation token.

## WordPiece Scoring

The program counts:

1. Individual token frequencies
2. Adjacent token-pair frequencies

The WordPiece score used in this implementation is:

```text
Score(pair) =
Pair Frequency /
(Token Frequency of First Token × Token Frequency of Second Token)
```

The pair with the highest score is selected for merging.

## Token Merging

After calculating the scores, the program identifies the best token pair and merges it into a new token.

For example:

```text
h + ##u → hu
```

The new token is then added to the vocabulary.

The process can be repeated to build a larger subword vocabulary.

## Tokenization

The tokenizer uses a longest-match approach.

For example, with the learned vocabulary, the word:

```text
hugs
```

can be tokenized as:

```text
hug ##s
```

The tokenizer checks the longest possible token first and continues until the complete word is processed.

## Token IDs

After tokenization, tokens can be converted into numerical IDs.

Example:

```text
Tokens:
["hug", "##s"]

Token IDs:
[7, 5]
```

These numerical IDs are what NLP models can use as input instead of raw text.

## Handling Unknown Words

If the tokenizer cannot find a valid token for part of a word, it returns:

```text
[UNK]
```

For example:

```text
bum → [UNK]
```

`[UNK]` means **Unknown Token**.

## Technologies Used

* Python
* JupyterLab
* Collections module (`Counter`)

## Project Structure

```text
WordPiece-Tokenizer/
│
├── wordpiece_tokenizer.ipynb
└── README.md
```

## How to Run

### 1. Clone the repository

```bash
git clone <your-repository-url>
```

### 2. Open the project

```bash
cd WordPiece-Tokenizer
```

### 3. Start JupyterLab

```bash
jupyter lab
```

### 4. Open the notebook

Open:

```text
wordpiece_tokenizer.ipynb
```

Run the cells to see the complete WordPiece tokenization process.

## Example Output

```text
Initial Vocabulary:
['h', 'p', '##u', '##g', '##s']

Training Words:
{'hug': 2, 'hugs': 1, 'pug': 1}

Best Pair:
('h', '##u')

New Token:
hu

Updated Vocabulary:
['h', 'p', '##u', '##g', '##s', 'hu']
```

The tokenizer can then process:

```text
hugs → hug ##s
```

and convert the tokens into:

```text
[7, 5]
```

## Learning Objectives

This project helps demonstrate:

* How subword tokenization works
* How WordPiece builds a vocabulary
* Token frequency calculation
* Pair frequency calculation
* WordPiece scoring
* Token merging
* Longest-match tokenization
* Token-to-ID conversion
* Handling unknown words

## Limitations

This is an educational implementation of WordPiece and is intentionally simplified.

Production WordPiece tokenizers include additional functionality such as:

* Larger vocabularies
* More training iterations
* Special tokens
* Unicode and normalization handling
* Efficient tokenization
* Model-specific preprocessing

The purpose of this project is to understand the core algorithm rather than reproduce a production tokenizer.

## License

This project is intended for educational and learning purposes.
