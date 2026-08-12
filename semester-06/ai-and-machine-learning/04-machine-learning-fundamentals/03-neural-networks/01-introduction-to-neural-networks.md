# Introduction to Neural Networks

## Introduction

A **Neural Network (NN)** or **Artificial Neural Network (ANN)** is a computational model inspired by the structure and functioning of the **human brain**. It consists of interconnected processing units called **neurons**, which work together to learn patterns from data and make predictions or decisions.

A neural network learns by adjusting the **weights** of the connections between neurons during the training process.

> **Definition:** An artificial neural network is a machine learning model composed of interconnected neurons arranged in layers that learn input-output relationships by modifying connection weights through training.

## Biological Inspiration

The concept of neural networks is inspired by the **biological nervous system**, particularly the human brain.

### Comparison of Biological and Artificial Neurons

| Biological Neuron | Artificial Neuron |
| --- | --- |
| Dendrites | Input features |
| Cell body | Processing unit |
| Synapses | Weights |
| Axon | Output |

Just as biological neurons receive signals, process them, and transmit outputs, artificial neurons receive numerical inputs, perform mathematical operations, and generate outputs.

## Basic Architecture of a Neural Network

A neural network is organized into **layers of neurons**.

```text
Input Layer  ->  Hidden Layer(s)  ->  Output Layer
```

### 1. Input Layer

- Receives the input data.
- Each neuron represents one feature of the dataset.
- Example: For house price prediction, inputs may include area, number of rooms, and location.

### 2. Hidden Layer

- Performs intermediate computations.
- Extracts patterns and relationships from the data.
- A network may contain **one or multiple hidden layers**.

### 3. Output Layer

- Produces the final prediction.
- Number of neurons depends on the problem:
  - One neuron for binary classification
  - Multiple neurons for multiclass classification
  - One neuron for regression

## Structure of an Artificial Neuron

A single artificial neuron receives multiple inputs and produces one output.

```text
x1 ----\
x2 -----\ 
x3 ------> [ Neuron ] ----> Output (y)
xn -----/
```

Each input is multiplied by a corresponding weight before processing.

## Mathematical Model of a Neuron

Suppose a neuron receives inputs:

$$
x_1, x_2, x_3, \ldots, x_n
$$

with corresponding weights:

$$
w_1, w_2, w_3, \ldots, w_n
$$

and bias **b**.

### Weighted Sum

$$
z = \sum_{i=1}^{n} w_i x_i + b
$$

### Output of the Neuron

$$
y = f(z)
$$

where:

- $z$ = weighted sum
- $f$ = activation function
- $y$ = output

## Working of a Neural Network

The operation of a neural network occurs in the following steps.

### Step 1: Input

Training examples are fed into the input layer.

### Step 2: Weighted Sum

Each neuron computes the weighted combination of its inputs.

### Step 3: Activation

The activation function transforms the weighted sum into an output.

### Step 4: Forward Propagation

Outputs from one layer become inputs to the next layer.

### Step 5: Prediction

The output layer generates the final prediction.

### Step 6: Learning

The network compares the prediction with the actual target and adjusts the weights to reduce the error.

## Activation Functions

Activation functions introduce **non-linearity** into the neural network.

Without activation functions, the network behaves like a simple linear model.

### Common Activation Functions

| Activation Function | Output Range |
| --- | --- |
| Step Function | 0 or 1 |
| Sigmoid | (0, 1) |
| Tanh | (-1, 1) |
| ReLU | 0 to ∞ |

### ReLU (Rectified Linear Unit)

$$
f(x)=\max(0,x)
$$

Advantages of ReLU:

- Computationally efficient
- Reduces the vanishing gradient problem
- Widely used in modern neural networks

## Characteristics of Neural Networks

### 1. Non-linear Modeling

Can learn complex non-linear relationships between inputs and outputs.

### 2. Learning from Examples

Automatically learns patterns from training data.

### 3. Generalization

Can make predictions on previously unseen data.

### 4. Parallel Processing

Multiple neurons operate simultaneously.

### 5. Adaptability

Performance improves with additional training data.

## Training a Neural Network

Training is the process of finding the **optimal weights**.

### Training Process

1. Initialize weights randomly.
2. Perform forward propagation.
3. Calculate prediction error.
4. Update weights.
5. Repeat until the error becomes sufficiently small.

The most common learning algorithm is **backpropagation with gradient descent**.

## Types of Neural Networks

| Neural Network Type | Primary Application |
| --- | --- |
| Perceptron | Simple linear classification |
| Multi-layer Feed Forward Network | Classification and regression |
| Convolutional Neural Network (CNN) | Image processing |
| Recurrent Neural Network (RNN) | Sequence and language data |

In this syllabus, the focus is on **Perceptron** and **Multi-layer Feed Forward Networks**.

## Advantages of Neural Networks

- Can model highly complex relationships.
- Excellent performance on image, speech, and text data.
- Automatically learns features from data.
- Robust to noisy inputs.
- Can handle large datasets efficiently.

## Limitations of Neural Networks

- Requires large amounts of training data.
- Computationally expensive.
- Often acts as a **black-box model**.
- Performance depends on architecture and hyperparameters.
- May suffer from **overfitting** if not properly regularized.

## Applications of Neural Networks

### Computer Vision

- Face recognition
- Object detection
- Medical image analysis

### Natural Language Processing

- Machine translation
- Chatbots
- Sentiment analysis

### Speech Processing

- Speech recognition
- Voice assistants

### Finance

- Credit scoring
- Fraud detection
- Stock market prediction

### Healthcare

- Disease diagnosis
- Medical decision support
- Drug discovery

### Autonomous Systems

- Self-driving cars
- Robotics
- Industrial automation

## Neural Networks vs Traditional Machine Learning

| Traditional Machine Learning | Neural Networks |
| --- | --- |
| Requires feature engineering | Learns features automatically |
| Works mainly with structured data | Works with structured and unstructured data |
| Simpler models | More complex models |
| Easier to interpret | Difficult to interpret |
| Lower computational cost | Higher computational cost |

## Advantages and Limitations

### Advantages

- Learns complex patterns
- High prediction accuracy
- Automatic feature extraction
- Suitable for unstructured data

### Limitations

- Large data requirement
- High computational cost
- Black-box behavior
- Overfitting risk

## Important Exam Questions

### 2 Marks

**Definition of Neural Network**

An artificial neural network is a layered network of interconnected artificial neurons that learns patterns from data by adjusting connection weights.

### 5 Marks

#### Architecture of Neural Network

Explain:

- Input layer
- Hidden layer(s)
- Output layer
- Weighted connections
- Activation function

#### Working of Neural Network

Explain:

1. Input
2. Weighted sum
3. Activation
4. Forward propagation
5. Output generation
6. Weight adjustment

#### Advantages and Limitations

Write at least **four advantages and four limitations** with suitable applications.

## Summary

- Neural networks are inspired by the **human brain**.
- They consist of **input, hidden, and output layers**.
- Each neuron computes a **weighted sum plus bias**.
- An **activation function** introduces non-linearity.
- Networks learn by **adjusting weights during training**.
- They are widely used in **classification, regression, computer vision, speech recognition, and natural language processing**.
- The next topics are **Perceptron** and **Multi-layer Feed Forward Networks**, which build directly on these concepts.
