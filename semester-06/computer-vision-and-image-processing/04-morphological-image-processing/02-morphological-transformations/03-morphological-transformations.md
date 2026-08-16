# 4.2.3 Morphological Transformations

## 1. Introduction

**Morphological transformations** are image processing techniques that analyze and modify the **shape, structure, boundaries, and geometric properties of objects** in an image using a **structuring element**.

Mathematical morphology is primarily based on the interaction between an image and a small predefined pattern called a **structuring element (SE)**.

Morphological transformations are especially useful for:

* Removing noise.
* Extracting object boundaries.
* Detecting specific shapes or structures.
* Filling holes and gaps.
* Separating or connecting objects.
* Extracting important features from images.
* Preparing images for segmentation and object recognition.

## 2. Basic Concept

Morphological processing treats an image as a **set of pixels** and applies operations based on the spatial relationship between pixels.

For a binary image:

* **Foreground pixels** are usually represented by $1$.
* **Background pixels** are usually represented by $0$.

A structuring element is moved across the image, and its interaction with the image determines the output.

The two fundamental morphological operations are:

$$
\boxed{\text{Erosion}}
$$

and

$$
\boxed{\text{Dilation}}
$$

Most other morphological transformations can be constructed from these two operations.

## 3. Structuring Element

A **structuring element (SE)** is a small binary pattern used to probe or modify an image.

For example, a $3\times3$ square structuring element can be represented as:

```text
1 1 1
1 1 1
1 1 1
```

Another example is a cross-shaped structuring element:

```text
0 1 0
1 1 1
0 1 0
```

The choice of structuring element affects the result of a morphological transformation.

### Common Structuring Elements

| Shape       | Typical Use                                  |
| --- | --- |
| Square      | General-purpose processing                   |
| Rectangle   | Directional structures                       |
| Circle/Disk | Rounded objects                              |
| Cross       | Connectivity-related operations              |
| Line        | Detecting or processing directional features |

## 4. Fundamental Morphological Transformations

The major morphological transformations include:

1. **Erosion**
2. **Dilation**
3. **Opening**
4. **Closing**
5. **Morphological Gradient**
6. **Top-Hat Transformation**
7. **Black-Hat Transformation**
8. **Hit-or-Miss Transformation**

The first four are the basic operations, while the others are derived transformations used for feature extraction and shape analysis.

## 5. Erosion

**Erosion** reduces or shrinks foreground regions of an image.

It is represented as:

$$
\boxed{A\ominus B}
$$

where $A$ is the image and $B$ is the structuring element.

### Effects of Erosion

* Shrinks objects.
* Removes small foreground objects.
* Removes thin protrusions.
* Breaks narrow connections.
* Makes boundaries move inward.

Conceptually:

```text
Large Object
    ↓
  Erosion
    ↓
Smaller Object
```

Erosion is also the first operation in **opening**.

## 6. Dilation

**Dilation** expands or grows foreground regions.

It is represented as:

$$
\boxed{A\oplus B}
$$

### Effects of Dilation

* Enlarges objects.
* Fills small gaps.
* Connects nearby components.
* Expands object boundaries.
* Strengthens thin structures.

Conceptually:

```text
Small Object
    ↓
  Dilation
    ↓
Larger Object
```

Dilation is the first operation in **closing**.

## 7. Opening

Opening is obtained by applying **erosion followed by dilation**.

$$
\boxed{A\circ B=(A\ominus B)\oplus B}
$$

### Main purpose

Opening is mainly used to:

* Remove small foreground objects.
* Remove noise.
* Eliminate thin protrusions.
* Smooth boundaries.
* Break narrow connections.

### Memory Rule

> **Opening = Erosion -> Dilation = Remove**

## 8. Closing

Closing is obtained by applying **dilation followed by erosion**.

$$
\boxed{A\bullet B=(A\oplus B)\ominus B}
$$

### Main purpose

Closing is mainly used to:

* Fill small holes.
* Fill small gaps.
* Connect nearby objects.
* Remove small boundary indentations.
* Smooth contours.

### Memory Rule

> **Closing = Dilation -> Erosion = Fill**

## 9. Morphological Gradient

The **morphological gradient** is used primarily for **detecting object boundaries**.

It is obtained by subtracting the eroded image from the dilated image:

$$
\boxed{G=(A\oplus B)-(A\ominus B)}
$$

Where:

* $A\oplus B$ = dilated image
* $A\ominus B$ = eroded image
* $G$ = morphological gradient

### Working Principle

Dilation expands the boundary outward, while erosion moves the boundary inward.

The difference between them highlights the region around the object boundary.

```text
Original Image
      ↓
 ┌─────────────┐
 │ Dilation    │
 │      −      │
 │ Erosion     │
 └─────────────┘
      ↓
Object Boundary
```

### Applications

* Edge detection.
* Object boundary extraction.
* Shape analysis.
* Segmentation preprocessing.

## 10. Internal and External Morphological Gradients

The morphological gradient can also be divided into internal and external gradients.

### 10.1 Internal Gradient

The internal gradient is:

$$
\boxed{G_i=A-(A\ominus B)}
$$

It highlights the pixels near the **inside of the object boundary**.

### 10.2 External Gradient

The external gradient is:

$$
\boxed{G_e=(A\oplus B)-A}
$$

It highlights the pixels near the **outside of the object boundary**.

### 10.3 Basic Gradient

$$
\boxed{G=(A\oplus B)-(A\ominus B)}
$$

It emphasizes both sides of the boundary.

## 11. Top-Hat Transformation

The **Top-Hat transformation** is used to extract small bright structures from an image.

It is defined as:

$$
\boxed{T=A-(A\circ B)}
$$

where:

* $A$ = original image
* $A\circ B$ = opened image
* $T$ = Top-Hat result

### Principle

Opening removes small bright structures.

Therefore, subtracting the opened image from the original image leaves behind those small bright structures.

```text
Original Image
      −
Opened Image
      ↓
Small Bright Structures
```

### Applications

* Highlighting small bright objects.
* Background correction.
* Enhancing details.
* Uneven illumination correction.

## 12. Black-Hat Transformation

The **Black-Hat transformation** is used to extract small dark structures from an image.

It is defined as:

$$
\boxed{BH=(A\bullet B)-A}
$$

where:

* $A\bullet B$ = closed image
* $A$ = original image

### Principle

Closing fills small dark regions.

The difference between the closed image and the original image therefore highlights those dark regions.

```text
Closed Image
      −
Original Image
      ↓
Small Dark Structures
```

### Applications

* Detecting dark objects.
* Detecting cracks.
* Enhancing dark details.
* Correcting uneven illumination.
* Document processing.

## 13. Hit-or-Miss Transformation

The **Hit-or-Miss transformation** is a morphological operation used primarily for **detecting specific shapes or patterns** in binary images.

It is represented conceptually as:

$$
\boxed{A\otimes B}
$$

It uses a structuring element designed to match a particular configuration of foreground and background pixels.

A general formulation is:

$$
\boxed{A\otimes(B_1,B_2)
=(A\ominus B_1)\cap(A^c\ominus B_2)}
$$

where:

* $B_1$ identifies the required foreground pattern.
* $B_2$ identifies the required background pattern.
* $A^c$ is the complement of (A).

### Applications

* Shape detection.
* Pattern recognition.
* Corner detection.
* Skeletonization-related processing.
* Detection of specific binary configurations.

## 14. Relationship Between Morphological Transformations

The major transformations can be summarized as follows:

```text
                 Morphological Transformations
                           │
             ┌─────────────┴─────────────┐
             │                           │
       Basic Operations             Derived Operations
             │                           │
       ┌─────┴─────┐            ┌────────┼─────────┐
       │           │            │        │         │
   Erosion      Dilation     Opening  Closing   Gradient
                                  │
                         ┌────────┴────────┐
                         │                 │
                     Top-Hat           Black-Hat
```

## 15. Comparison of Major Morphological Transformations

| Transformation  | Formula                              | Main Purpose                    |
| --- | --- | --- |
| **Erosion**     | $A\ominus B$                         | Shrink objects                  |
| **Dilation**    | $A\oplus B$                          | Expand objects                  |
| **Opening**     | $(A\ominus B)\oplus B$               | Remove small objects/noise      |
| **Closing**     | $(A\oplus B)\ominus B$               | Fill holes and gaps             |
| **Gradient**    | $(A\oplus B)-(A\ominus B)$           | Extract boundaries              |
| **Top-Hat**     | $A-(A\circ B)$                       | Extract small bright structures |
| **Black-Hat**   | $(A\bullet B)-A$                     | Extract small dark structures   |
| **Hit-or-Miss** | $(A\ominus B_1)\cap(A^c\ominus B_2)$ | Detect specific patterns        |

# 16. Applications of Morphological Transformations

Morphological transformations are widely used in different computer vision applications.

### 16.1 Noise Removal

Opening can remove small unwanted foreground structures.

### 16.2 Hole Filling

Closing can fill small holes inside objects.

### 16.3 Boundary Detection

The morphological gradient can extract object boundaries.

### 16.4 Feature Extraction

Top-Hat and Black-Hat transformations can extract small bright and dark features.

### 16.5 Object Separation

Erosion and opening can help separate connected objects.

### 16.6 Object Connection

Dilation and closing can connect nearby or broken components.

### 16.7 Document Processing

Morphological operations can improve:

* Character recognition.
* Text segmentation.
* Removal of small artifacts.
* Repair of broken characters.

### 16.8 Medical Image Processing

Morphology can assist in extracting and analyzing anatomical structures from segmented images.

### 16.9 Industrial Inspection

Morphological transformations can be used to identify:

* Defects.
* Cracks.
* Holes.
* Surface irregularities.

## 17. Importance of Structuring Element

The structuring element is one of the most important factors in morphological processing.

The result depends on:

1. **Shape** of the structuring element.
2. **Size** of the structuring element.
3. **Orientation** of the structuring element.
4. **Application requirements**.

For example, a line-shaped structuring element can be useful for processing elongated structures, whereas a circular element may be more appropriate for rounded objects.

> **Important:** A poorly selected structuring element can remove useful information or produce undesirable changes in object shape.

## 18. Morphological Transformation Workflow

A typical morphological processing workflow can be represented as:

```text
Input Image
     ↓
Select Structuring Element
     ↓
Apply Morphological Operation
     ↓
Analyze Result
     ↓
Extract / Enhance Desired Features
     ↓
Output Image
```

The appropriate operation depends on the objective.

For example:

```text
Remove small noise      => Opening
Fill small holes        => Closing
Expand objects          => Dilation
Shrink objects          => Erosion
Detect boundaries       => Morphological Gradient
Extract bright details  => Top-Hat
Extract dark details    => Black-Hat
Detect specific shapes  => Hit-or-Miss
```

## 19. Important Properties

Several morphological transformations have useful mathematical properties.

### Opening

$$
\boxed{A\circ B\subseteq A}
$$

Opening is **anti-extensive**.

### Closing

$$
\boxed{A\subseteq A\bullet B}
$$

Closing is **extensive**.

### Both Opening and Closing

They are **increasing** and **idempotent** under the usual morphological definitions.

$$
\boxed{(A\circ B)\circ B=A\circ B}
$$

$$
\boxed{(A\bullet B)\bullet B=A\bullet B}
$$

These properties make opening and closing useful for controlled shape modification.

## 20. Practical Example

Suppose a binary image contains a scanned character with:

* Small isolated noise.
* A small hole.
* A broken boundary.

A suitable sequence could be:

```text
Original Character
       ↓
Opening
       ↓
Remove Small Noise
       ↓
Closing
       ↓
Fill Small Hole / Gap
       ↓
Morphological Gradient
       ↓
Extract Boundary
```

This demonstrates how multiple morphological transformations can be combined to solve a practical image-processing problem.

## 21. Key Differences: Opening, Closing and Gradient

| Feature          | Opening                    | Closing                       | Gradient           |
| --- | --- | --- | --- |
| Primary purpose  | Remove small structures    | Fill small structures         | Detect boundaries  |
| First operation  | Erosion                    | Dilation                      | Dilation & erosion |
| Second operation | Dilation                   | Erosion                       | Subtraction        |
| Effect           | Removes foreground details | Adds/fills foreground regions | Highlights edges   |
| Typical use      | Noise removal              | Hole filling                  | Edge extraction    |

## Summary

**Morphological transformations are shape-based image processing operations that use a structuring element to modify, analyze, enhance, or extract geometric structures from an image.**

The fundamental transformations are:

$$
\boxed{\text{Erosion}}
$$

$$
\boxed{\text{Dilation}}
$$

$$
\boxed{\text{Opening}}
$$

$$
\boxed{\text{Closing}}
$$

Important derived transformations include:

$$
\boxed{\text{Morphological Gradient}}
$$

$$
\boxed{\text{Top-Hat}}
$$

$$
\boxed{\text{Black-Hat}}
$$

$$
\boxed{\text{Hit-or-Miss}}
$$

### Quick Revision Table

| Operation       | Remember It As             |
| --- | --- |
| **Erosion**     | Shrink                     |
| **Dilation**    | Expand                     |
| **Opening**     | Remove                     |
| **Closing**     | Fill                       |
| **Gradient**    | Find boundaries            |
| **Top-Hat**     | Find small bright features |
| **Black-Hat**   | Find small dark features   |
| **Hit-or-Miss** | Find specific patterns     |

### Most Important Formulas

$$
\boxed{A\circ B=(A\ominus B)\oplus B}
$$

$$
\boxed{A\bullet B=(A\oplus B)\ominus B}
$$

$$
\boxed{G=(A\oplus B)-(A\ominus B)}
$$

$$
\boxed{T=A-(A\circ B)}
$$

$$
\boxed{BH=(A\bullet B)-A}
$$

> Morphological transformations use the **shape of a structuring element** to manipulate and analyze the **shape of objects in an image**.
