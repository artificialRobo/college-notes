# 5.2.1 Image Representation and Description

## 1. Introduction

In digital image processing, an image must be represented in a suitable form before it can be **analyzed, classified, or recognized by a computer**.

**Image representation** refers to the process of converting an image or an object within an image into a suitable mathematical or structural form.

**Image description** refers to extracting meaningful features from the represented image that can be used to distinguish one object from another.

In simple terms:

> **Image Representation → How an object is represented**
> **Image Description → What characteristics of the object are extracted**

For example, consider an image containing a **circle, square, and triangle**. A computer cannot directly understand these objects as humans do. The objects must first be represented using pixels, boundaries, regions, or other structures, and then described using features such as **area, perimeter, shape, texture, or color**.

## 2. Image Representation

An image can be represented in several ways depending on the application.

The major forms of image representation are:

1. **Boundary representation**
2. **Region representation**
3. **Skeleton representation**
4. **Hierarchical representation**
5. **Feature-based representation**

The choice of representation depends on whether the application is primarily concerned with the **shape, region, structure, or appearance** of an object.

### 2.1 Boundary Representation

In boundary representation, only the **boundary or contour of an object** is represented.

Instead of storing all pixels belonging to an object, the system stores the pixels or coordinates that form its boundary.

For example:

```text
      ● ● ● ●
    ●         ●
   ●           ●
   ●           ●
    ●         ●
      ● ● ● ●
```

Here, only the outer contour is required to describe the object.

#### Common boundary representations

* Chain codes
* Polygonal approximation
* Boundary segments
* Signatures
* Fourier descriptors

#### Advantages

* Requires less data than complete region representation.
* Useful for shape analysis.
* Efficient for recognizing objects based primarily on their outlines.

#### Limitations

* Does not directly describe the interior of an object.
* Sensitive to noise and irregular boundaries.
* Not suitable when internal texture or intensity information is important.

#### Applications

Boundary representation is commonly used in:

* Character recognition
* Shape recognition
* Industrial inspection
* Object detection
* Contour analysis

### 2.2 Region Representation

In region representation, **all pixels belonging to an object or region** are represented.

If an object is segmented from its background, its complete set of pixels can be represented as a region.

Mathematically, a region (R) can be represented as:

$$
R = {(x,y) \mid f(x,y) \text{ satisfies a specified property}}
$$

where $f(x,y)$ represents the image intensity.

For a binary image:

$$
f(x,y)=
\begin{cases}
1, & \text{object}\
0, & \text{background}
\end{cases}
$$

#### Examples of region representation

* Binary masks
* Region boundaries
* Region adjacency structures
* Run-length representations
* Quadtree representations

#### Advantages

* Contains complete information about the object region.
* Useful for analyzing area, texture, and intensity.
* Suitable for objects where internal properties are important.

#### Limitations

* Requires more storage than boundary representation.
* Processing can be computationally expensive for large regions.

#### Applications

* Medical image analysis
* Satellite image analysis
* Character segmentation
* Object classification
* Image segmentation

### 2.3 Skeleton Representation

A **skeleton** is a thin, simplified representation of an object that preserves its basic structural properties.

The skeleton is obtained by reducing an object to approximately **one-pixel-wide central lines** while preserving its topology.

For example:

```text
Original object:

     █████
    ███████
   █████████
    ███████
     █████

Skeleton:

      │
      │
──────┼──────
      │
      │
```

Skeletonization is useful because it preserves the object's:

* Connectivity
* Branching structure
* General shape
* Topological properties

#### Applications

Skeleton representation is particularly useful in:

* Handwritten character recognition
* Fingerprint analysis
* Road-network extraction
* Shape analysis
* Biological structure analysis

### 2.4 Hierarchical Representation

Some images contain objects composed of **smaller parts**, and these parts may themselves contain subparts.

In such cases, a hierarchical representation can be used.

For example:

```text
Image
  │
  ├── Object A
  │     ├── Part A1
  │     └── Part A2
  │
  └── Object B
        ├── Part B1
        └── Part B2
```

This type of representation is useful when the **relationship between objects and their components** is important.

#### Applications

* Scene understanding
* Computer vision
* Object recognition
* Image interpretation
* 3-D object modeling

## 3. Image Description

Once an object has been represented, useful characteristics called **features** are extracted from it.

These features form the **description** of the object.

A feature should ideally be:

* Distinctive
* Robust to noise
* Computationally efficient
* Relatively invariant to translation, rotation, and scaling when required

For example, an object can be described using:

$$
\text{Object Description} = \{\text{Area, Perimeter, Shape, Texture, Color, etc.}\}
$$

## 4. Types of Image Descriptors

Image descriptors can broadly be classified into:

1. **Boundary descriptors**
2. **Region descriptors**
3. **Texture descriptors**
4. **Color descriptors**
5. **Statistical descriptors**
6. **Structural descriptors**

## 5. Boundary Descriptors

Boundary descriptors describe an object using information obtained from its contour.

Important boundary descriptors include:

### a. Chain Code

A chain code represents a boundary as a sequence of **directions** between consecutive boundary pixels.

For example, using 4-directional chain coding:

```text
       1
       ↑
   2 ← • → 0
       ↓
       3
```

A boundary can then be represented as:

$$
C = [0,0,1,1,2,2,3,3,\ldots]
$$

Chain codes are useful for:

* Shape representation
* Character recognition
* Contour analysis

### b. Polygonal Approximation

A complex boundary can be approximated using a smaller number of **straight-line segments**.

Instead of storing hundreds of boundary points, the system stores important corner or turning points.

For example:

```text
Complex contour:

~~~~~~~~~~~~~~~~~~~~

Polygon approximation:

   /──────\
  /        \
  \        /
   \──────/
```

This reduces the amount of data required to represent the shape.

### c. Fourier Descriptors

A boundary can also be represented mathematically using **Fourier descriptors**.

The boundary coordinates are treated as a periodic signal and transformed into the frequency domain using the Fourier transform.

The resulting coefficients describe the shape.

A general representation can be written as:

$$
F(u)=\sum_{n=0}^{N-1}z(n)e^{-j2\pi un/N}
$$

where:

* $z(n)$ represents boundary coordinates.
* $N$ is the number of boundary points.
* $F(u)$ represents Fourier descriptors.

Fourier descriptors are useful because they can provide compact representations of complex shapes.

## 6. Region Descriptors

Region descriptors describe the **entire area occupied by an object** rather than only its boundary.

Important region descriptors include:

### 6.1 Area

Area represents the number of pixels belonging to an object.

For a binary image:

$$
A = \sum_{(x,y)\in R}1
$$

Thus, area is simply the total number of object pixels.

### 6.2 Perimeter

Perimeter represents the length of the object's boundary.

For a digital image, it can be estimated by counting boundary pixels or calculating distances between consecutive boundary points.

Perimeter is useful for distinguishing objects having similar areas but different shapes.

### 6.3 Centroid

The centroid represents the **geometric center** of an object.

For a binary region:

$$
\bar{x}=\frac{1}{A}\sum_{(x,y)\in R}x
$$

$$
\bar{y}=\frac{1}{A}\sum_{(x,y)\in R}y
$$

Therefore, the centroid is:

$$
C=(\bar{x},\bar{y})
$$

The centroid is widely used for:

* Object localization
* Shape analysis
* Tracking
* Pattern recognition

### 6.4 Compactness

Compactness measures how closely an object's shape resembles a compact or circular shape.

A commonly used measure is:

$$
C=\frac{P^2}{4\pi A}
$$

where:

* $P$ = perimeter
* $A$ = area

For a perfect circle:

$$
C=1
$$

Objects with irregular or elongated boundaries generally have larger values.

### 6.5 Eccentricity

Eccentricity indicates how elongated an object is.

It is commonly derived from the major and minor axes of an object's equivalent ellipse.

A general expression is:

$$
e=\sqrt{1-\frac{b^2}{a^2}}
$$

where:

* $a$ = semi-major axis
* $b$ = semi-minor axis

For a circle:

$$
e=0
$$

For a highly elongated object, (e) approaches:

$$
1
$$

## 7. Texture Description

**Texture** describes the spatial arrangement and variation of intensity or color within an image region.

Examples include:

* Smooth surfaces
* Rough surfaces
* Repeated patterns
* Fabric
* Grass
* Wood
* Brick walls

Texture descriptors can be based on:

* Statistical methods
* Structural methods
* Transform-based methods

A common statistical approach uses the **Gray-Level Co-occurrence Matrix (GLCM)**.

From the GLCM, features such as:

* Contrast
* Energy
* Homogeneity
* Correlation

can be calculated.

Texture information is particularly important when two objects have similar shapes but different surface patterns.

## 8. Color Description

Color can also be used as an important image descriptor.

Common color spaces include:

* RGB
* HSV
* HSI
* YCbCr

A color descriptor may contain:

* Color histogram
* Mean color
* Color moments
* Dominant colors

### Color Histogram

A color histogram represents the distribution of colors in an image.

For grayscale images, it represents the frequency of different intensity levels.

For example:

$$
H(k)=n_k
$$

where $n_k$ represents the number of pixels having intensity level (k).

Color descriptors are widely used in:

* Image retrieval
* Object recognition
* Image classification
* Face detection
* Video analysis

## 9. Statistical Descriptors

Statistical descriptors summarize numerical properties of image pixels.

Common statistical features include:

### Mean

$$
\mu=\frac{1}{N}\sum_{i=1}^{N}x_i
$$

It represents the average intensity.

### Variance

$$
\sigma^2=\frac{1}{N}\sum_{i=1}^{N}(x_i-\mu)^2
$$

It represents the degree of intensity variation.

### Standard Deviation

$$
\sigma=\sqrt{\sigma^2}
$$

It indicates the spread of intensity values.

Other statistical descriptors include:

* Skewness
* Kurtosis
* Entropy
* Higher-order moments

## 10. Structural Description

Structural description represents an object according to its **parts and the relationships among those parts**.

For example, a human face can be described as:

```text
Face
 ├── Two Eyes
 ├── Nose
 └── Mouth
```

The relationships between these components provide important information for recognition.

Structural descriptions are useful when:

* Objects have meaningful components.
* The relationship between parts is important.
* Shape alone is insufficient for recognition.

Applications include:

* Character recognition
* Face recognition
* Scene interpretation
* Object recognition

## 11. Representation vs Description

| Aspect | Image Representation | Image Description |
| --- | --- | --- |
| Meaning  | Defines how an image/object is represented | Defines characteristics of the represented object |
| Purpose  | Provides a suitable form for processing    | Extracts meaningful features                      |
| Examples | Boundary, region, skeleton                 | Area, perimeter, texture, color                   |
| Focus    | Structure/form of the object               | Properties/features of the object                 |
| Output   | Mathematical or structural representation  | Feature vector or descriptor                      |
| Used for | Further image analysis                     | Classification and recognition                    |

### Simple way to remember

> **Representation tells us “how to store the object.”**
> **Description tells us “how to characterize the object.”**

## 12. Feature Vector

The extracted descriptors can be combined into a **feature vector**.

For example, an object may be represented by:

$$
\mathbf{F}=
[A,P,C,e,\mu,\sigma]
$$

where:

* $A$ = Area
* $P$ = Perimeter
* $C$ = Compactness
* $e$ = Eccentricity
* $\mu$ = Mean intensity
* $\sigma$ = Standard deviation

The feature vector can then be provided to a classification or recognition algorithm.

A typical processing pipeline is:

```text
Input Image
     ↓
Preprocessing
     ↓
Segmentation
     ↓
Object Representation
     ↓
Feature Extraction
     ↓
Feature Vector
     ↓
Classification / Recognition
```

This pipeline is fundamental to many computer vision systems.

## 13. Properties of a Good Image Descriptor

A good image descriptor should ideally possess the following properties:

### 1. Distinctiveness

It should effectively distinguish different objects.

### 2. Robustness

It should not change significantly due to noise or small image variations.

### 3. Invariance

Where required, the descriptor should remain stable under:

* Translation
* Rotation
* Scaling
* Illumination changes

### 4. Compactness

The descriptor should represent the object using a relatively small amount of data.

### 5. Computational Efficiency

Feature extraction should be fast enough for the intended application.

### 6. Reliability

The descriptor should provide consistent results for similar objects.

## 14. Applications

Image representation and description are fundamental to many computer vision applications:

* **Object recognition**
* **Face recognition**
* **Fingerprint recognition**
* **Optical Character Recognition (OCR)**
* **Medical image analysis**
* **Industrial quality inspection**
* **Remote sensing**
* **Image retrieval**
* **Autonomous vehicles**
* **Robotics**
* **Surveillance systems**

For example, in medical imaging, a tumor can be represented as a segmented region and described using features such as **area, shape, texture, and intensity**.

## Key Points

* **Image representation** converts an image/object into a suitable mathematical or structural form.
* **Image description** extracts meaningful features from the represented object.
* Boundary representation focuses on the **outline** of an object.
* Region representation considers the **complete object region**.
* Skeleton representation provides a simplified **structural form** of an object.
* Important shape descriptors include **area, perimeter, centroid, compactness, and eccentricity**.
* **Chain codes** represent boundaries using directional information.
* **Fourier descriptors** represent object boundaries using frequency-domain information.
* Texture descriptors characterize the **surface or intensity pattern** of an image.
* Color descriptors characterize the **color distribution**.
* Extracted features can be combined into a **feature vector** for classification and recognition.
* A good descriptor should ideally be **distinctive, robust, invariant, compact, and computationally efficient**.

### One-line definition

> **Image representation and description is the process of representing an image or object in a suitable form and extracting meaningful features such as shape, texture, color, and statistical properties for subsequent analysis, classification, and recognition.**

This gives us a solid **professional, university-exam-oriented foundation** for **Image Representation and Description**. The natural next topic is **Object Recognition**, where these representations and descriptors are actually used to identify objects.
