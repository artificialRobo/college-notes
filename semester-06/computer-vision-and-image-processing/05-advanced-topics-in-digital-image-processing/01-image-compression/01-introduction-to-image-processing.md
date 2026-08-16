# 5.1.1 Introduction to Image Compression

## 1. Definition

**Image compression** is the process of reducing the amount of data required to represent and store a digital image while preserving an acceptable level of visual quality.

A digital image contains a large number of pixels, and each pixel requires bits to represent its intensity or color. As image resolution and color depth increase, the amount of storage and transmission bandwidth required also increases. Image compression addresses this problem by removing or reducing redundant information in the image.

In simple terms:

> **Image Compression = Representing an image using fewer bits while maintaining the required image quality.**

## 2. Need for Image Compression

Digital images can require significant storage space. For example, an uncompressed color image of size **1920 × 1080 pixels** with 24-bit color depth requires:

$$
1920 \times 1080 \times 24
= 49,766,400 \text{ bits}
$$

or approximately:

$$
\frac{49,766,400}{8} \approx 6.22 \text{ MB}
$$

for just one image, ignoring file headers and other information.

Large numbers of images therefore require substantial storage capacity.

Image compression is needed because it:

1. **Reduces storage requirements**
   Compressed images occupy less disk or memory space.

2. **Reduces transmission time**
   Smaller files can be transmitted more quickly over networks.

3. **Reduces bandwidth requirements**
   Less data needs to be transferred between devices.

4. **Improves communication efficiency**
   It is particularly useful in multimedia, web applications, and image-based communication systems.

5. **Enables efficient multimedia applications**
   Applications such as digital photography, video streaming, medical imaging, satellite imaging, and social media depend heavily on efficient image storage and transmission.

## 3. Basic Principle of Image Compression

Image compression works by identifying **redundancy** or information that can be represented more efficiently.

A typical image contains three major types of redundancy:

### 3.1 Coding Redundancy

Coding redundancy occurs when the codes used to represent image information are not optimal.

For example, if frequently occurring pixel values are assigned short codes and less frequent values are assigned longer codes, the overall number of bits can be reduced.

**Examples:**

* Huffman coding
* Arithmetic coding

### 3.2 Interpixel Redundancy

Neighboring pixels in an image are often highly correlated. In a smooth region, adjacent pixels usually have similar intensity or color values.

Instead of storing every pixel independently, the relationship between neighboring pixels can be exploited.

This is also called **spatial redundancy**.

**Example:**
If a large portion of an image has nearly the same intensity, storing every pixel separately is inefficient. The image can instead be represented using differences or other compact representations.

### 3.3 Psychovisual Redundancy

Some information in an image may be less important to the human visual system.

Psychovisual redundancy occurs when image information that has little perceptual significance is retained with unnecessarily high precision.

Compression techniques can reduce such information while keeping the image visually acceptable.

This principle is especially important in **lossy compression**.

## 4. Compression Ratio

The effectiveness of an image compression method is commonly measured using the **compression ratio**.

$$
\boxed{C_R=\frac{n_1}{n_2}}
$$

where:

* $n_1$ = number of bits in the original image
* $n_2$ = number of bits in the compressed image

### Example

Suppose an original image requires **8 MB**, while its compressed version requires **2 MB**.

$$
C_R=\frac{8}{2}=4
$$

Therefore, the compression ratio is:

$$
\boxed{4:1}
$$

This means that the compressed image requires only one-fourth of the original storage.

## 5. Compression and Decompression

Image compression generally involves two major processes:

### Compression

The original image is processed to produce a compact representation.

$$
\text{Original Image}
\rightarrow
\text{Compression}
\rightarrow
\text{Compressed Data}
$$

### Decompression

The compressed data is processed to reconstruct the image.

$$
\text{Compressed Data}
\rightarrow
\text{Decompression}
\rightarrow
\text{Reconstructed Image}
$$

A complete image compression system can therefore be represented as:

$$
\boxed{
\text{Image}
\rightarrow
\text{Encoder}
\rightarrow
\text{Compressed Data}
\rightarrow
\text{Decoder}
\rightarrow
\text{Reconstructed Image}
}
$$

The **encoder** performs compression, while the **decoder** performs decompression.

## 6. Lossless and Lossy Compression

Image compression techniques are broadly divided into two categories.

### 6.1 Lossless Compression

In **lossless compression**, no information is permanently lost.

After decompression, the reconstructed image is **exactly identical** to the original image.

$$
\boxed{\text{Original Image}=\text{Reconstructed Image}}
$$

It is useful when every pixel must be preserved accurately.

**Applications:**

* Medical images
* Technical drawings
* Documents
* Scientific images
* Images requiring exact reconstruction

**Examples:**

* Run-Length Encoding (RLE)
* Huffman coding
* LZW
* PNG

### 6.2 Lossy Compression

In **lossy compression**, some image information is discarded to achieve a significantly smaller file size.

The reconstructed image is therefore not exactly identical to the original, although the difference may be visually insignificant.

$$
\boxed{\text{Original Image}\neq\text{Reconstructed Image}}
$$

**Applications:**

* Digital photography
* Web images
* Multimedia
* Image sharing
* Storage of large collections of photographs

**Example:**

* JPEG

Lossy compression generally provides a **higher compression ratio** than lossless compression, but at the cost of some image quality.

## 7. Quality–Compression Trade-off

One of the most important concepts in image compression is the trade-off between **file size and image quality**.

Generally:

$$
\boxed{\text{Higher Compression} \Rightarrow \text{Smaller File Size but Lower Quality}}
$$

and

$$
\boxed{\text{Lower Compression} \Rightarrow \text{Larger File Size but Higher Quality}}
$$

For lossless compression, image quality is preserved completely, but the achievable compression ratio is usually lower.

For lossy compression, much higher compression can be achieved, but excessive compression can introduce visible artifacts such as:

* Blurring
* Blocking artifacts
* Loss of fine details
* Ringing
* Color distortion

Therefore, an appropriate compression method must be selected according to the application.

## 8. General Image Compression Model

A conventional image compression system can be divided into three fundamental components:

### 8.1 Mapper

The **mapper** transforms the original image into a representation that is more suitable for compression.

For example, a transform may concentrate important image information into a smaller number of coefficients.

### 8.2 Quantizer

The **quantizer** reduces the precision of image data.

Quantization is usually responsible for information loss in a lossy compression system.

> Quantization is **not reversible**, so it is generally associated with lossy compression.

### 8.3 Symbol Encoder

The **symbol encoder** represents the processed data using efficient binary codes.

Examples include:

* Huffman coding
* Arithmetic coding
* Run-Length Encoding

A simplified model is:

$$
\boxed{
\text{Image}
\rightarrow
\text{Mapper}
\rightarrow
\text{Quantizer}
\rightarrow
\text{Symbol Encoder}
\rightarrow
\text{Compressed Data}
}
$$

During decompression, the reverse operations are performed as far as possible.

## 9. Characteristics of a Good Image Compression Technique

A good image compression technique should ideally provide:

1. **High compression ratio**
2. **Good reconstructed image quality**
3. **Low computational complexity**
4. **Fast encoding and decoding**
5. **Low memory requirements**
6. **Robustness against errors**, where required
7. **Suitability for the intended application**

The importance of each characteristic depends on the application. For example, medical imaging may prioritize image fidelity, whereas web applications may prioritize small file size.

## 10. Applications of Image Compression

Image compression is used extensively in:

| Application         | Purpose                                           |
| --- | --- |
| Digital photography | Reduce photo storage requirements                 |
| Web applications    | Faster loading and reduced bandwidth              |
| Medical imaging     | Efficient storage and transmission                |
| Satellite imaging   | Reduce the amount of transmitted image data       |
| Multimedia systems  | Efficient storage and communication               |
| Video systems       | Reduce the data associated with individual frames |
| Mobile applications | Save storage and network bandwidth                |
| Cloud storage       | Reduce storage costs                              |
| Document imaging    | Efficient storage of scanned documents            |

## 11. Advantages of Image Compression

* Requires less storage space.
* Reduces transmission time.
* Saves network bandwidth.
* Makes image-based applications more efficient.
* Facilitates faster file transfer.
* Allows more images to be stored on a given device.
* Reduces data-management requirements.

## 12. Limitations

Despite its advantages, image compression also has some limitations:

* Lossy compression can reduce image quality.
* Excessive compression may produce visible artifacts.
* Compression and decompression require computational resources.
* Some compression methods may be unsuitable for real-time applications.
* Certain applications require lossless reconstruction and therefore cannot tolerate information loss.

## Key Terms to Remember

| Term                        | Meaning                                                                      |
| --- | --- |
| **Image Compression**       | Reduction of the number of bits needed to represent an image                 |
| **Redundancy**              | Repeated or unnecessary information that can be represented more efficiently |
| **Compression Ratio**       | Ratio of original data size to compressed data size                          |
| **Lossless Compression**    | Compression with exact reconstruction                                        |
| **Lossy Compression**       | Compression involving some information loss                                  |
| **Encoder**                 | Converts image data into compressed representation                           |
| **Decoder**                 | Reconstructs an image from compressed data                                   |
| **Coding Redundancy**       | Inefficient representation of image symbols                                  |
| **Interpixel Redundancy**   | Redundancy caused by correlation between neighboring pixels                  |
| **Psychovisual Redundancy** | Information that has relatively low perceptual importance                    |
| **Quantization**            | Reduction of numerical precision, generally causing information loss         |

## Summary

**Image compression** is a technique for reducing the number of bits required to represent a digital image. It is primarily used to reduce storage requirements and transmission bandwidth.

The major sources of redundancy exploited by compression techniques are:

1. **Coding redundancy**
2. **Interpixel/spatial redundancy**
3. **Psychovisual redundancy**

Image compression is broadly classified into:

* **Lossless compression** — exact reconstruction of the original image.
* **Lossy compression** — some information is discarded to achieve greater compression.

The performance of a compression method is commonly expressed using the **compression ratio**:

$$
\boxed{C_R=\frac{\text{Original Size}}{\text{Compressed Size}}}
$$

A good compression technique attempts to achieve a **small file size while maintaining the required image quality and acceptable computational complexity**.

> **The fundamental objective of image compression is to eliminate or reduce image redundancy so that the image can be stored and transmitted using fewer bits, while maintaining the required level of image quality.**
