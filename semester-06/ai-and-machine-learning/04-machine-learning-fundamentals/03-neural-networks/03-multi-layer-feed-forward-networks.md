# Multi-layer Feed Forward Networks

## Introduction

A **Multi-layer Feed Forward Network (MLFFN)** is an artificial neural network that contains **one or more hidden layers** between the input layer and the output layer. Information flows only in the **forward direction**, from the input layer to the output layer, without forming any cycles or feedback connections.

Multi-layer feed forward networks are capable of learning **complex non-linear relationships**, making them significantly more powerful than a single-layer perceptron.

> **Definition (Exam):** A multi-layer feed forward network is a neural network with one or more hidden layers in which data moves only from the input layer to the output layer, enabling the network to solve complex non-linear classification and regression problems.

## Need for multi-layer feed forward networks

A **single-layer perceptron** has several limitations:

- Can classify only **linearly separable data**.
- Cannot solve problems such as **XOR**.
- Has limited learning capability.

To overcome these limitations, additional **hidden layers** are introduced, allowing the network to learn **non-linear decision boundaries** and hierarchical feature representations.

## Architecture of a multi-layer feed forward network

A typical MLFFN consists of three types of layers:

1. Input layer
2. Hidden layer(s)
3. Output layer

```text
Input Layer        Hidden Layer(s)           Output Layer

x1  ----\
         \
x2  -----\        ● ----\
           \      |      \
x3  -------> ● ---●------- ● ----> y
           /      |      /
x4  -----/        ● ----/
```

Each neuron in one layer is connected to neurons in the next layer through **weighted connections**.

## Characteristics of MLFFN

- Information flows only in the **forward direction**.
- No loops or recurrent connections.
- Can contain **multiple hidden layers**.
- Uses **non-linear activation functions**.
- Learns through **backpropagation**.
- Can perform both **classification and regression** tasks.

## Layers in MLFFN

### 1. Input layer

- Receives the input features.
- Performs no computation.
- Simply passes data to the hidden layer.

Examples:

- Height
- Weight
- Age
- Income

### 2. Hidden layer

The hidden layer performs the actual learning.

Functions:

- Feature extraction
- Pattern recognition
- Non-linear transformation
- Representation learning

A network may contain:

- One hidden layer
- Two hidden layers
- Many hidden layers (deep neural networks)

### 3. Output layer

Produces the final prediction.

Examples:

- Binary classification -> one neuron
- Multiclass classification -> multiple neurons
- Regression -> one neuron

## Mathematical model

Consider a network with:

- $n$ input neurons
- $m$ hidden neurons
- one output neuron

### Hidden layer computation

For hidden neuron $j$:

$$
z_j=\sum_{i=1}^{n} w_{ij}x_i+b_j
$$

After applying the activation function:

$$
h_j=f(z_j)
$$

### Output layer computation

$$
z=\sum_{j=1}^{m} v_jh_j+c
$$

Final output:

$$
y=g(z)
$$

Where:

- $w_{ij}$ = input-to-hidden weights
- $v_j$ = hidden-to-output weights
- $b_j$ = hidden bias
- $c$ = output bias
- $f$ and $g$ = activation functions

## Forward propagation

Forward propagation is the process of computing the output of the network.

### Step 1: Input

Input features are supplied.

### Step 2: Hidden layer computation

Each hidden neuron computes:

$$
z_j=\sum w_{ij}x_i+b_j
$$

### Step 3: Activation

Apply activation function:

$$
h_j=f(z_j)
$$

### Step 4: Output layer computation

$$
z=\sum v_jh_j+c
$$

### Step 5: Final prediction

Apply output activation function:

$$
y=g(z)
$$

## Activation functions

Hidden layers generally use **non-linear activation functions**.

### Common activation functions

| Activation function | Formula | Output range |
| --- | --- | --- |
| Sigmoid | $1/(1+e^{-x})$ | (0,1) |
| Tanh | $(e^x-e^{-x})/(e^x+e^{-x})$ | (-1,1) |
| ReLU | $\max(0,x)$ | [0,∞) |
| Softmax | Probability distribution | (0,1) |

#### ReLU

Most commonly used in hidden layers because it:

- is computationally efficient,
- accelerates training,
- reduces the vanishing gradient problem.

#### Softmax

Commonly used in multiclass classification problems.

## Learning in MLFFN

Learning occurs by adjusting the network weights.

The most common learning algorithm is **Backpropagation**.

### Training process

1. Initialize weights randomly.
2. Perform forward propagation.
3. Compute prediction error.
4. Calculate gradients.
5. Update weights.
6. Repeat until convergence.

## Backpropagation algorithm

Backpropagation is a supervised learning algorithm used for training multi-layer networks.

### Main idea

The prediction error is propagated **backward** from the output layer to the hidden layers.

#### Training cycle

```text
Forward propagation
        |
        v
Compute error
        |
        v
Backward propagation
        |
        v
Update weights
        |
        v
Repeat
```

## Error function

For a single training example:

$$
E=\frac{1}{2}(t-y)^2
$$

Where:

- $t$ = target output
- $y$ = predicted output

The objective is to minimize the error by adjusting the weights.

## Gradient descent

Weights are updated using gradient descent.

$$
w^{new}=w^{old}-\eta\frac{\partial E}{\partial w}
$$

Where:

- $\eta$ = learning rate
- $\frac{\partial E}{\partial w}$ = gradient of the error

Gradient descent moves the weights in the direction that **reduces the error**.

## Solving the XOR problem

The XOR function is not linearly separable.

### XOR truth table

| x1 | x2 | Output |
| --- | --- | --- |
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

A single perceptron cannot solve XOR.

A **multi-layer feed forward network with at least one hidden layer** can solve XOR by creating a **non-linear decision boundary**.

This is one of the most important advantages of MLFFN.

## Advantages of MLFFN

### 1. Solves non-linear problems

Can model highly complex relationships.

### 2. Universal approximation capability

Can approximate almost any continuous function.

### 3. Automatic feature learning

Hidden layers automatically learn useful features.

### 4. High prediction accuracy

Suitable for complex real-world datasets.

### 5. Flexible architecture

Can be designed with different numbers of layers and neurons.

## Limitations of MLFFN

### 1. Computationally expensive

Training requires significant computation.

### 2. Large data requirement

Needs substantial training data.

### 3. Risk of overfitting

May memorize training data if the network is too large.

### 4. Difficult to interpret

Acts as a **black-box model**.

### 5. Hyperparameter tuning

Performance depends on:

- learning rate,
- number of hidden layers,
- number of neurons,
- activation functions,
- batch size.

## Applications of MLFFN

### Image classification

- Handwritten digit recognition
- Object recognition
- Medical imaging

### Speech recognition

- Voice assistants
- Speech-to-text systems

### Natural language processing

- Machine translation
- Text classification
- Sentiment analysis

### Finance

- Fraud detection
- Credit scoring
- Stock prediction

### Healthcare

- Disease diagnosis
- Medical decision support

### Industrial automation

- Quality inspection
- Predictive maintenance
- Process optimization

## Perceptron vs multi-layer feed forward network

| Perceptron | MLFFN |
| --- | --- |
| Single layer | Multiple layers |
| No hidden layer | One or more hidden layers |
| Linear classifier | Non-linear classifier |
| Binary classification | Binary, multiclass, and regression |
| Step activation | Various activation functions |
| Cannot solve XOR | Can solve XOR |
| Limited learning capacity | High learning capacity |

## Important examination points

### 2 Marks

#### Definition

A multi-layer feed forward network is a neural network containing one or more hidden layers with forward-only information flow.

#### Feed forward property

Data moves only from input to output; there are no feedback connections.

### 5 Marks

#### Architecture of MLFFN

Draw and explain:

- Input layer
- Hidden layer(s)
- Output layer
- Weighted connections
- Activation functions

#### Working of MLFFN

Explain:

1. Forward propagation
2. Hidden layer computation
3. Activation
4. Output generation
5. Error computation
6. Weight update

#### Advantages and limitations

Write at least four advantages and four limitations.

## Summary

- MLFFN contains **input, hidden, and output layers**.
- Information flows only in the **forward direction**.
- Hidden layers enable learning of **complex non-linear relationships**.
- The network is trained using **backpropagation**.
- Weights are updated through **gradient descent**.
- MLFFN can solve **XOR and other non-linearly separable problems**.
- It is widely used in **image recognition, speech processing, natural language processing, healthcare, finance, and industrial automation**.
- Multi-layer feed forward networks form the foundation of **modern deep learning systems**.
