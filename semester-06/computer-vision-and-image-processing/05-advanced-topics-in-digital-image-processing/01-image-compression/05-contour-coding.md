# 5.1.5 Contour Coding

## 1. Introduction

**Contour coding** is an image representation and compression technique in which the **boundary or contour of an object or region is encoded instead of representing all of its pixels individually**.

In many images, especially those containing distinct objects, the boundary contains most of the important information needed to describe the object's **shape, size, and structure**.

Instead of storing every pixel belonging to an object, contour coding represents the object using:

* Boundary points
* Boundary coordinates
* Directional information
* Chain codes
* Other compact boundary descriptions

### Core idea

> **Contour coding represents an object's boundary efficiently so that its shape can be stored or transmitted using fewer data.**

## 2. What is a Contour?

A **contour** is the boundary separating an object or region from its surrounding background.

For example, consider a binary image containing a simple object:

```text
000000000
000111000
001111100
001111100
000111000
000000000
```

The pixels represented by `1` form the object.

The **outer boundary** of these pixels is its contour.

Instead of storing every `1` pixel, contour coding can store only the information needed to describe this boundary.

## 3. Need for Contour Coding

Consider an object occupying a large region of an image.

If the object contains thousands of pixels, storing every pixel may require substantial data.

However, if the primary objective is to identify its **shape**, the complete interior may not be necessary.

For example, a simple circle can be represented using:

* Center coordinates
* Radius

rather than storing every pixel inside the circle.

Similarly, an arbitrary object can be represented using its boundary.

Thus:

$$
\boxed{
\text{Object Pixels}
\rightarrow
\text{Boundary Representation}
\rightarrow
\text{Reduced Data}
}
$$

Contour coding is particularly useful when **shape information is more important than pixel-level information**.

## 4. Contour Coding and Redundancy

Contour coding primarily reduces the amount of data needed to represent **object boundaries and shapes**.

It is especially effective for images where:

* Objects occupy large areas.
* Objects have relatively simple boundaries.
* The interior of objects contains little useful information.
* Shape is the main feature of interest.

It is therefore closely related to **shape representation and boundary description**.

## 5. Basic Contour Coding Process

A typical contour coding process consists of the following stages:

```text id="9u2p9r"
Input Image
     ↓
Segmentation
     ↓
Identify Object/Region
     ↓
Extract Boundary
     ↓
Represent Boundary
     ↓
Encode Contour
     ↓
Compressed Contour Data
```

### Step 1: Segmentation

The image is divided into meaningful regions or objects.

### Step 2: Boundary Detection

The boundary of the selected object is identified.

### Step 3: Boundary Representation

The contour is represented using an appropriate representation method.

### Step 4: Encoding

The representation is encoded into a compact form.

## 6. Chain Coding

One of the most important techniques used in contour coding is **chain coding**.

Chain coding represents a contour as a sequence of **directions** between successive boundary pixels.

Instead of storing the coordinates of every boundary point, the direction of movement from one boundary pixel to the next is stored.

This can significantly reduce the amount of information required.

## 7. Freeman Chain Code

The **Freeman chain code** is a well-known method for representing object boundaries.

It represents movement between neighboring pixels using a numerical direction code.

There are two common versions:

1. **4-connected chain code**
2. **8-connected chain code**

### 7.1 4-Connected Chain Code

In a 4-connected system, movement is allowed in four directions:

```text id="4xg1g4"
       0
       ↑
  3 ← P → 1
       ↓
       2
```

A possible numbering convention is:

| Direction | Code |
| --- | ---: |
| Right     |    1 |
| Down      |    2 |
| Left      |    3 |
| Up        |    0 |

Thus, a contour can be represented as a sequence such as:

$$
1,1,2,2,3,3,0,0
$$

The exact numerical direction convention may vary depending on the implementation.

## 8. 8-Connected Chain Code

In an 8-connected system, diagonal movement is also allowed.

A common representation is:

```text id="1m6g0m"
        3   2   1
         \  ↑  /
          \ | /
        4 ← P → 0
          / | \
         /  ↓  \
        5   6   7
```

Thus, the eight possible directions are represented by eight codes.

| Direction   | Example Code |
| --- | ---: |
| Right       |            0 |
| Upper-right |            1 |
| Up          |            2 |
| Upper-left  |            3 |
| Left        |            4 |
| Lower-left  |            5 |
| Down        |            6 |
| Lower-right |            7 |

Again, the exact starting direction and numbering convention may differ.

### Advantage

8-connected chain coding can represent diagonal boundaries more naturally than 4-connected coding.

## 9. Example of Chain Coding

Suppose an object boundary consists of the following movements:

$$
\text{Right} \rightarrow
\text{Right} \rightarrow
\text{Down} \rightarrow
\text{Down} \rightarrow
\text{Left}
$$

Using a suitable directional coding scheme, this boundary can be stored as:

$$
\boxed{0,0,6,6,4}
$$

rather than storing the complete coordinates of every boundary pixel.

The sequence of directions completely describes the contour once the **starting point** is known.

Therefore, a chain code generally requires:

1. Starting point
2. Sequence of directions

## 10. Boundary Representation

A contour can be represented in several ways.

### 10.1 Boundary Coordinates

Store the coordinates:

$$
(x_1,y_1),(x_2,y_2),\ldots,(x_n,y_n)
$$

for boundary points.

This is simple but may require significant storage.

### 10.2 Chain Code

Store the starting point and the sequence of movement directions.

$$
\boxed{
\text{Start Point}+\text{Direction Sequence}
}
$$

This is generally more compact.

### 10.3 Polygonal Approximation

A complex contour can be approximated using a smaller number of line segments.

For example, a boundary can be represented by:

```text
P1 -> P2 -> P3 -> P4 -> P1
```

instead of storing every boundary pixel.

This is particularly useful when the contour is approximately polygonal.

### 10.4 Parametric Representation

Some contours can be represented mathematically using parameters.

For example, a circle can be described using:

$$
(x-a)^2+(y-b)^2=r^2
$$

where:

* $(a,b)$ = center
* $r$ = radius

This can provide an extremely compact representation for regular shapes.

## 11. Differential Chain Coding

Chain codes can themselves contain redundancy.

For example, a contour that moves mostly in the same direction may contain long sequences of identical codes.

A further compression step can therefore be applied.

One approach is to encode **changes in direction** rather than the absolute direction.

This is called **differential chain coding**.

Instead of:

$$
2,2,2,3,3,3,4,4
$$

the encoder can represent changes between successive directions.

This can make the contour representation more compact and less dependent on the absolute orientation.

## 12. Starting Point Problem

A chain code depends on the point at which the contour traversal begins.

Suppose the same contour is traversed from different starting points.

The resulting chain-code sequences may be different even though the shape is identical.

For example:

$$
1,2,3,4,1,2
$$

and

$$
3,4,1,2,1,2
$$

may represent the same contour with different starting positions.

Therefore, the starting point must be handled carefully.

### Possible solutions

* Specify a standard starting point.
* Normalize the starting point.
* Use a canonical representation.
* Use a representation based on relative direction changes.

## 13. Rotation and Scale Considerations

A contour representation may change when the object is:

* Rotated
* Scaled
* Translated

For many image-analysis applications, we want the representation to be independent of these transformations.

### Translation

Translation changes the absolute coordinates but does not change the relative shape.

Chain codes are naturally less dependent on absolute position once the starting point is known.

### Rotation

Rotation can change the directional codes.

Differential chain codes can help make the representation more robust to rotation.

### Scale

Changing the size of an object changes the number of boundary pixels and therefore may affect the chain code.

Additional normalization techniques can be used when scale invariance is required.

## 14. Contour Coding vs. Region Coding

Contour coding represents primarily the **boundary**, whereas region-based representation considers the **entire object or region**.

| Feature | Contour Coding | Region Representation |
| --- | --- | --- |
| Main information | Boundary                             | Entire region                         |
| Focus            | Shape                                | Shape + interior                      |
| Data requirement | Often lower                          | Usually higher                        |
| Useful for       | Shape analysis                       | Complete object representation        |
| Common methods   | Chain codes, polygonal approximation | Region descriptors, run-based methods |

Contour coding is particularly effective when the interior of the object does not contain important information.

## 15. Advantages of Contour Coding

1. **Compact representation of object boundaries.**
2. Reduces the need to store every object pixel.
3. Preserves important shape information.
4. Useful for object recognition.
5. Useful for pattern recognition.
6. Efficient for objects with simple or smooth boundaries.
7. Chain codes are relatively simple to implement.
8. Can be combined with other compression methods.

## 16. Limitations of Contour Coding

1. It does not preserve complete information about the object's interior.
2. Complex boundaries may require long chain codes.
3. Noise can create irregular boundaries and increase the representation size.
4. Chain codes may depend on the starting point.
5. Rotation and scale may require normalization.
6. Not suitable when the internal texture or pixel intensity information is important.
7. Boundary extraction itself may require segmentation and edge-detection operations.

## 17. Applications of Contour Coding

Contour coding is useful in applications where **shape and boundary information** are important.

### Major applications include:

* **Object recognition**
* **Pattern recognition**
* **Character recognition**
* **Shape analysis**
* **Image segmentation**
* **Medical image analysis**
* **Industrial inspection**
* **Computer vision**
* **Document analysis**
* **Geometric image processing**

For example, in character recognition, the contour of a character can provide important information for distinguishing between different characters.

## 18. Contour Coding in Object Recognition

Contour information is particularly useful in object recognition.

A typical system can operate as follows:

$$
\boxed{
\text{Image}
\rightarrow
\text{Segmentation}
\rightarrow
\text{Contour Extraction}
\rightarrow
\text{Contour Description}
\rightarrow
\text{Feature Extraction}
\rightarrow
\text{Object Recognition}
}
$$

The contour can provide features such as:

* Shape
* Curvature
* Boundary length
* Corners
* Direction changes
* Symmetry

These features can then be compared with known object models.

## 19. Contour Coding vs. Spatial Compression

These concepts should be distinguished.

| Spatial Compression | Contour Coding |
| --- | --- |
| Exploits neighboring pixel relationships          | Represents object boundaries                   |
| Primarily addresses spatial/interpixel redundancy | Primarily describes shape/boundary information |
| Works directly with pixel relationships           | Works with extracted contours                  |
| Can represent the entire image                    | Usually represents selected object boundaries  |
| Examples: predictive coding, DPCM                 | Chain codes, polygonal approximation           |

Contour coding can, however, be considered a specialized way of representing image information efficiently.

## Important Terms

| Term | Meaning |
| --- | --- |
| **Contour**                 | Boundary of an object or region                                 |
| **Contour Coding**          | Compact encoding of an object's boundary                        |
| **Chain Code**              | Represents a contour using directional movements                |
| **Freeman Chain Code**      | Standard directional chain-code representation                  |
| **4-Connected**             | Allows horizontal and vertical movements                        |
| **8-Connected**             | Allows horizontal, vertical, and diagonal movements             |
| **Starting Point**          | Point from which contour traversal begins                       |
| **Differential Chain Code** | Represents changes in direction rather than absolute directions |
| **Polygonal Approximation** | Represents a contour using a smaller number of line segments    |

## Summary

**Contour coding** is a technique for representing an object by encoding its **boundary or contour** rather than storing all of its pixels.

The basic process is:

$$
\boxed{
\text{Image}
\rightarrow
\text{Object Extraction}
\rightarrow
\text{Boundary Detection}
\rightarrow
\text{Contour Representation}
\rightarrow
\text{Encoding}
}
$$

The most important contour representation technique is **chain coding**, particularly the **Freeman chain code**.

Chain coding represents the boundary using a sequence of directions between neighboring boundary pixels.

Two common forms are:

* **4-connected chain code** — four possible directions.
* **8-connected chain code** — eight possible directions, including diagonals.

A contour can also be represented using:

* Boundary coordinates
* Chain codes
* Differential chain codes
* Polygonal approximations
* Parametric representations

### One-line definition

> **Contour coding is an image representation and compression technique that encodes the boundary of an object using a compact representation such as chain codes, thereby reducing the data required to describe the object's shape.**

### Key point to remember

$$
\boxed{
\text{Contour Coding}
\rightarrow
\text{Boundary Information}
\rightarrow
\text{Compact Shape Representation}
}
$$
