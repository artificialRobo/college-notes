# Color images

## Definition

A **color image** is a digital image in which each pixel contains **color information** instead of only intensity values.

A color image is usually represented using the **RGB (Red, Green, Blue) color model**.

## RGB color model

Each pixel consists of **three color components**:

* **R (Red)**
* **G (Green)**
* **B (Blue)**

The combination of these three components produces different colors.

Pixel = (R, G, B)

## Pixel values

For an 8-bit color image, each component has values from **0 to 255**.

Examples:

| RGB value | Color |
| --- | --- |
| (0, 0, 0) | Black |
| (255, 255, 255) | White |
| (255, 0, 0) | Red |
| (0, 255, 0) | Green |
| (0, 0, 255) | Blue |

## Representation

A color image is represented by **three matrices**, one for each color channel.

R channel

255 120
60 0

G channel

0 180
255 90

B channel

30 200
100 255

These three channels together form the final color image.

## Color depth

Color depth is the number of bits used to represent a pixel.

For RGB images:

* **8 bits for Red**
* **8 bits for Green**
* **8 bits for Blue**

Total = **24 bits per pixel**

Number of possible colors = **2^24 = 16,777,216 colors**

## Characteristics

* Contains **brightness and color information**
* Provides a more realistic representation of objects
* Requires more storage than intensity images
* More computationally expensive to process

## Advantages

* Better visual appearance
* Preserves color details
* Useful for object recognition and scene analysis
* Suitable for photography and multimedia applications

## Applications

* Digital photography
* Video processing
* Medical color imaging
* Remote sensing
* Traffic monitoring
* Computer vision systems 

## Difference between intensity and color images

| Intensity image | Color image |
| --- | --- |
| One channel | Three channels (RGB) |
| Gray levels only | Full color information |
| Lower memory requirement | Higher memory requirements |
| Simpler processing | More complex processing |

## Short Summary

A **color image** is a digital in which each pixel is represented by three color components (Red, Green, and Blue). Each channel stores an intensity value, and the combination of the three channels produces the final color of the image.
