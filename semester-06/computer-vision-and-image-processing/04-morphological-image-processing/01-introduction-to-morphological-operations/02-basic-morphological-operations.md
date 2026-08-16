# 4.1.2 Basic Morphological Operations

Basic morphological operations are fundamental techniques used in **morphological image processing** to analyze and modify the shape and structure of objects in an image.

The two primary morphological operations are:

1. **Erosion**
2. **Dilation**

These operations form the foundation for more advanced operations such as **opening and closing**.

## 1. Erosion

### Definition

**Erosion** is a morphological operation that reduces the size of foreground objects by removing pixels from their boundaries.

It is represented mathematically as:

$$
\boxed{A \ominus B}
$$

where:

* $A$ = input image
* $B$ = structuring element
* $\ominus$ = erosion operator

### Basic Principle

During erosion, the structuring element is moved across the image. A foreground pixel remains in the output only when the structuring element **fits completely within the foreground region**.

For a binary image:

* If the structuring element fits -> output pixel is **1**
* If it does not fit -> output pixel is **0**

### Example

Consider the following binary image:

$$
A=
\begin{bmatrix}
0&0&0&0&0\
0&1&1&1&0\
0&1&1&1&0\
0&1&1&1&0\
0&0&0&0&0
\end{bmatrix}
$$

Using a (3\times3) structuring element:

$$
B=
\begin{bmatrix}
1&1&1\
1&1&1\
1&1&1
\end{bmatrix}
$$

only the central pixel has a complete $3\times3$ neighborhood of foreground pixels. Therefore, the object becomes smaller:

$$
A\ominus B=
\begin{bmatrix}
0&0&0&0&0\
0&0&0&0&0\
0&0&1&0&0\
0&0&0&0&0\
0&0&0&0&0
\end{bmatrix}
$$

### Effects of Erosion

Erosion:

* Shrinks foreground objects
* Removes boundary pixels
* Removes small isolated objects
* Removes thin protrusions
* Breaks narrow connections between objects
* Increases the separation between nearby objects
* Can eliminate small noise components

### Applications of Erosion

Erosion is commonly used for:

* Noise removal
* Separating connected objects
* Removing small objects
* Extracting object skeleton-like structures
* Reducing the size of foreground regions

### Important Point

> **Erosion generally makes foreground objects smaller or thinner.**

## 2. Dilation

### Definition

**Dilation** is a morphological operation that increases the size of foreground objects by adding pixels to their boundaries.

It is represented mathematically as:

$$
\boxed{A \oplus B}
$$

where:

* $A$ = input image
* $B$ = structuring element
* $\oplus$ = dilation operator

### Basic Principle

During dilation, the structuring element is moved across the image. A pixel becomes part of the foreground when the structuring element **overlaps the foreground region**.

For a binary image:

* If the structuring element overlaps the object -> output pixel becomes **1**
* Otherwise → output pixel remains **0**

### Example

Consider:

$$
A=
\begin{bmatrix}
0&0&0&0&0\
0&0&1&0&0\
0&0&1&0&0\
0&0&0&0&0\
0&0&0&0&0
\end{bmatrix}
$$

Using a suitable $3\times3$ structuring element, dilation expands the object:

$$
A\oplus B=
\begin{bmatrix}
0&1&1&1&0\
0&1&1&1&0\
0&1&1&1&0\
0&1&1&1&0\
0&0&0&0&0
\end{bmatrix}
$$

The exact result depends on the **shape, size, and origin** of the structuring element.

### Effects of Dilation

Dilation:

* Expands foreground objects
* Adds pixels to object boundaries
* Fills small gaps
* Fills small holes or breaks
* Connects nearby objects
* Strengthens thin structures
* Can increase the size of small objects

### Applications of Dilation

Dilation is commonly used for:

* Connecting broken components
* Filling small gaps
* Repairing broken shapes
* Joining nearby objects
* Strengthening thin lines
* Expanding regions of interest

### Important Point

> **Dilation generally makes foreground objects larger or thicker.**

## 3. Comparison Between Erosion and Dilation

| Feature         | Erosion                  | Dilation               |
| --- | --- | --- |
| Symbol          | (A\ominus B)             | (A\oplus B)            |
| Main effect     | Shrinks objects          | Expands objects        |
| Boundary        | Moves inward             | Moves outward          |
| Foreground area | Decreases                | Increases              |
| Thin structures | May disappear            | May become thicker     |
| Small objects   | May be removed           | May become larger      |
| Narrow gaps     | Become larger            | Become smaller         |
| Nearby objects  | May be separated         | May be connected       |
| Main use        | Remove/reduce structures | Add/connect structures |

### Easy way to remember

$$
\boxed{\text{Erosion} \rightarrow \text{Shrink}}
$$

$$
\boxed{\text{Dilation} \rightarrow \text{Grow}}
$$

## 4. Structuring Element in Basic Operations

The **structuring element (SE)** determines how erosion and dilation affect the image.

Common structuring elements include:

### Square

$$
\begin{bmatrix}
1&1&1\
1&1&1\
1&1&1
\end{bmatrix}
$$

### Cross

$$
\begin{bmatrix}
0&1&0\
1&1&1\
0&1&0
\end{bmatrix}
$$

### Horizontal Line

$$
\begin{bmatrix}
1&1&1&1&1
\end{bmatrix}
$$

### Vertical Line

$$
\begin{bmatrix}
1\
1\
1\
1\
1
\end{bmatrix}
$$

The structuring element should be selected according to the **shape and orientation of the features** that need to be processed.

## 5. Role of the Origin of a Structuring Element

A structuring element generally has a designated **origin (or anchor point)**.

For example:

$$
B=
\begin{bmatrix}
1&1&1\
1&\boxed{1}&1\
1&1&1
\end{bmatrix}
$$

The center pixel is the origin.

As the structuring element moves over the image, the origin determines which input-image location corresponds to the output pixel being processed.

The location of the origin can affect the result, particularly for asymmetric structuring elements.

## 6. Basic Operations on Grayscale Images

Erosion and dilation can also be applied to grayscale images.

For a grayscale image $f(x,y)$, erosion is generally associated with a **minimum operation**, while dilation is generally associated with a **maximum operation**.

### Grayscale Erosion

$$
(f\ominus B)(x,y) = \min_{(s,t)\in B} f(x-s,y-t)
$$

Thus, grayscale erosion tends to produce darker regions and suppress bright structures.

### Grayscale Dilation

$$
(f\oplus B)(x,y) = \max_{(s,t)\in B} f(x-s,y-t)
$$

Thus, grayscale dilation tends to produce brighter regions and enhance bright structures.

### Key Relationship

$$
\boxed{\text{Grayscale Erosion} \rightarrow \text{Minimum}}
$$

$$
\boxed{\text{Grayscale Dilation} \rightarrow \text{Maximum}}
$$

## 7. Geometric Interpretation

Morphological operations can be understood intuitively in terms of object shape.

### Erosion

Imagine shrinking an object by removing a thin layer from its boundary.

**Effect:**

$$
\text{Large Object}
\quad\longrightarrow\quad
\text{Smaller Object}
$$

### Dilation

Imagine expanding an object by adding a thin layer around its boundary.

**Effect:**

$$
\text{Small Object}
\quad\longrightarrow\quad
\text{Larger Object}
$$

This geometric interpretation makes morphological operations particularly useful for **shape analysis**.

## 8. Practical Example

Suppose a binary image contains two objects connected by a very thin bridge:

```text
████      ████
██████████████
    ████████
```

### Applying erosion

The thin connecting bridge may disappear:

```text
████      ████
████      ████
```

Thus, **erosion can separate connected objects**.

### Applying dilation

If two objects are close but separated by a small gap:

```text
████      ████
████      ████
```

dilation may expand them until they touch:

```text
██████████████
██████████████
```

Thus, **dilation can connect nearby objects**.

## 9. Important Properties

### Erosion

For a binary image, erosion generally satisfies:

$$
A\ominus B \subseteq A
$$

This means the eroded object is generally contained within the original object.

### Dilation

Similarly:

$$
A \subseteq A\oplus B
$$

This means the dilated object generally contains the original object.

These relationships explain why erosion decreases foreground regions while dilation increases them.

## 10. Common Applications

| Application                   | Operation commonly used |
| --- | --- |
| Remove small foreground noise | Erosion                 |
| Separate connected objects    | Erosion                 |
| Remove thin protrusions       | Erosion                 |
| Connect broken components     | Dilation                |
| Fill small gaps               | Dilation                |
| Strengthen thin structures    | Dilation                |
| Reduce object size            | Erosion                 |
| Increase object size          | Dilation                |

## 11. Erosion and Dilation as Building Blocks

Erosion and dilation are not only useful individually; they are also used to construct more advanced morphological operations.

### Opening

Opening is performed by:

$$
\boxed{A\circ B=(A\ominus B)\oplus B}
$$

It consists of:

**Erosion => Dilation**

Opening is generally useful for removing small objects and noise while preserving the general shape of larger objects.

### Closing

Closing is performed by:

$$
\boxed{A\bullet B=(A\oplus B)\ominus B}
$$

It consists of:

**Dilation => Erosion**

Closing is generally useful for filling small gaps and holes and connecting nearby regions.

These operations will be discussed in detail under **Morphological Transformations**.

## Summary

The basic morphological operations are **erosion and dilation**.

* **Erosion** removes pixels from object boundaries and generally **shrinks foreground objects**.
* **Dilation** adds pixels to object boundaries and generally **expands foreground objects**.
* Both operations use a **structuring element**.
* The size and shape of the structuring element determine the nature of the transformation.
* In grayscale morphology:

  * Erosion is associated with a **minimum** operation.
  * Dilation is associated with a **maximum** operation.
* Erosion and dilation are the fundamental building blocks for **opening and closing**.

### Quick Revision

$$
\boxed{\text{Erosion} = \text{Shrink / Remove}}
$$

$$
\boxed{\text{Dilation} = \text{Grow / Connect}}
$$

$$
\boxed{\text{Opening} = \text{Erosion + Dilation}}
$$

$$
\boxed{\text{Closing} = \text{Dilation + Erosion}}
$$
