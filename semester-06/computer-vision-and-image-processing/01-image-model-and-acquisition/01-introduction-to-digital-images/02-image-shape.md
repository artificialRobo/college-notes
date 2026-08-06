# Image Shape

## Definition

Image shape refers to the **geometric structure and dimensions of an image**. It describes how an image is represented in terms of its **rows, columns, width, height, and aspect ratio**.

An image is represented as a rectangular array of pixels.

## Image dimensions

An image has two dimensions:

* **Width (W)** = number of columns
* **Height(H)** = number of rows

Image size is written as:

**H x W**

Example:

* 256 x 256
* 512 x 512
* 1920 x 1080

## Shape of an image

### Square image

* Width = Height
* Example: 512 x 512

### Rectangular image

* Width != Height
* Example: 640 x 480

## Aspect Ratio

Aspect ratio is the ratio of image width to image height.

Aspect ratio = Width ÷ Height

Common aspect ratios:

| Aspect ratio | Example |
| --- | --- |
| 1:1 | 512 x 512 |
| 4:3 | 640 x 480 |
| 16:9 | 1920 x 1080 |

A change in aspect ratio may distort the image shape.

## Pixel arrangement

Pixels are arranged in a grid.

For an M x N image:

* M = number of rows
* N = number of columns
* Total pixels = M x N

Example:

For a 512 x 512 image:

Total pixels = 512 x 512 = 262,144

## Spatial representation

Each pixel is identified by coordinates:

(x,y)

where:

* x -> column index
* y -> row index

The image boundary is determined by its width and height.

## Importance of image shape

Image shape affects:

* image display
* image storage
* geometric transformations
* resizing
* rotation
* object measurement
* image analysis

## Advantages of rectangular image representation

* Simple storage in memory
* Easy pixel indexing
* Efficient image processing operations
* Suitable for matrix representation

## Quick Summary

**Image Shape** is the geometric representation of an image defined by its width, height, pixel arrangement, and aspect ratio, which determine the overall dimensions and spatial structure of the image.
