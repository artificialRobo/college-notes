# Perceptron

## Introduction

A **Perceptron** is the **simplest type of artificial neural network**, introduced by **Frank Rosenblatt in 1958**. It is a **single-layer neural network** used primarily for **binary classification problems**.

The perceptron receives multiple input values, computes a weighted sum, applies a threshold activation function, and produces a binary output (0 or 1).

> **Definition:** A perceptron is a single-layer feed-forward neural network that performs binary classification by computing a weighted sum of inputs and applying a threshold activation function.

## Basic architecture of a perceptron

A perceptron consists of:

- Input neurons
- Weights
- Bias
- Summation unit
- Activation function
- Output neuron

```text
x1 ----\
        \
x2 -----\ 
         > ( Weighted Sum ) --> Activation Function --> Output (y)
x3 -----/
       /
xn ---/
```

Where:

- $x_1, x_2, \ldots, x_n$ are input features.
- $w_1, w_2, \ldots, w_n$ are weights.
- $b$ is the bias.
- $y$ is the output.

## Components of a perceptron

### 1. Input layer

Receives the input features from the dataset.

Examples:

- Height
- Weight
- Age

### 2. Weights

Each input is associated with a weight that indicates its importance.

A higher weight means greater influence on the output.

### 3. Bias

The bias shifts the decision boundary and improves learning flexibility.

### 4. Summation unit

Calculates the weighted sum of all inputs.

### 5. Activation function

Determines whether the neuron should produce output 0 or 1.

## Mathematical model of a perceptron

For inputs:

$$
x_1, x_2, \ldots, x_n
$$

and weights:

$$
w_1, w_2, \ldots, w_n
$$

the weighted sum is:

$$
z = \sum_{i=1}^{n} w_i x_i + b
$$

The output is:

$$
y = f(z)
$$

## Step activation function

The perceptron uses the **step (threshold) activation function**.

$$
f(z)=
\begin{cases}
1, & z \geq 0 \\
0, & z < 0
\end{cases}
$$

This function converts the weighted sum into a binary output.

## Working of a perceptron

The perceptron operates through the following steps.

### Step 1: Receive inputs

Input features are supplied to the perceptron.

### Step 2: Compute weighted sum

Each input is multiplied by its weight.

$$
z=w_1x_1+w_2x_2+\cdots+w_nx_n+b
$$

### Step 3: Apply activation function

The step function determines the output.

- $z \geq 0$ => output = 1
- $z < 0$ => output = 0

### Step 4: Produce output

The perceptron classifies the input into one of two classes.

## Example of perceptron computation

Suppose:

$$
x_1=2,\quad x_2=1
$$

Weights:

$$
w_1=1,\quad w_2=2
$$

Bias:

$$
b=-2
$$

### Step 1: Weighted sum

$$
z=(1\times2)+(2\times1)-2
$$

$$
z=2
$$

### Step 2: Activation

Since

$$
z=2 \geq 0
$$

Output:

$$
y=1
$$

Hence, the perceptron predicts **Class 1**.

## Perceptron learning algorithm

The perceptron learns by **adjusting its weights** whenever it makes an incorrect prediction.

### Algorithm steps

1. Initialize weights and bias.
2. Select a training example.
3. Compute the output.
4. Compare predicted output with actual output.
5. Update weights if the prediction is incorrect.
6. Repeat for all training examples.

## Weight update rule

The weight update equation is:

$$
w_i^{new}=w_i^{old}+\eta(t-y)x_i
$$

Where:

- $\eta$ = learning rate
- $t$ = target output
- $y$ = predicted output
- $x_i$ = input value

Bias update:

$$
b^{new}=b^{old}+\eta(t-y)
$$

## Perceptron learning example

Assume:

Inputs:

$$
x_1=1,\quad x_2=1
$$

Target:

$$
t=1
$$

Current weights:

$$
w_1=0,\quad w_2=0
$$

Bias:

$$
b=0
$$

Learning rate:

$$
\eta=1
$$

### Prediction

$$
z=0
$$

Output:

$$
y=1
$$

Since the prediction is correct:

$$
t-y=0
$$

Weights remain unchanged.

If the prediction were incorrect, the weights would be updated using the update rule.

## Decision boundary of a perceptron

The perceptron creates a **linear decision boundary**.

For two input features:

$$
w_1x_1+w_2x_2+b=0
$$

This equation represents a **straight line** that separates the two classes.

Example:

```text
Class A        |        Class B
      ●        |       ○
         ●     |    ○
---------------|--------------
            Decision Boundary
```

## Linearly separable data

A perceptron can successfully classify data only if the classes are **linearly separable**.

### Definition

Data is linearly separable if a single straight line (or hyperplane in higher dimensions) can separate all positive and negative examples.

#### Example: Linearly separable

```text
● ● ●

------------

○ ○ ○
```

#### Example: Not linearly separable (XOR)

```text
●      ○

○      ●
```

The XOR problem cannot be solved by a single perceptron.

## Limitations of the perceptron

### 1. Only binary classification

Produces only two output classes.

### 2. Linear decision boundary

Cannot model complex non-linear relationships.

### 3. Cannot solve XOR problem

Fails for non-linearly separable datasets.

### 4. Limited representation power

Cannot learn hierarchical features.

These limitations motivated the development of **multi-layer neural networks**.

## Advantages of the perceptron

- Simple and easy to implement.
- Fast training.
- Low computational cost.
- Effective for linearly separable problems.
- Forms the foundation of modern neural networks.

## Applications of perceptron

Perceptrons are used for simple classification tasks such as:

- Spam detection
- Document classification
- Pattern recognition
- Medical diagnosis (binary decision)
- Credit approval

Although modern applications usually employ multi-layer networks, the perceptron remains important as a fundamental learning model.

## Perceptron vs multi-layer neural network

| Perceptron | Multi-layer neural network |
| --- | --- |
| Single layer | Multiple layers |
| Linear classifier | Non-linear classifier |
| Binary classification | Binary and multiclass classification |
| Step activation | Various activation functions |
| Cannot solve XOR | Can solve XOR and complex problems |
| Simple architecture | Complex architecture |

## Perceptron learning algorithm (pseudocode)

```text
Initialize weights and bias

Repeat until convergence:

    For each training example (x, t):

        Compute:

            y = activation(wx + b)

        If y ≠ t:

            w = w + η(t - y)x

            b = b + η(t - y)
```

## Important examination questions

### 2 Marks

#### Definition

A perceptron is a single-layer neural network used for binary classification.

#### Activation function

The perceptron uses the **step activation function**.

### 5 Marks

#### Architecture of perceptron

Draw and explain:

- Input layer
- Weights
- Bias
- Summation unit
- Activation function
- Output

#### Perceptron learning algorithm

Explain:

- Weight initialization
- Prediction
- Error calculation
- Weight update rule
- Convergence

#### Advantages and limitations

Write at least **four advantages and four limitations**.

## Summary

- The **Perceptron** is the **first artificial neural network model**.
- It is a **single-layer feed-forward network**.
- It performs **binary classification**.
- Output is determined using the **step activation function**.
- Learning occurs through the **perceptron learning algorithm**.
- Weight update rule:

$$
w=w+\eta(t-y)x
$$

- It can classify **linearly separable data**.
- It **cannot solve non-linearly separable problems** such as XOR.
- The perceptron is the foundation for **multi-layer feed-forward neural networks**, which overcome its limitations.
