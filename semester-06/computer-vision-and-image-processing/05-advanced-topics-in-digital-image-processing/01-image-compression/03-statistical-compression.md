# 5.1.3 Statistical Compression

## 1. Introduction

**Statistical compression** is an image compression technique that reduces **coding redundancy** by assigning shorter codes to frequently occurring symbols and longer codes to less frequently occurring symbols.

The basic idea is simple:

> **Frequently occurring image values should require fewer bits, while rarely occurring values can use more bits.**

Statistical compression does not necessarily change the actual image information. Instead, it attempts to represent the same information using a **more efficient coding scheme**.

It is therefore primarily associated with **lossless compression**.

## 2. Need for Statistical Compression

In a digital image, some pixel values or symbols occur more frequently than others.

Suppose an image contains four symbols with the following probabilities:

| Symbol | Probability |
| --- | ---: |
| A      |        0.50 |
| B      |        0.25 |
| C      |       0.125 |
| D      |       0.125 |

If every symbol is represented using a fixed-length code, each symbol requires:

$$
\log_2 4=2\text{ bits}
$$

Thus, every occurrence requires 2 bits, regardless of how frequently the symbol occurs.

Statistical compression instead assigns shorter codes to symbols with high probability.

For example:

| Symbol | Probability | Variable-Length Code |
| --- | ---: | --- |
| A      |        0.50 | 0                    |
| B      |        0.25 | 10                   |
| C      |       0.125 | 110                  |
| D      |       0.125 | 111                  |

Now the most frequent symbol **A** requires only 1 bit, while the less frequent symbols require 3 bits.

This reduces the **average number of bits per symbol**.

## 3. Basic Principle

Statistical compression is based on the probability distribution of image symbols.

If $p_i$ is the probability of occurrence of symbol (i), an ideal code length is approximately:

$$
\boxed{l_i \approx -\log_2(p_i)}
$$

Therefore:

* High probability -> small code length
* Low probability -> large code length

For example:

If

$$
p(A)=0.5
$$

then:

$$
-\log_2(0.5)=1
$$

So approximately 1 bit is sufficient for symbol A.

If:

$$
p(B)=0.125
$$

then:

$$
-\log_2(0.125)=3
$$

So approximately 3 bits are required for symbol B.

## 4. Coding Redundancy

Statistical compression primarily removes **coding redundancy**.

### Coding redundancy

Coding redundancy occurs when the representation of image symbols uses more bits than theoretically necessary based on their probabilities.

Consider an image with four possible pixel values:

$$
{A,B,C,D}
$$

A fixed-length representation requires:

$$
\log_2 4=2\text{ bits/symbol}
$$

However, if A occurs much more frequently than the other symbols, assigning 2 bits to every symbol is inefficient.

A variable-length coding scheme can reduce the average number of bits per symbol.

Thus:

$$
\boxed{\text{Statistical Compression} \rightarrow \text{Reduction of Coding Redundancy}}
$$

## 5. Entropy

The theoretical lower bound on the average number of bits required to represent a source is related to its **entropy**.

For a discrete source with symbols (r_1,r_2,\ldots,r_L) and probabilities (p(r_k)), entropy is:

$$
\boxed{
H=-\sum_{k=1}^{L}p(r_k)\log_2 p(r_k)
}
$$

where:

* $H$ = entropy in bits/symbol
* $p(r_k)$ = probability of symbol (r_k)
* $L$ = number of possible symbols

### Interpretation

Entropy represents the **average information content** of the source.

A source with highly predictable symbols has lower entropy.

A source where all symbols are equally likely has higher entropy.

### Example

Consider four symbols:

| Symbol | Probability |
| --- | ---: |
| A      |         0.5 |
| B      |        0.25 |
| C      |       0.125 |
| D      |       0.125 |

The entropy is:

$$
H=
-\left[
0.5\log_2(0.5)
+0.25\log_2(0.25)
+0.125\log_2(0.125)
+0.125\log_2(0.125)
\right]
$$

Since:

$$
\log_2(0.5)=-1
$$

$$
\log_2(0.25)=-2
$$

$$
\log_2(0.125)=-3
$$

we get:

$$
H=0.5(1)+0.25(2)+0.125(3)+0.125(3)
$$

$$
H=0.5+0.5+0.375+0.375
$$

$$
\boxed{H=1.75\text{ bits/symbol}}
$$

A fixed-length code requires 2 bits/symbol, whereas the theoretical entropy is only 1.75 bits/symbol.

Therefore, there is an opportunity for statistical compression.

## 6. Average Code Length

For a variable-length code, the average code length is:

$$
\boxed{
L_{avg}=\sum_{i=1}^{n}p_i l_i
}
$$

where:

* $p_i$ = probability of symbol $i$
* $l_i$ = code length assigned to symbol $i$

For the previous example:

| Symbol | Probability | Code | Length |
| --- | ---: | --- | ---: |
| A      |        0.50 | 0    |      1 |
| B      |        0.25 | 10   |      2 |
| C      |       0.125 | 110  |      3 |
| D      |       0.125 | 111  |      3 |

Therefore:

$$
L_{avg}
=(0.5)(1)+(0.25)(2)+(0.125)(3)+(0.125)(3)
$$

$$
=0.5+0.5+0.375+0.375
$$

$$
\boxed{L_{avg}=1.75\text{ bits/symbol}}
$$

In this particular example, the average code length reaches the entropy value.

## 7. Important Statistical Compression Techniques

The most important statistical coding techniques used in image compression include:

1. **Huffman Coding**
2. **Arithmetic Coding**
3. **Run-Length Encoding (RLE)**

Among these, **Huffman coding** and **arithmetic coding** are classical statistical coding techniques.

## 8. Huffman Coding

### 8.1 Definition

**Huffman coding** is a variable-length, prefix-based coding technique that assigns shorter binary codes to more frequently occurring symbols and longer codes to less frequently occurring symbols.

It is widely used for **lossless data compression**.

### 8.2 Basic Principle

The symbols are arranged according to their probabilities.

The two symbols with the lowest probabilities are repeatedly combined to form a new node until a binary tree is constructed.

The tree is then traversed to obtain the binary codes.

#### General procedure

1. Determine the frequency/probability of each symbol.
2. Arrange symbols in increasing order of probability.
3. Select the two least probable symbols.
4. Combine them.
5. Insert the combined node back into the list.
6. Repeat until only one node remains.
7. Construct the binary tree.
8. Assign 0 and 1 to the branches.
9. Obtain the code for each symbol.

## 8.3 Properties of Huffman Coding

* Variable-length coding.
* Prefix-free code.
* Lossless.
* More frequent symbols get shorter codes.
* Less frequent symbols get longer codes.
* Decoding is unambiguous.

#### Prefix-free property

A Huffman code is designed so that no valid codeword is the prefix of another codeword.

For example:

```text
A -> 0
B -> 10
C -> 110
D -> 111
```

Here, no complete codeword is the beginning of another codeword.

This makes decoding straightforward.

## 9. Arithmetic Coding

### 9.1 Definition

**Arithmetic coding** represents an entire sequence of symbols as a single fractional number in the interval:

$$
[0,1)
$$

Instead of assigning an independent binary codeword to every symbol, arithmetic coding progressively narrows an interval according to the probability of each symbol.

### 9.2 Basic Principle

Suppose the symbols have probabilities:

$$
P(A)=0.5,\quad P(B)=0.3,\quad P(C)=0.2
$$

The interval $[0,1)$ is divided according to these probabilities.

```text
0        0.5       0.8       1.0
|---------|---------|----------|
    A         B          C
```

As symbols are processed, the interval becomes smaller.

The final interval identifies the complete sequence.

### 9.3 Characteristics

* Statistical coding technique.
* Can achieve compression close to the source entropy.
* Can outperform Huffman coding in some cases.
* Supports fractional average bits per symbol.
* More computationally complex than basic Huffman coding.
* Used in several advanced compression standards and systems.

## 10. Run-Length Encoding

### 10.1 Definition

**Run-Length Encoding (RLE)** represents consecutive repetitions of the same symbol by storing the symbol and the number of repetitions.

For example:

```text
AAAAAAABBBBCC
```

can be represented as:

```text
7A 4B 2C
```

Instead of storing 13 symbols individually, the repeated runs are represented compactly.

### 10.2 Suitability

RLE is particularly effective when an image contains:

* Large uniform regions
* Long sequences of identical pixels
* Simple graphics
* Binary images
* Scanned documents

It is less effective for highly detailed natural images where adjacent pixel values change frequently.

## 11. Comparison of Statistical Coding Techniques

| Technique             | Basic Principle                                    | Typical Nature | Main Advantage                              |
| --- | --- | --- | --- |
| **Huffman Coding**    | Variable-length prefix codes                       | Lossless       | Simple and efficient                        |
| **Arithmetic Coding** | Represents a sequence using a probability interval | Lossless       | Can approach entropy closely                |
| **RLE**               | Encodes repeated consecutive symbols               | Lossless       | Very simple and effective for repeated data |

## 12. Statistical Compression Process

A general statistical compression system can be represented as:

```text
Original Image
      ↓
Analyze Symbol Frequencies
      ↓
Estimate Probabilities
      ↓
Construct Efficient Code
      ↓
Encode Image Data
      ↓
Compressed Bitstream
```

During decompression:

```text
Compressed Bitstream
      ↓
Decode Using Coding Model
      ↓
Recover Image Symbols
      ↓
Reconstructed Image
```

For a lossless statistical compression system:

$$
\boxed{
\text{Original Image}
===

\text{Reconstructed Image}
}
$$

## 13. Advantages of Statistical Compression

1. **Lossless compression is possible.**
2. Reduces coding redundancy.
3. Takes advantage of non-uniform symbol probabilities.
4. Can significantly reduce the average number of bits per pixel.
5. Original data can be reconstructed exactly.
6. Useful as a component of more sophisticated image compression systems.
7. Huffman coding is relatively simple to implement.

## 14. Limitations

1. Compression performance depends heavily on the probability distribution of image symbols.
2. If all symbols are equally probable, statistical coding provides limited improvement.
3. A probability model or frequency table may need to be stored or transmitted.
4. Some statistical methods require greater computational complexity.
5. Statistical compression alone may not achieve very high compression for complex natural images.
6. RLE performs poorly when long runs of identical values are uncommon.

## 15. Statistical Compression vs. Quantization

These two concepts should not be confused.

| Statistical Compression          | Quantization                                          |
| --- | --- |
| Mainly removes coding redundancy | Reduces precision of data                             |
| Can be lossless                  | Generally lossy                                       |
| Uses probability/statistics      | Maps values to fewer representative levels            |
| Examples: Huffman, Arithmetic    | Used in JPEG and other lossy methods                  |
| Original data can be preserved   | Original values generally cannot be recovered exactly |

A common compression system may actually use **both**.

For example:

$$
\text{Image}
\rightarrow
\text{Transform}
\rightarrow
\text{Quantization}
\rightarrow
\text{Huffman Coding}
\rightarrow
\text{Compressed Data}
$$

Here, **quantization reduces the amount of information**, while **Huffman coding efficiently represents the remaining information**.

## Key Concepts

### Coding Redundancy

Extra bits used because symbols are not encoded according to their probabilities.

### Entropy

The theoretical minimum average number of bits per symbol required to represent a source:

$$
\boxed{
H=-\sum p_i\log_2p_i
}
$$

### Average Code Length

$$
\boxed{
L_{avg}=\sum p_i l_i
}
$$

### Statistical Compression

Reduction of coding redundancy by exploiting the statistical properties of image data.

### Major Methods

$$
\boxed{\text{Huffman Coding, Arithmetic Coding, RLE}}
$$

## Summary

**Statistical compression** reduces image data by exploiting the statistical distribution of image symbols. It primarily removes **coding redundancy**.

The fundamental principle is:

> **Assign shorter codes to frequently occurring symbols and longer codes to less frequently occurring symbols.**

The theoretical information content of an image source is measured using **entropy**:

$$
H=-\sum p_i\log_2p_i
$$

The average length of a variable-length code is:

$$
L_{avg}=\sum p_i l_i
$$

Important statistical compression techniques include:

* **Huffman Coding** : creates an optimal prefix-free variable-length code.
* **Arithmetic Coding** : represents an entire symbol sequence using a progressively narrowed numerical interval.
* **Run-Length Encoding** : represents consecutive repetitions using a symbol and its run length.

### One-line definition

> **Statistical image compression is a lossless compression approach that exploits the statistical properties of image data to reduce coding redundancy by assigning shorter codes to more probable symbols and longer codes to less probable symbols.**
