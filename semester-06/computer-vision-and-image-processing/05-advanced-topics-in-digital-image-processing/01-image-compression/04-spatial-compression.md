# 5.1.4 Spatial Compression

## 1. Introduction

**Spatial compression** is an image compression technique that exploits the **spatial relationship and correlation between neighboring pixels** in an image.

In most natural images, adjacent pixels tend to have similar intensity or color values. Therefore, storing every pixel independently results in considerable **interpixel redundancy**.

Spatial compression reduces this redundancy by representing a pixel in terms of:

* Its neighboring pixels
* The difference from a neighboring pixel
* A predicted value
* A group or pattern of nearby pixels

### Core idea

> **Instead of encoding every pixel independently, spatial compression exploits the relationship between neighboring pixels to represent image data more efficiently.**

## 2. Need for Spatial Compression

Consider a small region of a grayscale image:

$$
\begin{bmatrix}
100 & 101 & 102\
100 & 101 & 103\
99 & 100 & 102
\end{bmatrix}
$$

The neighboring pixel values are very similar.

If every pixel is stored independently, the same type of information is repeatedly represented.

This repetition is called **interpixel redundancy** or **spatial redundancy**.

Spatial compression attempts to remove this redundancy.

$$
\boxed{
\text{Spatial Correlation}
\rightarrow
\text{Interpixel Redundancy}
\rightarrow
\text{Compression Opportunity}
}
$$

## 3. Spatial Redundancy

### Definition

**Spatial redundancy** refers to the repeated or predictable information present among neighboring pixels of an image.

Natural images generally contain smooth regions in which adjacent pixels have similar values.

For example:

$$
100,;101,;102,;103,;104
$$

Instead of representing every value independently, we could represent the first value and then the changes:

$$
100,;+1,;+1,;+1,;+1
$$

The second representation is more suitable for compression because the differences are small and may require fewer bits after further coding.

## 4. Spatial Correlation

Spatial compression depends heavily on **spatial correlation**.

Spatial correlation describes the relationship between the values of neighboring pixels.

If two neighboring pixels have similar values, they have **high spatial correlation**.

If their values vary significantly and unpredictably, they have **low spatial correlation**.

### Example

Smooth image region:

$$
100,;101,;101,;102,;102
$$

=> High correlation.

Highly textured region:

$$
20,;230,;45,;210,;60
$$

=> Lower correlation.

Therefore:

$$
\boxed{
\text{Higher Spatial Correlation}
\Rightarrow
\text{Greater Compression Potential}
}
$$

## 5. Basic Principle of Spatial Compression

A general spatial compression process can be represented as:

```text
Original Image
      ↓
Analyze Neighboring Pixels
      ↓
Exploit Spatial Correlation
      ↓
Generate Differences / Prediction Errors
      ↓
Encode the Result
      ↓
Compressed Image Data
```

Instead of directly encoding the pixel (x(i,j)), the encoder may predict it from neighboring pixels.

Let:

$$
\hat{x}(i,j)
$$

be the predicted value of the pixel.

The prediction error is:

$$
\boxed{
e(i,j)=x(i,j)-\hat{x}(i,j)
}
$$

If the prediction is good, the error values will generally be small.

These smaller, more concentrated values can then be encoded efficiently.

## 6. Predictive Coding

**Predictive coding** is one of the important approaches used in spatial compression.

The basic idea is:

> Predict the current pixel from previously known neighboring pixels and encode only the prediction error.

For example, suppose the actual pixel value is:

$$
x=105
$$

and the predicted value is:

$$
\hat{x}=103
$$

Then:

$$
e=x-\hat{x}
$$

$$
e=105-103=2
$$

Instead of directly encoding 105, the encoder represents the prediction error as:

$$
\boxed{e=2}
$$

If prediction errors are generally small, they can be represented efficiently.

## 7. Predictive Coding Model

A simplified predictive coding system is:

$$
\boxed{
\text{Image}
\rightarrow
\text{Predictor}
\rightarrow
\text{Prediction Error}
\rightarrow
\text{Encoder}
\rightarrow
\text{Compressed Data}
}
$$

During decompression:

$$
\boxed{
\text{Compressed Data}
\rightarrow
\text{Decoder}
\rightarrow
\text{Prediction Error}
\rightarrow
\text{Predictor}
\rightarrow
\text{Reconstructed Image}
}
$$

For a lossless predictive system:

$$
x(i,j)=\hat{x}(i,j)+e(i,j)
$$

Thus, the original pixel can be reconstructed exactly.

## 8. Types of Spatial Prediction

The predicted value of a pixel can be obtained from different neighboring pixels.

### 8.1 One-Dimensional Prediction

The current pixel may be predicted using the previous pixel:

$$
\hat{x}(i)=x(i-1)
$$

The prediction error becomes:

$$
e(i)=x(i)-x(i-1)
$$

This is simple and useful for sequences of pixels.

### 8.2 Two-Dimensional Prediction

For images, the current pixel can be predicted using neighboring pixels such as:

* Left pixel
* Upper pixel
* Upper-left pixel
* Combination of several neighboring pixels

For example:

$$
\hat{x}(i,j)=x(i,j-1)
$$

uses the **left neighbor** as the prediction.

Another simple predictor could be:

$$
\hat{x}(i,j)=\frac{x(i,j-1)+x(i-1,j)}{2}
$$

which uses the left and upper neighbors.

The choice of predictor depends on the image characteristics and compression algorithm.

## 9. Differential Coding

A common way of exploiting spatial redundancy is **differential coding**.

Instead of encoding the absolute pixel values, the encoder stores the differences between neighboring pixels.

Suppose the pixel sequence is:

$$
100,;102,;103,;105,;106
$$

The differences can be represented as:

$$
100,;+2,;+1,;+2,;+1
$$

The resulting sequence contains many small values.

These small differences can then be efficiently encoded using a statistical coding technique.

Thus:

$$
\boxed{
\text{Pixel Values}
\rightarrow
\text{Differences}
\rightarrow
\text{Statistical Encoding}
}
$$

This combination can provide significant compression.

## 10. Run-Length Encoding and Spatial Compression

**Run-Length Encoding (RLE)** can also exploit spatial redundancy when identical or similar values occur consecutively.

Consider a binary image row:

$$
11111111000000001111
$$

Instead of storing every pixel individually, it can be represented as:

$$
8(1),;8(0),;4(1)
$$

or:

$$
(8,1),(8,0),(4,1)
$$

This is particularly effective for images containing large uniform regions.

### Suitable images

RLE works well for:

* Binary images
* Text documents
* Line drawings
* Simple graphics
* Images with large uniform areas

It is less effective for highly detailed photographs.

## 11. Transform-Based Spatial Compression

Another important approach is to transform image data into a different representation where the image information becomes easier to compress.

A common example is the **Discrete Cosine Transform (DCT)**.

Instead of directly representing pixels, a block of pixels is transformed into frequency coefficients.

The transformed coefficients can then be quantized and encoded.

A simplified JPEG-style process is:

$$
\boxed{
\text{Image}
\rightarrow
\text{DCT}
\rightarrow
\text{Quantization}
\rightarrow
\text{Entropy Coding}
\rightarrow
\text{Compressed Data}
}
$$

The DCT concentrates much of the image energy into a relatively small number of coefficients, particularly for smooth image regions.

This allows less important coefficients to be represented with lower precision.

## 12. Spatial Compression and Image Quality

Spatial compression can be either **lossless or lossy**, depending on the technique used.

### Lossless spatial compression

The original image can be reconstructed exactly.

Examples include:

* Lossless predictive coding
* Differential coding followed by lossless entropy coding
* Some forms of RLE

### Lossy spatial compression

Some information is discarded to achieve higher compression.

Examples include:

* Predictive coding with quantization
* Transform coding with quantization
* JPEG-style compression

Therefore:

$$
\boxed{
\text{Spatial Compression} \neq \text{Always Lossy}
}
$$

The presence of spatial processing alone does not determine whether information is lost.

## 13. Example of Spatial Compression

Consider a grayscale pixel sequence:

$$
100,;101,;102,;103,;104,;104,;105
$$

### Step 1: Original representation

The original values are:

$$
100,101,102,103,104,104,105
$$

### Step 2: Differential representation

Taking differences:

$$
100,+1,+1,+1,+1,0,+1
$$

### Step 3: Encode the differences

The resulting data contains mostly small values:

$$
+1,;+1,;+1,;+1,;0,;+1
$$

These values have a highly concentrated statistical distribution and can therefore be efficiently encoded using a statistical coding method.

This demonstrates how spatial and statistical compression can work together.

## 14. Spatial Compression vs. Statistical Compression

These two techniques are closely related but solve different problems.

| Feature          | Spatial Compression                              | Statistical Compression               |
| --- | --- | --- |
| Main redundancy  | Interpixel/spatial redundancy                    | Coding redundancy                     |
| Main principle   | Exploit relationships between neighboring pixels | Exploit symbol probabilities          |
| Typical approach | Prediction, differences, transforms              | Variable-length or arithmetic coding  |
| Examples         | Predictive coding, DPCM, transform methods       | Huffman, arithmetic coding            |
| Can be lossless? | Yes                                              | Yes                                   |
| Can be lossy?    | Yes                                              | Usually used as lossless coding stage |

### Important relationship

A practical compression system may use both:

$$
\boxed{
\text{Spatial Processing}
\rightarrow
\text{Statistical Coding}
\rightarrow
\text{Compressed Data}
}
$$

For example:

$$
\text{Image}
\rightarrow
\text{Prediction}
\rightarrow
\text{Prediction Errors}
\rightarrow
\text{Huffman Coding}
$$

The prediction stage removes **spatial redundancy**, while Huffman coding removes **coding redundancy**.

## 15. Differential Pulse Code Modulation (DPCM)

**Differential Pulse Code Modulation (DPCM)** is an important predictive image compression technique.

Instead of encoding the actual pixel value, DPCM encodes the difference between the actual pixel and its predicted value.

$$
\boxed{
e(n)=x(n)-\hat{x}(n)
}
$$

where:

* $x(n)$ = actual pixel value
* $\hat{x}(n)$ = predicted pixel value
* $e(n)$ = prediction error

The decoder reconstructs the pixel using:

$$
\boxed{
x(n)=\hat{x}(n)+e(n)
}
$$

DPCM can operate in either lossless or lossy form depending on whether the prediction error is quantized.

## 16. Advantages of Spatial Compression

1. **Reduces interpixel redundancy.**
2. Makes use of the natural correlation between neighboring pixels.
3. Can achieve good compression for smooth images.
4. Predictive methods can be computationally efficient.
5. Can be combined with statistical coding methods.
6. Can be implemented as either lossless or lossy compression.
7. Particularly useful for natural images containing smooth regions.

## 17. Limitations of Spatial Compression

1. Performance depends on the degree of spatial correlation.
2. Highly textured images may provide less compression.
3. Sharp edges can produce relatively large prediction errors.
4. A poor predictor can reduce compression efficiency.
5. Some advanced spatial methods require additional computation.
6. Lossy implementations may introduce image degradation.

## 18. Applications

Spatial compression is used in many image-processing systems, including:

* Digital photography
* Medical imaging
* Satellite imaging
* Remote sensing
* Document image compression
* Multimedia systems
* Image transmission
* Digital cameras
* Image databases
* Video and frame compression

## Important Terms

| Term | Meaning |
| --- | --- |
| **Spatial Compression**   | Compression that exploits relationships among neighboring pixels    |
| **Spatial Redundancy**    | Repeated/predictable information between neighboring pixels         |
| **Interpixel Redundancy** | Another term for redundancy caused by pixel-to-pixel correlation    |
| **Predictive Coding**     | Encoding prediction errors rather than direct pixel values          |
| **Prediction Error**      | Difference between actual and predicted pixel values                |
| **Differential Coding**   | Representing changes/differences between pixel values               |
| **DPCM**                  | Differential Pulse Code Modulation                                  |
| **RLE**                   | Encoding consecutive repeated values as runs                        |
| **DCT**                   | Transform that represents image blocks using frequency coefficients |

## Summary

**Spatial compression** is a technique that reduces **interpixel redundancy** by exploiting the correlation between neighboring pixels.

The main idea is to avoid encoding every pixel independently. Instead, the pixel can be predicted from neighboring pixels, and only the **prediction error** is encoded.

The prediction error is:

$$
\boxed{
e(i,j)=x(i,j)-\hat{x}(i,j)
}
$$

where $x(i,j)$ is the actual pixel and $\hat{x}(i,j)$ is the predicted pixel.

Important approaches include:

* **Predictive coding**
* **Differential coding**
* **DPCM**
* **Run-Length Encoding**
* **Transform-based techniques**

Spatial compression can be combined with statistical compression:

$$
\boxed{
\text{Image}
\rightarrow
\text{Spatial Prediction}
\rightarrow
\text{Prediction Errors}
\rightarrow
\text{Statistical Coding}
\rightarrow
\text{Compressed Data}
}
$$

### One-line definition

> **Spatial compression is an image compression technique that reduces interpixel redundancy by exploiting the spatial correlation between neighboring pixels and representing image information through predictions, differences, or other compact spatial representations.**
