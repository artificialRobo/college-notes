# 4.2.2 Closing Operation

## 1. Definition

**Closing** is a fundamental morphological operation used in image processing to **fill small holes, gaps, and narrow breaks in objects while preserving the overall shape of larger objects**.

It is performed by applying **dilation followed by erosion** using the same structuring element.

$$
\boxed{A \bullet B = (A \oplus B) \ominus B}
$$

Where:

* $A$ = input image
* $B$ = structuring element
* $\oplus$ = dilation
* $\ominus$ = erosion
* $A \bullet B$ = closing of image $A$ by structuring element $B$

> **Key Point:** Closing = **Dilation -> Erosion**

## 2. Purpose of Closing

The main purposes of the closing operation are to:

* Fill **small holes** inside objects.
* Fill **small gaps and cracks**.
* Connect objects separated by **narrow gaps**.
* Remove small indentations from object boundaries.
* Smooth object contours.
* Join nearby portions of an object.
* Preserve the general shape of larger objects.

## 3. How Closing Works

Closing consists of two morphological operations.

### Step 1: Dilation

The image is first **dilated** using the structuring element.

Dilation:

* Expands foreground objects.
* Fills small gaps.
* Connects nearby objects.
* Reduces small breaks and discontinuities.

$$
A \oplus B
$$

### Step 2: Erosion

The dilated image is then **eroded** using the **same structuring element**.

Erosion:

* Shrinks the expanded objects.
* Removes some of the excess expansion produced by dilation.
* Restores the object's boundary toward its original size.

$$
(A \oplus B) \ominus B
$$

Therefore,

$$
\boxed{\text{Closing} = \text{Dilation followed by Erosion}}
$$

## 4. Intuitive Understanding

Consider a binary image containing a large object with a few small holes or gaps.

During **dilation**, the foreground region expands and may cover these small holes and gaps.

The subsequent **erosion** shrinks the expanded region back toward its original boundary.

The small holes or gaps that were filled during dilation generally remain filled.

Conceptually:

```text
Original Image
      ↓
   Dilation
      ↓
Gaps/Holes filled
      ↓
    Erosion
      ↓
Cleaned Image
```

Thus, closing is particularly useful when the objective is to **connect and fill** structures.

## 5. Mathematical Definition

For a binary set $A$ and structuring element $B$, the closing operation is defined as:

$$
\boxed{A \bullet B = (A \oplus B) \ominus B}
$$

The dilation is performed first, followed by erosion.

> **Important:** The **same structuring element** is normally used for both operations.

## 6. Example

Suppose a binary object contains a small gap in its boundary:

### Original

```text
0 0 0 0 0 0 0
0 1 1 1 1 1 0
0 1 1 0 1 1 0
0 1 1 1 1 1 0
0 0 0 0 0 0 0
```

The `0` inside the foreground region represents a **small hole**.

After applying dilation, the foreground expands and may cover the small hole.

After erosion, the object's outer boundary is reduced while the small hole remains filled.

### After Closing

```text
0 0 0 0 0 0 0
0 1 1 1 1 1 0
0 1 1 1 1 1 0
0 1 1 1 1 1 0
0 0 0 0 0 0 0
```

Thus, the closing operation has **filled the small hole**.

## 7. Closing of Gaps Between Objects

Closing can also be used to connect objects that are separated by a small gap.

For example:

```text
Before:

1111  1111
```

If the gap is sufficiently small relative to the structuring element, dilation can bridge the gap:

```text
1111111111
```

The subsequent erosion reduces the excessive expansion while maintaining the connection.

Result:

```text
1111111111
```

Therefore, closing is useful for **joining nearby components**.

## 8. Effect of the Structuring Element

The structuring element determines which gaps and holes can be closed.

### Small Structuring Element

* Fills very small holes.
* Closes very narrow gaps.
* Causes relatively little modification to the image.

### Large Structuring Element

* Can fill larger holes.
* Can bridge wider gaps.
* May unintentionally merge separate objects.
* Can significantly alter object boundaries.

Therefore, the **size and shape of the structuring element must be selected carefully**.

## 9. Geometric Interpretation

Closing can be understood as allowing the structuring element to **expand the foreground region** and then reducing the expansion.

During dilation, the structuring element grows the object into nearby empty regions.

During erosion, the object is reduced again.

Small cavities and narrow gaps that were covered during dilation may remain filled after erosion.

Thus, closing tends to:

* Smooth boundaries.
* Fill small cavities.
* Remove small indentations.
* Connect nearby components.

## 10. Important Properties of Closing

### 10.1 Extensive Property

The original image is contained within its closing:

$$
\boxed{A \subseteq A\bullet B}
$$

This means closing does not remove foreground pixels from the original set.

Instead, it can add foreground pixels.

### 10.2 Increasing Property

If:

$$
A\subseteq C
$$

then:

$$
\boxed{A\bullet B\subseteq C\bullet B}
$$

Therefore, the ordering of images is preserved after closing.

### 10.3 Idempotent Property

Applying closing repeatedly with the same structuring element does not change the result after the first closing:

$$
\boxed{(A\bullet B)\bullet B=A\bullet B}
$$

Thus, once the image has been closed, applying the same closing operation again produces the same result.

## 11. Applications of Closing

### 11.1 Filling Small Holes

Closing is commonly used to fill small holes within foreground objects.

### 11.2 Removing Small Gaps

It can remove small discontinuities and gaps in object boundaries.

### 11.3 Connecting Broken Objects

Closing can connect nearby regions separated by small gaps.

### 11.4 Document Image Processing

It can be used to:

* Connect broken characters.
* Fill small gaps in printed text.
* Improve the continuity of text strokes.

### 11.5 Medical Image Processing

Closing can help fill small gaps or cavities in segmented anatomical structures.

### 11.6 Object Detection

It can improve the continuity of objects before object analysis or feature extraction.

### 11.7 Boundary Smoothing

Closing removes small indentations and irregularities from object boundaries.

## 12. Closing vs. Dilation

| Feature            | Dilation         | Closing                                    |
| --- | --- | --- |
| Operations         | Single operation | Dilation + Erosion                         |
| Main effect        | Expands objects  | Fills gaps and holes                       |
| Boundary           | Expands          | Smooths                                    |
| Small gaps         | May fill them    | Specifically useful for closing them       |
| Object restoration | No               | Reduces excessive expansion after dilation |
| Formula            | $A\oplus B$      | $(A\oplus B)\ominus B$                     |

## 13. Opening vs. Closing

This is an **important examination comparison**.

| Feature              | Opening                     | Closing                     |
| --- | --- | --- |
| Operation sequence   | Erosion -> Dilation         | Dilation -> Erosion         |
| Formula              | $(A\ominus B)\oplus B$      | $(A\oplus B)\ominus B$      |
| Main purpose         | Removes small objects/noise | Fills small holes/gaps      |
| Effect on foreground | Generally removes pixels    | Generally adds pixels       |
| Small protrusions    | Removes them                | Preserves/fills around them |
| Small holes          | Generally preserved         | Filled                      |
| Narrow gaps          | Can remove thin connections | Can bridge narrow gaps      |
| Property             | Anti-extensive              | Extensive                   |

### Easy Memory Trick

> **Opening = Removes**
> **Closing = Fills**

Or:

> **Opening starts with Erosion.**
> **Closing starts with Dilation.**

## 14. Advantages of Closing

* Effective for filling small holes.
* Removes small gaps and cracks.
* Connects nearby components.
* Smooths object boundaries.
* Preserves the general structure of large objects.
* Useful as a preprocessing operation.
* Simple to implement.

## 15. Limitations of Closing

* The result depends on the size and shape of the structuring element.
* A very large structuring element may merge objects that should remain separate.
* Important narrow gaps may be unintentionally removed.
* Excessive closing can distort object boundaries.
* It may not be suitable when small gaps themselves contain important information.

## 16. Opening and Closing in Practical Image Processing

Opening and closing are often used together.

For example, a binary image may contain:

* Small unwanted foreground noise.
* Small holes inside objects.
* Broken boundaries.
* Irregular contours.

A possible processing sequence is:

```text
Input Image
     ↓
Opening
     ↓
Remove Small Noise
     ↓
Closing
     ↓
Fill Small Holes and Gaps
     ↓
Improved Image
```

The exact order depends on the application and the type of defects present in the image.

## Summary

**Closing is a morphological operation that performs dilation followed by erosion using the same structuring element.**

$$
\boxed{A\bullet B=(A\oplus B)\ominus B}
$$

Its major functions are:

1. Filling small holes.
2. Closing small gaps.
3. Connecting nearby components.
4. Removing small indentations.
5. Smoothing object boundaries.
6. Improving object continuity.

### One-Line Definition

> **Closing is the morphological operation obtained by dilating an image with a structuring element and then eroding the result with the same structuring element.**

### Most Important Formula

$$
\boxed{\text{Closing}=\text{Dilation}\rightarrow\text{Erosion}}
$$

### Key Properties

$$
\boxed{A\subseteq A\bullet B}
$$

$$
\boxed{A\subseteq C\Rightarrow A\bullet B\subseteq C\bullet B}
$$

$$
\boxed{(A\bullet B)\bullet B=A\bullet B}
$$

### Final Memory Rule

$$
\boxed{\text{Opening = Remove small objects}}
$$

$$
\boxed{\text{Closing = Fill small holes}}
$$
