# Support Vector Machines (SVM)

## Introduction

**Support Vector Machine (SVM)** is a powerful **supervised machine learning algorithm** primarily used for **classification** and **regression** tasks. It is widely used for classification problems because of its ability to create an **optimal decision boundary** that separates different classes with the **maximum possible margin**.

SVM is particularly effective for **high-dimensional datasets**, **text classification**, **image recognition**, and **bioinformatics applications**.

> **Definition**: A **Support Vector Machine (SVM)** is a supervised learning algorithm that finds the **best hyperplane** that separates data points of different classes while maximizing the distance (margin) between the nearest data points and the decision boundary.

The main objective of SVM is to achieve **maximum margin classification**, which improves the model's ability to generalize to unseen data.

## Basic Concept of SVM

Consider a binary classification problem with two classes:

- **Class A (●)**
- **Class B (▲)**

A decision boundary separates these two classes.

```text
Class A (●)         Class B (▲)

●    ●    ●

----------------------  Decision Boundary

        ▲    ▲    ▲
```

Among all possible boundaries, SVM selects the one with the **largest margin**.

## Hyperplane

A **hyperplane** is the decision boundary that separates classes.

In different dimensions:

- **2D:** A line
- **3D:** A plane
- **n-dimensional:** A hyperplane

The equation of a hyperplane is:

$$
\mathbf{w}\cdot\mathbf{x} + b = 0
$$

Where:

- **w** = weight vector
- **x** = feature vector
- **b** = bias term

The hyperplane divides the feature space into two regions corresponding to different classes.

## Margin

The **margin** is the distance between the hyperplane and the nearest data points from each class.

```text
Class A              Class B

●   ●   ●

----------------------  Margin

======================  Hyperplane

----------------------  Margin

        ▲   ▲   ▲
```

A **larger margin** generally results in better classification performance and improved generalization.

## Support Vectors

The data points that lie closest to the hyperplane are called **support vectors**.

These points determine the position and orientation of the hyperplane.

```text
●       ●

●   ●   ●

=========== Hyperplane ===========

▲   ▲   ▲

        ▲       ▲
```

The support vectors are the most critical training samples.

Removing non-support-vector points usually does not change the hyperplane significantly.

## Objective of SVM

The objective is to maximize the margin between the two classes.

Mathematically,

$$
\text{Margin} = \frac{2}{\|\mathbf{w}\|}
$$

Maximizing the margin is equivalent to minimizing:

$$
\frac{1}{2}\|\mathbf{w}\|^2
$$

subject to correct classification constraints.

## Mathematical Formulation

For a training dataset:

$$
(\mathbf{x}_1,y_1),(\mathbf{x}_2,y_2),\ldots,(\mathbf{x}_n,y_n)
$$

where:

- $\mathbf{x}_i$ = feature vector
- $y_i$ = class label (+1 or -1)

The constraints are:

$$
y_i(\mathbf{w}\cdot\mathbf{x}_i+b)\ge 1
$$

The optimization problem becomes:

Minimize

$$
\frac{1}{2}\|\mathbf{w}\|^2
$$

Subject to

$$
y_i(\mathbf{w}\cdot\mathbf{x}_i+b)\ge 1
$$

This is a **convex optimization problem**, ensuring a unique global optimum.

---

## Linear SVM

A **Linear SVM** is used when the data is **linearly separable**.

Example:

```text
● ● ●

------------------

▲ ▲ ▲
```

A straight line can perfectly separate the two classes.

### Characteristics

- Simple
- Fast
- Effective for linearly separable data

## Maximum Margin Classifier

Among all separating hyperplanes, SVM chooses the one with the **maximum margin**.

Example:

```text
Hyperplane 1

● ● ●
-------------
▲ ▲ ▲

Hyperplane 2 (Maximum Margin)

● ● ●

-------------

=============

-------------

▲ ▲ ▲
```

Hyperplane 2 is preferred because it maximizes the distance from both classes.

## Non-Linearly Separable Data

Real-world data is often **not linearly separable**.

Example:

```text
      ●

   ●     ●

      ▲

   ▲     ▲
```

A straight line cannot separate the classes.

SVM solves this problem using:

- **Soft Margin SVM**
- **Kernel Trick**

## Soft Margin SVM

Soft Margin SVM allows **some classification errors** to achieve better generalization.

Instead of perfectly separating all points, it balances:

- Margin maximization
- Classification accuracy

A penalty parameter **C** controls this trade-off.

## Regularization Parameter (C)

The parameter **C** determines how much the model penalizes misclassification.

### Large C

- Fewer classification errors
- Smaller margin
- Higher risk of overfitting

### Small C

- Larger margin
- More classification errors
- Better generalization

| Large C | Small C |
| --- | --- |
| Less tolerant to errors | More tolerant |
| Smaller margin | Larger margin |
| May overfit | May underfit |

## Kernel Trick

The **Kernel Trick** is the most important concept in SVM.

It transforms data from a lower-dimensional space into a higher-dimensional space where linear separation becomes possible.

Instead of explicitly performing the transformation, the kernel computes inner products directly.

Original Space:

```text
○ ○

  ▲

○ ○
```

Transformed Space:

```text
○ ○ ○

--------------

▲ ▲ ▲
```

The classes become linearly separable.

## Kernel Functions

A kernel function measures similarity between two data points.

### Linear Kernel

$$
K(\mathbf{x},\mathbf{z})=\mathbf{x}\cdot\mathbf{z}
$$

Used when data is approximately linearly separable.

#### Advantages

- Fast
- Suitable for high-dimensional sparse data

#### Applications

- Text classification
- Spam detection

### Polynomial Kernel

$$
K(\mathbf{x},\mathbf{z})=(\mathbf{x}\cdot\mathbf{z}+c)^d
$$

Where:

- **d** = polynomial degree
- **c** = constant

Captures polynomial relationships between features.

#### Applications

- Image classification
- Pattern recognition

### Radial Basis Function (RBF) Kernel

$$
K(\mathbf{x},\mathbf{z})=\exp(-\gamma\|\mathbf{x}-\mathbf{z}\|^2)
$$

Where **γ (gamma)** controls the influence of individual training samples.

#### Characteristics

- Most widely used kernel
- Handles complex non-linear boundaries
- Works well in many practical problems

### Sigmoid Kernel

$$
K(\mathbf{x},\mathbf{z})=\tanh(\alpha\,\mathbf{x}\cdot\mathbf{z}+c)
$$

Similar to neural network activation functions.

Less commonly used in practice.

## Comparison of Kernel Functions

| Kernel | Best For |
| --- | --- |
| Linear | Linearly separable data |
| Polynomial | Polynomial relationships |
| RBF | Complex non-linear data |
| Sigmoid | Neural-network-like boundaries |

## Choosing the Kernel

General guideline:

- **Linear kernel:** Large datasets, text data
- **RBF kernel:** Most non-linear problems
- **Polynomial kernel:** Moderate non-linearity
- **Sigmoid kernel:** Rarely used

The RBF kernel is often the default choice.

## SVM Classification Process

### Step 1

Collect labeled training data.

### Step 2

Select an appropriate kernel.

### Step 3

Train the SVM model.

### Step 4

Identify support vectors.

### Step 5

Construct the optimal hyperplane.

### Step 6

Classify new data points.

## Advantages of SVM

- Effective in high-dimensional spaces
- Works well with small and medium-sized datasets
- Maximizes margin for better generalization
- Robust to overfitting
- Memory efficient (uses support vectors)
- Can model complex non-linear decision boundaries

## Limitations of SVM

- Computationally expensive for very large datasets
- Training can be slow
- Choosing the correct kernel is challenging
- Performance depends on parameter tuning
- Less interpretable than decision trees
- Multi-class classification requires additional strategies

## SVM vs Decision Tree

| Support Vector Machine | Decision Tree |
| --- | --- |
| Margin-based classifier | Rule-based classifier |
| Less interpretable | Highly interpretable |
| Handles high-dimensional data well | May overfit |
| Kernel functions available | No kernel concept |
| Strong theoretical foundation | Simple and intuitive |

## Applications of SVM

### Text Classification

- Spam detection
- Sentiment analysis
- Document categorization

### Image Recognition

- Face detection
- Object recognition
- Handwriting recognition

### Bioinformatics

- Gene classification
- Protein classification
- Disease prediction

### Medical Diagnosis

- Cancer detection
- Tumor classification
- ECG analysis

### Finance

- Credit risk assessment
- Fraud detection
- Stock trend classification

## Multi-Class SVM

SVM is fundamentally a **binary classifier**.

For multiple classes, common approaches are:

### One-vs-Rest (OvR)

For **k classes**, train **k classifiers**.

### One-vs-One (OvO)

Train a classifier for every pair of classes.

For **k classes**:

$$
\frac{k(k-1)}{2}
$$

classifiers.

## Short Note

A **Support Vector Machine (SVM)** is a supervised learning algorithm used mainly for **classification**. It finds the **optimal hyperplane** that separates different classes with the **maximum margin**. The nearest data points, called **support vectors**, determine the position of the hyperplane. SVM can handle both **linear and non-linear classification** problems using **kernel functions** such as Linear, Polynomial, and RBF kernels. It provides good generalization and high accuracy, especially in high-dimensional spaces, but requires careful parameter and kernel selection.

## Key Points

- SVM is a **supervised classification algorithm**.
- Objective: **maximum margin classification**.
- Important terms: **Hyperplane, Margin, Support Vectors**.
- Linear SVM works for **linearly separable data**.
- Non-linear problems are solved using the **Kernel Trick**.
- Common kernels: **Linear, Polynomial, RBF, Sigmoid**.
- Parameter **C** controls margin and misclassification.
- Major advantages: **high accuracy and good generalization**.
- Major limitation: **computational cost for large datasets**.
- SVM is widely used in **text classification, image recognition, and medical diagnosis**.
