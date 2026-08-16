# 5.1.6 Quantizing Compression

## 1. Introduction

**Quantizing compression** is an image compression technique that reduces the amount of image information by **reducing the number of distinct values used to represent image data**.

The basic idea is to map a large number of possible input values into a smaller number of representative values.

For example, instead of representing grayscale intensity using all 256 levels:

$$
0,1,2,\ldots,255
$$

we may represent the image using only 16 levels.

This reduces the amount of information required to store the image.

### Core idea

> **Quantizing compression reduces data by representing a range of similar values with a single representative value.**

Unlike statistical coding, which mainly changes the way information is represented, quantization can **discard information**. Therefore, it is most commonly associated with **lossy image compression**.

## 2. Need for Quantizing Compression

A grayscale image with 8-bit representation has:

$$
2^8=256
$$

possible intensity levels.

If the image is represented using only 4 bits per pixel:

$$
2^4=16
$$

intensity levels are available.

Thus, the number of bits per pixel is reduced from:

$$
8\rightarrow4
$$

which significantly reduces the amount of image data.

The trade-off is that several original intensity values must be represented by the same quantized value.

Therefore:

$$
\boxed{
\text{Reduced Precision}
\rightarrow
\text{Reduced Data}
\rightarrow
\text{Possible Quality Loss}
}
$$

## 3. Definition of Quantization

**Quantization** is the process of mapping a continuous or large set of discrete values into a smaller set of discrete representative values.

For image processing, this means mapping the original pixel intensity (x) to a quantized value (Q(x)).

$$
\boxed{
x\rightarrow Q(x)
}
$$

For example:

$$
\begin{aligned}
0-15 &\rightarrow 8\
16-31 &\rightarrow 24\
32-47 &\rightarrow 40\
\vdots
\end{aligned}
$$

Several original intensity values are therefore represented by one value.

## 4. Quantization in Image Compression

A simplified image compression system can be represented as:

```text id="8ajybs"
Original Image
      ↓
Transformation / Processing
      ↓
Quantization
      ↓
Entropy Coding
      ↓
Compressed Image
```

Quantization is often followed by **statistical or entropy coding**.

For example, a JPEG-style compression system can be simplified as:

$$
\boxed{
\text{Image}
\rightarrow
\text{DCT}
\rightarrow
\text{Quantization}
\rightarrow
\text{Huffman Coding}
\rightarrow
\text{Compressed Data}
}
$$

Here:

* **DCT** transforms the image into frequency coefficients.
* **Quantization** reduces the precision of those coefficients.
* **Huffman coding** efficiently represents the remaining values.

## 5. Types of Quantization

Quantization can broadly be classified into:

1. **Scalar Quantization**
2. **Vector Quantization**

These are important concepts in image and signal compression.

## 6. Scalar Quantization

### 6.1 Definition

In **scalar quantization**, each input value is quantized independently.

For an image, each pixel or individual transform coefficient can be mapped to one of a finite number of output levels.

$$
\boxed{
x\rightarrow Q(x)
}
$$

For example:

```text id="q5x4qm"
Input intensity       Quantized intensity

0 – 31       =>             16
32 – 63      =>             48
64 – 95      =>             80
96 – 127     =>            112
128 – 159    =>            144
160 – 191    =>            176
192 – 223    =>            208
224 – 255    =>            240
```

Here, 256 possible intensity values are represented by only 8 output levels.

## 7. Uniform Quantization

In **uniform quantization**, the quantization intervals have equal width.

Suppose the input range is:

$$
0\leq x\leq255
$$

and we want (L=8) quantization levels.

The approximate interval size is:

$$
\Delta=\frac{256}{8}=32
$$

Thus, the intensity range can be divided into eight equal intervals.

$$
[0,31],[32,63],\ldots,[224,255]
$$

Each interval is represented by a single output value.

### Advantages

* Simple implementation.
* Low computational complexity.
* Easy to analyze.
* Suitable when the input values are relatively uniformly distributed.

### Limitation

It may not be efficient when some intensity ranges occur much more frequently than others.

## 8. Non-Uniform Quantization

In **non-uniform quantization**, the quantization intervals are not equal.

More quantization levels can be allocated to regions where image values occur frequently or where greater accuracy is important.

For example:

```text id="x2c0yr"
Input Range

0----10--20----50---------100----------------255
|     |   |     |            |                  |
  small intervals       larger intervals
```

This allows the quantizer to represent important regions more accurately.

### Advantages

* Better adaptation to the statistical characteristics of the image.
* Can provide better quality for the same number of quantization levels.
* More efficient for non-uniform data distributions.

### Disadvantage

* More complex than uniform quantization.

## 9. Vector Quantization

### 9.1 Definition

**Vector Quantization (VQ)** processes a group of values together rather than quantizing each value independently.

For an image, a small block of pixels can be treated as a vector.

For example, a (2\times2) block:

$$
\begin{bmatrix}
100 & 102\
101 & 103
\end{bmatrix}
$$

can be represented as a vector:

$$
[100,102,101,103]
$$

The vector is then compared with a set of predefined representative vectors called a **codebook**.

The index of the closest codebook vector is stored.

## 10. Codebook in Vector Quantization

A **codebook** contains a collection of representative vectors.

For example:

$$
C={C_1,C_2,C_3,\ldots,C_K}
$$

For an input vector (X), the encoder finds the codebook vector that is closest to (X).

$$
\boxed{
X\rightarrow C_i
}
$$

Instead of storing the entire vector, only the index (i) may be stored.

### Example

Suppose:

$$
X=[100,102,101,103]
$$

and the closest codebook vector is:

$$
C_7=[99,101,102,103]
$$

Instead of storing all four values, the encoder stores:

$$
\boxed{7}
$$

The decoder uses codebook entry 7 to reconstruct the block.

## 11. Quantization Error

Because multiple input values can be represented by the same output value, quantization introduces an error.

The quantization error can be expressed as:

$$
\boxed{
e=x-Q(x)
}
$$

where:

* $x$ = original value
* $Q(x)$ = quantized value
* $e$ = quantization error

### Example

Suppose:

$$
x=117
$$

and the quantizer represents it as:

$$
Q(x)=120
$$

Then:

$$
e=117-120=-3
$$

Thus, the quantization error is:

$$
\boxed{-3}
$$

The magnitude of the error is:

$$
|e|=3
$$

## 12. Quantization Error in Uniform Quantization

For an ideal uniform quantizer with step size (\Delta), the quantization error is generally bounded approximately by:

$$
-\frac{\Delta}{2}\leq e\leq\frac{\Delta}{2}
$$

Therefore:

$$
\boxed{
|e|\leq\frac{\Delta}{2}
}
$$

This means that reducing the quantization step size generally reduces the maximum quantization error.

However, smaller quantization steps require more quantization levels and therefore reduce the amount of compression.

## 13. Compression–Quality Trade-off

Quantization creates an important trade-off between **compression ratio and image quality**.

### More quantization levels

$$
\text{More Levels}
\rightarrow
\text{Higher Precision}
\rightarrow
\text{Better Quality}
\rightarrow
\text{Less Compression}
$$

### Fewer quantization levels

$$
\text{Fewer Levels}
\rightarrow
\text{Lower Precision}
\rightarrow
\text{Lower Quality}
\rightarrow
\text{Higher Compression}
$$

Therefore:

$$
\boxed{
\text{Compression Ratio}
\leftrightarrow
\text{Image Quality}
}
$$

## 14. Example of Quantization

Suppose a grayscale image has intensity values:

$$
20,;23,;27,;52,;55,;58
$$

Suppose we use the following quantization ranges:

| Original Range | Quantized Value |
| --- | ---: |
| 0–31           |              24 |
| 32–63          |              56 |

The image becomes:

$$
24,;24,;24,;56,;56,;56
$$

The original six different values have been represented using only two levels.

This reduces the number of distinct values that need to be encoded.

However, the exact original values cannot be recovered from the quantized values.

## 15. Quantization and Lossy Compression

Quantization is generally the **lossy stage** of a compression system.

Before quantization:

$$
x=117
$$

After quantization:

$$
Q(x)=120
$$

The original value 117 is no longer available.

Therefore, the inverse operation cannot recover 117 exactly.

The decoder can only reconstruct the representative value:

$$
\hat{x}=120
$$

Thus:

$$
\boxed{
\text{Quantization}
\rightarrow
\text{Information Loss}
}
$$

This is why quantization is generally associated with lossy compression.

## 16. Quantization in JPEG

Quantization plays a particularly important role in **JPEG image compression**.

A simplified JPEG process is:

$$
\boxed{
\text{Image}
\rightarrow
\text{8×8 Blocks}
\rightarrow
\text{DCT}
\rightarrow
\text{Quantization}
\rightarrow
\text{Zig-Zag Ordering}
\rightarrow
\text{Entropy Coding}
}
$$

The DCT produces frequency coefficients.

Quantization then divides these coefficients by values from a **quantization matrix** and rounds the results.

Conceptually:

$$
\boxed{
Q_{ij}=
\operatorname{round}
\left(
\frac{D_{ij}}{M_{ij}}
\right)
}
$$

where:

* $D_{ij}$ = DCT coefficient
* $M_{ij}$ = quantization matrix value
* $Q_{ij}$ = quantized coefficient

Many high-frequency coefficients may become zero after quantization.

These zeros can then be represented efficiently using run-length and entropy coding.

## 17. Why Quantization Produces High Compression

After quantization, many values become:

* Zero
* Small integers
* Repeated values

This creates a distribution that is easier to compress using statistical coding.

For example:

Before quantization:

$$
15.7,;-8.3,;4.8,;-2.1,;1.2,;0.9,\ldots
$$

After quantization:

$$
16,;-8,;5,;-2,;1,;1,;0,;0,;0,\ldots
$$

The resulting sequence contains many zeros and repeated/small values.

An entropy encoder can compress this sequence efficiently.

Thus, quantization and statistical compression often work together.

## 18. Quantization vs. Statistical Compression

These two techniques perform different functions.

| Feature | Quantization | Statistical Compression |
| --- | --- | --- |
| Main purpose      | Reduce precision/data values    | Reduce coding redundancy           |
| Information loss  | Usually yes                     | Usually no                         |
| Basic operation   | Map many values to fewer values | Assign efficient codes             |
| Main parameter    | Quantization levels/step size   | Symbol probabilities               |
| Examples          | Scalar VQ, JPEG quantization    | Huffman, Arithmetic coding         |
| Effect on quality | Can reduce image quality        | Does not inherently reduce quality |
| Typical role      | Main lossy stage                | Final coding stage                 |

### Important relationship

A practical lossy compression system may use:

$$
\boxed{
\text{Quantization}
\rightarrow
\text{Statistical Coding}
}
$$

Quantization reduces the information, and statistical coding compresses the resulting data efficiently.

## 19. Advantages of Quantizing Compression

1. **Provides high compression ratios.**
2. Reduces the number of values that need to be represented.
3. Can significantly reduce storage requirements.
4. Can reduce transmission bandwidth.
5. Simple quantizers can be computationally efficient.
6. Can be adapted to image characteristics using non-uniform quantization.
7. Works effectively with transform coding.
8. Plays a major role in practical lossy image compression standards.

## 20. Limitations

1. **Information loss is generally irreversible.**
2. Excessive quantization causes visible image degradation.
3. Fine image details may be lost.
4. Edges can become less sharp.
5. Compression artifacts may appear.
6. Choosing an inappropriate quantization level can significantly reduce quality.
7. Vector quantization may require significant memory for codebooks.
8. A good quantizer may require careful optimization.

## 21. Quantization Artifacts

Excessive quantization can introduce visible distortions.

### Common effects include:

* **Blocking artifacts** — especially in block-based compression.
* **Blurring** — loss of high-frequency detail.
* **Ringing** — oscillatory artifacts near sharp edges.
* **Banding** — visible transitions between quantized intensity levels.
* **Loss of texture** — fine patterns may disappear.

The severity depends on the quantization level and the image content.

## 22. Applications of Quantizing Compression

Quantization is used in:

* JPEG image compression
* JPEG 2000
* Digital photography
* Web image compression
* Multimedia systems
* Image transmission
* Video compression
* Image storage
* Pattern recognition
* Machine-learning data compression

## Important Terms

| Term | Meaning |
| --- | --- |
| **Quantization**             | Mapping many possible values to fewer representative values |
| **Quantization Level**       | One of the allowed output values                            |
| **Quantization Step Size**   | Width of an interval in uniform quantization                |
| **Quantization Error**       | Difference between original and quantized values            |
| **Scalar Quantization**      | Quantizes individual values independently                   |
| **Vector Quantization**      | Quantizes groups of values together                         |
| **Codebook**                 | Collection of representative vectors in VQ                  |
| **Uniform Quantization**     | Equal-sized quantization intervals                          |
| **Non-Uniform Quantization** | Unequal-sized quantization intervals                        |
| **Lossy Compression**        | Compression in which some information is discarded          |

## Summary

**Quantizing compression** reduces image data by mapping a large number of possible values into a smaller set of representative values.

The fundamental operation is:

$$
\boxed{x\rightarrow Q(x)}
$$

The quantization error is:

$$
\boxed{e=x-Q(x)}
$$

The major types are:

1. **Scalar Quantization** — each value is quantized independently.
2. **Vector Quantization** — groups of values are quantized together using a codebook.

Scalar quantization can further be:

* **Uniform**
* **Non-uniform**

Quantization is generally a **lossy operation** because the original values cannot usually be recovered exactly.

In practical compression systems, quantization is often followed by entropy coding:

$$
\boxed{
\text{Image}
\rightarrow
\text{Transform}
\rightarrow
\text{Quantization}
\rightarrow
\text{Entropy Coding}
\rightarrow
\text{Compressed Image}
}
$$

### One-line definition

> **Quantizing compression is a lossy image compression technique that reduces the number of bits required to represent image data by mapping a large set of input values to a smaller set of representative quantized values.**

### Key point to remember

$$
\boxed{
\text{Fewer Quantization Levels}
\rightarrow
\text{Higher Compression}
\rightarrow
\text{Greater Information Loss}
}
$$

Conversely,

$$
\boxed{
\text{More Quantization Levels}
\rightarrow
\text{Better Quality}
\rightarrow
\text{Lower Compression}
}
$$
