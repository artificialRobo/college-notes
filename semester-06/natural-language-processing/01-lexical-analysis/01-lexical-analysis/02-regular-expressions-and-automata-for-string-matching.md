# Regular Expressions and Automata for String Matching

## Introduction

**Regular Expressions (Regex)** and **Finite Automata** are the fundamental computational tools used in **lexical analysis** and **string matching**. They enable a lexical analyzer to recognize patterns such as words, numbers, dates, email addresses, identifiers, and other lexical units in text.

In NLP, regular expressions are used to define patterns, while finite automata provide an efficient mechanism to recognize those patterns automatically.

> **Definition:** A regular expression is a formal language notation used to describe a set of strings, and a finite automaton is a mathematical model used to recognize strings that belong to the language defined by the regular expression.

## String Matching

### Definition

**String matching** is the process of determining whether a given text contains a specific pattern or whether the entire text matches a predefined pattern.

For example:

Text:

```text
Natural Language Processing
```

Pattern:

```text
Language
```

The pattern exists in the text; therefore, the string matching operation succeeds.

## Regular Expressions (Regex)

### Definition

A **regular expression** is a sequence of characters that specifies a search pattern.

Regex is used for:

- tokenization,
- lexical analysis,
- information extraction,
- validation,
- text preprocessing,
- pattern matching.

## Basic Components of Regular Expressions

### Literal Characters

A literal character matches itself.

Examples:

| Regex | Matches |
| --- | --- |
| `a` | `a` |
| `cat` | `cat` |
| `NLP` | `NLP` |

### Character Classes

A character class matches one character from a set.

| Regex | Meaning |
| --- | --- |
| `[abc]` | `a`, `b`, or `c` |
| `[A-Z]` | Any uppercase letter |
| `[a-z]` | Any lowercase letter |
| `[0-9]` | Any digit |
| `[A-Za-z]` | Any English letter |

Example:

Regex:

```text
[0-9]
```

Matches:

```text
3
7
9
```

### Quantifiers

Quantifiers specify the number of repetitions.

| Symbol | Meaning |
| --- | --- |
| `*` | Zero or more occurrences |
| `+` | One or more occurrences |
| `?` | Zero or one occurrence |
| `{n}` | Exactly `n` occurrences |
| `{n,m}` | Between `n` and `m` occurrences |

Examples:

```text
a*
```

Matches:

```text
(empty)
a
aa
aaa
```

```text
a+
```

Matches:

```text
a
aa
aaa
```

### Wildcard Character

The dot (`.`) matches any single character.

Example:

```text
c.t
```

Matches:

```text
cat
cot
cut
```

### Anchors

Anchors specify positions.

| Symbol | Meaning |
| --- | --- |
| `^` | Beginning of string |
| `$` | End of string |

Examples:

```text
^NLP
```

Matches:

```text
NLP is useful
```

```text
ing$
```

Matches:

```text
processing
learning
```

## Common Regular Expression Patterns

### Word

```text
[A-Za-z]+
```

Matches:

```text
Natural
language
NLP
```

### Integer Number

```text
[0-9]+
```

Matches:

```text
1
25
2026
```

### Decimal Number

```text
[0-9]+\.[0-9]+
```

Matches:

```text
3.14
10.5
0.75
```

### Email Address (Simplified)

```text
[A-Za-z0-9._]+@[A-Za-z]+\.[A-Za-z]+
```

Matches:

```text
user@gmail.com
abc123@yahoo.com
```

### Date Format

```text
[0-9]{2}/[0-9]{2}/[0-9]{4}
```

Matches:

```text
12/08/2026
```

## Applications of Regular Expressions in NLP

Regex is extensively used in lexical processing.

### Tokenization

Sentence:

```text
Ravi bought 3 books.
```

Regex:

```text
[A-Za-z]+|[0-9]+|[.]
```

Tokens extracted:

```text
Ravi
bought
3
books
.
```

### Named Entity Detection

Regex can identify:

- phone numbers,
- email addresses,
- dates,
- URLs,
- currency amounts.

### Text Cleaning

Examples:

Remove punctuation:

```text
[^A-Za-z0-9 ]
```

Normalize spaces:

```text
\s+
```

## Limitations of Regular Expressions

Regular expressions are powerful but have limitations.

They cannot effectively handle:

- nested structures,
- long-distance dependencies,
- complex grammatical relationships,
- recursive patterns.

Example:

```text
The book that Ravi said Mohan bought is interesting.
```

Regex cannot reliably determine grammatical structure.

## Automata Theory

### Definition

An **automaton** is an abstract computational machine that processes an input string symbol by symbol and decides whether the string belongs to a language.

Automata provide the implementation mechanism for regular expressions.

## Finite Automata

A **Finite Automaton (FA)** consists of:

- a finite set of states,
- an input alphabet,
- transition rules,
- a start state,
- one or more accepting states.

### Components of a Finite Automaton

A finite automaton is represented by the 5-tuple:

```text
(Q, Σ, δ, q0, F)
```

Where:

- **Q** = finite set of states,
- **Σ** = input alphabet,
- **δ** = transition function,
- **q0** = start state,
- **F** = set of accepting states.

## Deterministic Finite Automaton (DFA)

A **Deterministic Finite Automaton (DFA)** has exactly **one transition** for each state and input symbol.

### Example: Recognizing the Word “cat”

States:

```text
q0 --c--> q1 --a--> q2 --t--> q3
```

Here:

- `q0` = start state,
- `q3` = accepting state.

Input:

```text
cat
```

Processing:

| Symbol | Current State | Next State |
| --- | --- | --- |
| `c` | `q0` | `q1` |
| `a` | `q1` | `q2` |
| `t` | `q2` | `q3` |

Since `q3` is an accepting state, the string is accepted.

## Non-Deterministic Finite Automaton (NFA)

A **Non-Deterministic Finite Automaton (NFA)** may have:

- multiple transitions for the same input,
- epsilon (`ε`) transitions,
- multiple possible computation paths.

Example:

```text
q0
 |\
a a
 |  \
q1  q2
```

NFAs are often easier to construct from regular expressions.

## Regular Expressions and Finite Automata

Every regular expression can be converted into an equivalent finite automaton.

Example:

Regular expression:

```text
a*b
```

Accepted strings:

```text
b
ab
aab
aaab
```

Equivalent automaton:

```text
      a
   ↺
q0 -----> q0
 |
 b
 |
 v
q1
```

`q1` is the accepting state.

## DFA Construction Example

Construct a DFA for:

```text
ab*
```

Accepted strings:

```text
a
ab
abb
abbb
```

State diagram:

```text
q0 --a--> q1 --b--> q1
```

Transition table:

| State | a | b |
| --- | --- | --- |
| `q0` | `q1` | Dead |
| `q1` | Dead | `q1` |

## String Matching Using DFA

Suppose we want to find the pattern:

```text
NLP
```

DFA:

```text
q0 --N--> q1 --L--> q2 --P--> q3
```

Input:

```text
I love NLP techniques.
```

The automaton scans each character.

When it reaches `q3`, the pattern has been found.

This process is extremely efficient because each input character is processed only once.

## Comparison: Regex vs Automata

| Regular Expressions | Finite Automata |
| --- | --- |
| Pattern specification | Pattern recognition |
| Declarative | Computational |
| Easy for humans | Efficient for machines |
| Used to define lexical patterns | Used to implement lexical analyzers |

## Advantages of Automata-Based String Matching

- Linear-time processing,
- Efficient memory usage,
- Suitable for large text corpora,
- Easy implementation in lexical analyzers,
- Foundation of compiler and NLP tokenizers.

## Applications in NLP

Finite automata are used in:

- lexical analyzers,
- tokenizers,
- spell checkers,
- morphological analyzers,
- search engines,
- information retrieval systems,
- pattern matching systems.

## Key Points

- **Regular expressions define patterns**, while **finite automata recognize patterns**.
- Regex operators include **concatenation, union (`|`), and Kleene star (`*`)**.
- **DFA has one transition per symbol**, whereas **NFA may have multiple transitions**.
- Every regular expression can be converted into an equivalent finite automaton.
- Lexical analyzers commonly use **regex and finite automata** for efficient token recognition.

## Summary

**Regular expressions** are formal pattern descriptions used for string matching and lexical analysis. They specify sets of valid strings using operators such as concatenation, union, and Kleene star. **Finite automata** are abstract machines that recognize these patterns efficiently. A **DFA** has deterministic transitions, while an **NFA** allows multiple transitions for the same input. In NLP, regular expressions are used for tokenization and pattern extraction, whereas finite automata implement lexical analyzers and string matching algorithms efficiently.
