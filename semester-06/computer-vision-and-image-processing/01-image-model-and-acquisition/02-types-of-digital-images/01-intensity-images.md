# Intensity images

## Defintion

An **intensity image** (grayscale image) is a digital image in which each pixel represents **only the brightness or intensity** of the image.

Each pixel stores a **single intensity value**.

## Pixel Values

In an 8-bit intensity image:

* 0 -> black
* 255 -> white
* 1-254 -> different shades of gray

Thus, an 8-bit image contains **256 gray levels**.

## Representation

An intensity image is represented by a **2D matrix**.

Example:

| | | |
| --- | --- | ---|
| 0 | 50 | 120 |
| 80 | 150 | 220 |
| 30 | 180 | 255 |

Each number represents the intensity of the corresponding pixel.

## Characteristics

* Contains **only brightness information**
* Does **not contain color information**
* Requires **less memory** than color images
* Easy to process mathematically

## Gray-level resolution

The number of intensity levels depends on the number of bits per pixel.

L = 2^k

where:

* **L** = number of gray levels
* **k** = bits per pixel

Examples:

| Bits per pixel | Gray levels |
| --- | --- |
| 1 | 2 |
| 4 | 16 |
| 8 | 256 |
| 10 | 1024 |

## Advantages

* Simple image representation
* Lower storage requirements
* Faster image processing
* Suitable for many computer vision algorithms

## Applications

* Medical imaging (X-ray, CT scans)
* Document scanning
* Satellite imaging
* Industrial Inspection
* Face detection and recognition

## Difference from binary image

| Binary image | Intensity image |
| --- | --- |
| 2 intensity levels | Multiple gray levels |
| 1 bit per pixel | Usually 8 bits per pixel |
| Black and white only | Shades of gray |

## Short Summary

An **intensity image** is a grayscale digital image in which each pixel is represented by a single intensity value, typically ranging from 0 (black) to 255 (white), and the image is represented as a two-dimentional matrix of gray levels.
