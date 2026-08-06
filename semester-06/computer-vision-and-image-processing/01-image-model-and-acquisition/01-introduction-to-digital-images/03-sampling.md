# Sampling

## Definition

Sampling is the process of converting a **continuous image into a digital image** by selecting values at **discrete spatial locations (pixels)**.

It determines **how many pixels are used to represent an image**.

A continuous image f(x,y) is converted into a digital image by taking samples at regular intervals.

## Why is Sampling Needed?

A real-world image contains infinite points.
A digital image stores only a finite number of points (pixels).
Sampling divides the images plane into a **grid of pixels**.
Continuous image -> Sampling -> Pixel grid (digital image)
Each grid point stores the intensity value of the image.

## Mathematical representation

If the sampling intervals are ∆x and ∆y, the sampled image is represented as:

f(m∆x, n∆y)

where:

* m = row index
* n = column index
* ∆x = sampling distance in x-direction
* ∆y = sampling distance in y-direction

After sampling, coordinates become discrete.

## Example

Suppose we photograph a flower.

### Before Sampling

The flower exists continuously.

```text
Flower
```

No fixed pixels.

### After Sampling

Suppose the camera captures

```text
640 × 480 pixels
```

This means

* Width = 640 pixels
* Height = 480 pixels

Total pixels

```text
640 × 480 = 307200
```

The flower is now represented using **307,200 pixels**.

## Sampling Interval

Sampling interval is the distance between two adjacent samples.

* **Small interval** -> more samples
* **Large interval** -> fewer samples

Smaller sampling intervals produce images with better spatial detail.

## Sampling frequency

Sampling frequency is the number of samples taken per unit distance.

Sampling frequency: 1 / Sampling Interval

Higher sampling frequency gives better image representation.

## Effect of sampling

### High sampling

* More pixels
* Better image quality
* Higher resolution
* Larger storage requirement

### Low sampling

* Fewer pixels
* Loss of detail
* Jagged edges
* Lower resolution
* Smaller storage requirement

## Spatial resolution

Spatial resolution is the ability to distinguish small details in an image.

It depends on the sampling density.

More pixels per unit area result in higher spatial resolution.

Example:

* 128 x 128 -> low resolution
* 512 x 512 -> medium resolution
* 1920 x 1080 -> high resolution

## Nyquist sampling theorem

To preserve image information, the sampling frequency must be at least **twice the highest spatial frequency** present in the image.

If this condition is not satisfied, aliasing occurs.

### Aliasing

Aliasing is the distortion caused by **insufficient sampling**.

It appears as:

* jagged edges
* false patterns
* moiré patterns
* loss of fine details

Aliasing occurs when:

Sampling frequency < 2 x highest image frequency

## Undersampling and oversampling

### Undersampling

* Sampling frequency too low
* Causes aliasing
* Loss of image information

### Oversampling

* Sampling frequency very high
* Better image quality
* Increased memory and processing time

## Relationship with image resolution

For an M x N image:

* M = number of rows
* N = number of columns

Total number of samples = M x N

Increasing the number of samples increases image resolution.

## Sampling vs quantization

| Sampling | Quantization |
| --- | --- |
| Discretizes spatial coordinates | Discretizes intensity values |
| Determines number of pixels | Determines gray levels |
| Affects spatial resolution | Affects intensity resolution |

## Advantages of proper sampling

* Accurate image representation
* Better spatial resolution
* Reduced distortion
* Improved image analysis and recognition

## Quick Summary

**Sampling** is the process of converting a continuous image into a digital image by selecting intensity value at discrete spatial locations. It determines the spatial resolution of the image and the number of pixels used for image representation.
