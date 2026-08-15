# Introduction to Lexical Analysis

## Introduction

**Lexical analysis** is the **first stage of Natural Language Processing (NLP)** in which a stream of input text is converted into a sequence of meaningful units called **tokens**. The lexical analyzer identifies words, numbers, punctuation marks, symbols, and other lexical elements from raw text.

In simple terms, lexical analysis breaks a sentence into smaller components that can be processed by later NLP stages such as morphological analysis, syntax analysis, and semantic analysis.

> **Definition:** Lexical analysis is the process of transforming raw text into a structured sequence of lexical units (tokens) while optionally removing irrelevant characters and normalizing word forms.

## Objectives of Lexical Analysis

The main objectives of lexical analysis are:

- **Tokenization** – splitting text into words and symbols.
- **Normalization** – converting different word forms into a standard form.
- **Identification of lexical units** – recognizing words, numbers, punctuation, and symbols.
- **Preparation for further NLP processing** – providing clean input for morphological analysis, POS tagging, and syntax analysis.

## Role of Lexical Analysis in NLP

Lexical analysis acts as the **interface between raw text and linguistic processing**.

### NLP Processing Pipeline

```text
Raw Text
     │
     v
Lexical Analysis
     │
     v
Morphological Analysis
     │
     v
Syntax Analysis
     │
     v
Semantic Analysis
```

Without lexical analysis, later stages cannot correctly interpret the structure and meaning of text.

## Basic Terminology

| Term | Meaning |
| --- | --- |
| **Lexeme** | The basic lexical unit or dictionary form of a word. |
| **Token** | An occurrence of a lexeme in text. |
| **Vocabulary** | The set of all unique words in a language or corpus. |
| **Corpus** | A large collection of text documents. |

### Example

Sentence:

> The students are studying NLP.

Lexical analysis produces:

```text
[The] [students] [are] [studying] [NLP] [.]
```

Here:

- **students** is a **token**.
- **student** is the **lexeme** (dictionary form).

## Tokenization

Tokenization is the **core operation of lexical analysis**.

### Example 1

Input:

> Natural Language Processing is interesting.

Tokens:

```text
Natural
Language
Processing
is
interesting
.
```

### Example 2

Input:

> I paid ₹500.

Tokens:

```text
I
paid
₹
500
.
```

Depending on the application, the currency symbol may be treated as a separate token.

## Steps Involved in Lexical Analysis

### 1. Input Reading

The text is read from a document, webpage, speech transcript, or another source.

### 2. Text Segmentation

The text is divided into **sentences** and **words**.

### 3. Token Generation

Words, numbers, punctuation marks, and symbols are extracted.

### 4. Normalization (Optional)

Common normalization operations include:

- converting to lowercase,
- removing extra spaces,
- handling punctuation,
- expanding contractions.

Examples:

```text
Don't  -> do not
NLP    -> nlp
```

### 5. Output Generation

A sequence of tokens is passed to subsequent NLP modules.

## Example of Lexical Analysis

Consider the sentence:

> Ravi bought 3 books from Patna.

### Step 1: Raw Text

```text
Ravi bought 3 books from Patna.
```

### Step 2: Tokenization

```text
Ravi
bought
3
books
from
Patna
.
```

### Step 3: Token Classification

| Token | Category |
| --- | --- |
| Ravi | Proper noun |
| bought | Verb |
| 3 | Number |
| books | Noun |
| from | Preposition |
| Patna | Proper noun |
| . | Punctuation |

This classified token stream becomes the input for **POS tagging** and **morphological analysis**.

## Challenges in Lexical Analysis

Lexical analysis is not always straightforward.

### 1. Ambiguity

A word may have multiple interpretations.

Example:

```text
book
```

- **Noun:** This is a book.
- **Verb:** Book a ticket.

### 2. Compound Words

Examples:

- railway station
- state-of-the-art

The tokenizer must determine whether these are single lexical units or multiple tokens.

### 3. Contractions

Examples:

```text
I'm    -> I am
can't  -> can not
```

### 4. Numbers and Symbols

Examples:

- 10,000
- ₹500
- 12.5%

### 5. URLs and Email Addresses

Examples:

- https://example.com
- user@example.com

These often require special tokenization rules.

## Lexical Analysis in Indian Languages

Indian languages present additional challenges because they are **morphologically rich** and often contain complex word formations.

### Example (Hindi)

Sentence:

> लड़कों ने किताबें पढ़ीं।

Possible tokens:

```text
लड़कों
ने
किताबें
पढ़ीं
```

The word **लड़कों** contains information about:

- root word: **लड़का**
- plural
- oblique case

Therefore, lexical analysis in Indian languages is closely connected with **morphological analysis**.

## Lexical Analyzer

A **lexical analyzer (lexer)** is a software component that performs lexical analysis.

### Functions of a Lexical Analyzer

- scans input text,
- identifies tokens,
- ignores irrelevant characters,
- reports lexical errors,
- supplies tokens to the next processing stage.

### General Workflow

```text
Input Text
     │
     v
Lexical Analyzer
     │
     v
Token Stream
```

## Applications of Lexical Analysis

Lexical analysis is used in almost every NLP application.

- Machine translation
- Speech recognition
- Text summarization
- Question answering systems
- Information retrieval
- Spell checking
- Sentiment analysis
- Chatbots and virtual assistants

For example, a search engine first tokenizes a user query before searching documents.

## Advantages of Lexical Analysis

- Reduces text complexity.
- Produces structured input.
- Improves processing efficiency.
- Enables morphological and syntactic analysis.
- Supports language-independent preprocessing.

## Limitations of Lexical Analysis

- Cannot determine complete sentence meaning.
- Faces ambiguity in word boundaries.
- Requires language-specific tokenization rules.
- Richly inflected languages need deeper morphological processing.

## Key Points

- Lexical analysis is the **first stage of NLP**.
- It converts **raw text into tokens**.
- The main operation is **tokenization**.
- Tokens are used for **morphological analysis, POS tagging, and parsing**.
- Lexical analysis is especially important for **Indian languages** due to their rich morphology.
- A lexical analyzer scans text and generates a **token stream** for further processing.

## Summary

**Lexical analysis** is the first phase of NLP that converts raw text into a sequence of tokens. It performs tokenization, normalization, and lexical unit identification. For example, the sentence *“Ravi bought books.”* is converted into the tokens **Ravi**, **bought**, **books**, and **.**. The output of lexical analysis is used by later stages such as morphological analysis, POS tagging, and syntactic parsing. Lexical analysis improves text processing efficiency and is essential for applications such as machine translation, information retrieval, and speech processing.
