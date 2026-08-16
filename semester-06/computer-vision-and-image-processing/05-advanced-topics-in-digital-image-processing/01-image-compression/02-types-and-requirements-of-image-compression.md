# 5.1.2 Types and Requirements of Image Compression

## 1. Introduction

Image compression techniques can be classified according to **how redundancy is removed** and **whether information is permanently lost**.

A suitable image compression technique should reduce the amount of data required to store or transmit an image while maintaining the required image quality and computational efficiency.

The two fundamental types of image compression are:

1. **Lossless compression**
2. **Lossy compression**

Compression techniques can also be categorized based on the type of redundancy they exploit, such as **statistical, spatial, contour-based, and quantization-based compression**.

## 2. Types of Image Compression

### 2.1 Lossless Image Compression

In **lossless compression**, the compressed representation allows the original image to be reconstructed **exactly**.

No image information is permanently discarded.

$$
\boxed{\text{Original Image} = \text{Reconstructed Image}}
$$

#### Characteristics

* No loss of information.
* Exact reconstruction is possible.
* Usually provides a lower compression ratio than lossy methods.
* Suitable when image accuracy is critical.

#### Examples

* Run-Length Encoding (RLE)
* Huffman Coding
* Arithmetic Coding
* LZW
* PNG

#### Applications

Lossless compression is commonly used for:

* Medical images
* Engineering drawings
* Scientific images
* Technical documents
* Maps
* Images used for further numerical analysis

#### Example

Suppose an image contains a long sequence of identical pixels:

$$
AAAAAAAABBBBCC
$$

Instead of storing every symbol separately, it can be represented as:

$$
8A4B2C
$$

The information can be recovered exactly.

### 2.2 Lossy Image Compression

In **lossy compression**, some image information is deliberately discarded to obtain a much smaller representation.

After decompression, the reconstructed image is not exactly identical to the original.

$$
\boxed{\text{Original Image} \neq \text{Reconstructed Image}}
$$

However, the difference can often be made sufficiently small that it is difficult for the human eye to notice.

#### Characteristics

* Some information is lost.
* Provides higher compression ratios.
* Reconstructed image may have reduced quality.
* Suitable when small file size is more important than exact reconstruction.

#### Examples

* JPEG
* JPEG 2000 in lossy mode
* Transform-based compression techniques
* Quantization-based methods

#### Applications

* Digital photographs
* Web images
* Social media
* Multimedia applications
* Image databases
* Consumer photography

#### Important point

Lossy compression should be controlled carefully. Excessive compression can introduce:

* Blurring
* Blocking artifacts
* Loss of fine details
* Ringing artifacts
* Color distortions

## 3. Comparison Between Lossless and Lossy Compression

| Feature                    | Lossless Compression           | Lossy Compression                |
| --- | --- | --- |
| Information loss           | None                           | Some information is lost         |
| Reconstruction             | Exact                          | Approximate                      |
| Compression ratio          | Usually lower                  | Usually higher                   |
| Image quality              | Completely preserved           | May decrease                     |
| Repeated encoding/decoding | Safe for exact data            | May cause additional degradation |
| Complexity                 | Often relatively simple        | Often more complex               |
| Applications               | Medical, scientific, technical | Photography, web, multimedia     |
| Examples                   | PNG, RLE, Huffman, LZW         | JPEG                             |

### Easy way to remember

> **Lossless -> No information lost -> Exact image**
> **Lossy -> Some information lost -> Smaller file**

## 4. Classification Based on Compression Technique

In digital image processing, compression methods can also be classified according to the type of redundancy or image information they exploit.

### Major categories include:

1. **Statistical compression**
2. **Spatial compression**
3. **Contour coding**
4. **Quantizing compression**

These categories correspond directly to the topics covered later in this unit.

### 4.1 Statistical Compression

Statistical compression exploits the **frequency of occurrence of image symbols or pixel values**.

Frequently occurring symbols are represented using shorter codes, while less frequent symbols receive longer codes.

#### Examples

* Huffman coding
* Arithmetic coding

#### Main principle

$$
\text{Higher probability} \rightarrow \text{Shorter code}
$$

$$
\text{Lower probability} \rightarrow \text{Longer code}
$$

This reduces **coding redundancy**.

### 4.2 Spatial Compression

Spatial compression exploits the relationship between **neighboring pixels**.

Adjacent pixels in natural images are generally correlated, meaning their intensity or color values tend to be similar.

Instead of encoding each pixel independently, the compression algorithm can encode:

* Pixel differences
* Prediction errors
* Repeated pixel values
* Transform coefficients

This reduces **interpixel or spatial redundancy**.

#### Examples

* Predictive coding
* Run-Length Encoding
* Transform-based techniques

### 4.3 Contour Coding

**Contour coding** represents an object or region primarily through its **boundary or contour** rather than representing every pixel within the region independently.

The contour describes the shape of an object.

For example, instead of storing every pixel belonging to a simple object, its boundary can be represented using a sequence of directions or boundary points.

#### Applications

Contour representation is useful in:

* Object recognition
* Shape analysis
* Character recognition
* Image segmentation
* Pattern recognition

### 4.4 Quantizing Compression

Quantizing compression reduces the precision of image data by mapping a large set of possible values to a smaller set of representative values.

For example:

$$
0,1,2,3,4,5,6,7
$$

might be mapped into fewer levels such as:

$$
0,2,4,6
$$

This reduces the amount of information that needs to be stored.

Quantization is generally associated with **lossy compression**, because the original values cannot always be recovered exactly.

## 5. Requirements of Image Compression

A good image compression system must satisfy several requirements. The relative importance of these requirements depends on the application.

### 5.1 High Compression Ratio

The primary requirement is to reduce the amount of data required to represent an image.

The compression ratio is:

$$
\boxed{
C_R=\frac{\text{Original Image Size}}
{\text{Compressed Image Size}}
}
$$

A higher compression ratio means that less storage is required.

However, a very high compression ratio may result in unacceptable image degradation in lossy systems.

Therefore:

$$
\boxed{\text{High Compression} + \text{Acceptable Quality}}
$$

is generally the desired objective.

### 5.2 Good Reconstructed Image Quality

The compressed image should maintain sufficient visual quality for its intended application.

For lossless compression:

$$
\text{Quality Loss}=0
$$

For lossy compression, the quality loss should remain within an acceptable limit.

For example:

* Medical diagnosis → very high fidelity required
* Web thumbnail → moderate quality may be acceptable
* Scientific analysis → potentially exact reconstruction required
* Social media → high compression may be acceptable

### 5.3 Low Computational Complexity

The compression algorithm should not require excessive computational resources.

This is particularly important for:

* Mobile devices
* Embedded systems
* Real-time imaging
* Cameras
* Video communication systems

A highly complex algorithm may achieve excellent compression but may not be practical when processing speed is important.

### 5.4 Fast Encoding and Decoding

A compression system should ideally perform both:

* **Encoding quickly**
* **Decoding quickly**

This is particularly important in real-time applications.

For example, in a live imaging or communication system, slow decompression can cause delays even if the compressed file is very small.

### 5.5 Low Memory and Storage Requirements

The compression algorithm itself should not require excessive memory.

This is important for systems with limited resources, such as:

* Embedded devices
* Smartphones
* IoT devices
* Digital cameras
* Sensor systems

### 5.6 Error Robustness

In communication systems, compressed data may be affected by transmission errors.

A good compression system may therefore need to minimize the impact of errors.

This is especially important in:

* Wireless communication
* Satellite communication
* Remote sensing
* Mobile networks

A single error in some highly compressed data streams can potentially affect a large portion of the reconstructed image.

### 5.7 Scalability

Some applications require an image to be available at different quality or resolution levels.

A scalable compression technique allows the user to obtain:

* Low-resolution versions
* Medium-quality versions
* High-quality versions

from the same compressed representation.

This is useful for web applications and progressive image transmission.

### 5.8 Suitability for the Application

No single compression technique is ideal for every application.

The compression method must be selected according to the requirements of the system.

For example:

| Application         | Preferred Requirement                  |
| --- | --- |
| Medical imaging     | High fidelity                          |
| Web images          | Small file size + acceptable quality   |
| Satellite imaging   | High compression + error robustness    |
| Scientific imaging  | Accurate reconstruction                |
| Digital photography | High compression + good visual quality |
| Real-time systems   | Fast encoding/decoding                 |

## 6. Important Performance Measures

The effectiveness of an image compression algorithm can be evaluated using several parameters.

### 6.1 Compression Ratio

$$
\boxed{
C_R=\frac{N_o}{N_c}
}
$$

where:

* $N_o$ = number of bits in the original image
* $N_c$ = number of bits in the compressed image

Higher (C_R) generally means greater compression.

### 6.2 Compression Factor

The **compression factor** can be expressed as:

$$
\boxed{
CF=\frac{N_c}{N_o}
}
$$

It indicates the fraction of the original data that remains after compression.

For example, if:

$$
N_o=10\text{ MB}
$$

and

$$
N_c=2\text{ MB}
$$

then:

$$
CF=\frac{2}{10}=0.2
$$

Thus, the compressed image requires only **20% of the original storage**.

### 6.3 Bits Per Pixel

Another useful measure is **bits per pixel (bpp)**.

$$
\boxed{
bpp=\frac{\text{Total compressed bits}}
{\text{Number of pixels}}
}
$$

A lower bpp generally indicates a more compact representation.

However, image quality must also be considered, particularly for lossy compression.

## 7. Fundamental Trade-offs

Designing an image compression system involves balancing several competing requirements.

### Compression Ratio vs. Image Quality

Higher compression often results in lower quality in lossy systems.

### Compression Ratio vs. Computational Complexity

More sophisticated algorithms may achieve better compression but require greater processing power.

### Speed vs. Compression Efficiency

Very fast algorithms may not achieve the highest possible compression ratio.

### Memory Usage vs. Algorithm Complexity

Advanced algorithms may require more memory for intermediate calculations.

Therefore, the best compression algorithm is not necessarily the one with the highest compression ratio. It is the one that provides the **best balance between compression, quality, speed, complexity, and application requirements**.

## 8. Overall Classification

The classification can be summarized as:

```text
                    Image Compression
                           │
             ┌─────────────┴─────────────┐
             │                           │
         Lossless                     Lossy
             │                           │
      Exact reconstruction        Approximate reconstruction
             │                           │
      ┌──────┴──────┐              ┌─────┴─────┐
      │             │              │           │
     RLE         Huffman          JPEG     Quantization
                  Coding
```

Another classification based on the method is:

```text
Image Compression Techniques
            │
   ┌────────┼─────────┬────────────┐
   │        │         │            │
Statistical Spatial  Contour   Quantizing
Compression Compression Coding  Compression
```

## Summary

**Image compression** can primarily be classified into **lossless** and **lossy** compression.

### Lossless Compression

* No information is lost.
* Original image can be reconstructed exactly.
* Lower compression ratio.
* Used in medical, scientific, and technical applications.
* Examples: RLE, Huffman, LZW, PNG.

### Lossy Compression

* Some information is discarded.
* Reconstruction is approximate.
* Higher compression ratio.
* Used in photography, web, and multimedia applications.
* Example: JPEG.

Image compression methods can also be categorized as:

* **Statistical compression** → exploits coding/statistical redundancy.
* **Spatial compression** → exploits correlation between neighboring pixels.
* **Contour coding** → represents object boundaries efficiently.
* **Quantizing compression** → reduces the precision/number of possible values.

### Main requirements of an image compression system

1. High compression ratio
2. Good reconstructed image quality
3. Low computational complexity
4. Fast encoding and decoding
5. Low memory requirements
6. Error robustness
7. Scalability, where required
8. Suitability for the target application

> A good image compression system should reduce image data as much as possible while maintaining the required image quality, processing speed, reliability, and resource efficiency.
