# Image Model

## Definition

An image model is the mathematical representation of an image. A digital image is represented as a two-dimentional function:

**f(x,y)**

where:

* **x** = horizontal coordinate
* **y** = vertical coordinate
* **f(x,y)** = intensity (brightness) or color value at position (x,y)

## Basic Concept

A digital image is made up of **pixels (picture elements)** arranged in rows and columns.

Each pixel has:

* a **location** -> (x,y)
* an **intensity or color value** -> f(x,y)

## Image Formation model

An image is formed when light falls on an object and gets reflected, and this **reflected** light is captured by a sensor. The intensity of an Image depends on illumination and reflectance.

**f(x,y) = i(x,y) x r(x,y)**

where:

* **i(x,y)** = illumination (light falling on the object)
* **r(x,y)** = reflectance (light reflected by the object)

## Continuous and digital image

### Continuous image

* Infinite coordinates
* Continuous intensity value

### Digital image

* Discrete coordinates (pixels)
* Discrete intensity values

Conversion from continuous to digital image:

1. **Sampling** -> discretizes spatial coordinates
2. **Quantization** -> discretizes intensity values

## Coordinate system

* Origin (0,0) is at the **top-left corner**.
* x increases to the **right**.
* y increases **downward**.

## Gray-Level representation

For a k-bit image:

**L = 2^k**

where **L** is the number of gray levels.

Examples:

* 1 bit = 2 gray levels
* 8 bits = 256 gray levels
* 10 bits = 1024 gray levels

In an 8-bit image:

* 0 = black
* 256 = white

## Image resolution

Resolution = number of rows x number of columns.

Example:

* 512 x 512 image
* Total pixels = 512 x 512 = 262,144 pixels

Higher resolution means more spatial detail.

## Importance of image model

The image model is the basis for:

* image enhancement
* filtering
* edge detecting
* segmentation
* feature extraction
* object recognition

## Quick Summary

**Image model:** A mathematical representation of a digital image as a two-dimentional discrete function f(x,y), where each pixel is identified by its coordinates and corresponding intensity or color value.
