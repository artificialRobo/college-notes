# Learning Decision Trees

## Introduction

A **Decision Tree** is one of the most widely used supervised learning algorithms for both **classification** and **regression** tasks. It represents decisions and their possible consequences in the form of a **tree-like structure**, where each internal node represents a test on an attribute, each branch represents the outcome of the test, and each leaf node represents the final prediction.

Decision trees are popular because they are **simple to understand, easy to interpret, and require minimal data preprocessing**.

> **Definition**: A **Decision Tree** is a supervised learning model that recursively divides the dataset into smaller subsets based on feature values until a decision can be made. The objective is to create a tree that accurately predicts the target variable by learning decision rules from the training data.

## Basic Structure of a Decision Tree

A decision tree consists of three main components:

- **Root Node** – Represents the entire dataset and the first decision.
- **Internal (Decision) Nodes** – Represent tests on input features.
- **Leaf (Terminal) Nodes** – Represent the final predicted class or value.

Example:

```text
                 Outlook
               /    |     \
           Sunny Overcast Rain
            /           |      \
       Humidity        Yes     Wind
        /    \                 /   \
     High Normal           Strong Weak
      No     Yes             No     Yes
```

In this example:

- **Outlook** is the root node.
- **Humidity** and **Wind** are internal nodes.
- **Yes** and **No** are leaf nodes.

## Working Principle

Decision trees work by repeatedly selecting the **best feature** that divides the training data into the most homogeneous subsets.

The algorithm follows a **top-down recursive partitioning** approach.

### Step-by-Step Process

1. Start with the entire training dataset.
2. Select the best feature for splitting.
3. Divide the dataset based on the selected feature.
4. Repeat the process for each subset.
5. Stop when a stopping condition is satisfied.

## Decision Tree Learning Process

Suppose we want to predict whether a person will **buy a computer**.

| Age | Income | Student | Buy Computer |
| --- | --- | --- | --- |
| Young | High | No | No |
| Young | High | No | No |
| Middle | High | No | Yes |
| Senior | Medium | No | Yes |
| Senior | Low | Yes | Yes |

The algorithm evaluates all attributes and selects the one that provides the **best separation** of the target classes.

## Recursive Partitioning

The tree is built recursively.

At each node:

- Evaluate all possible splits.
- Choose the split with the highest information gain or lowest impurity.
- Create child nodes.
- Continue until termination.

## Attribute Selection

Selecting the appropriate attribute is the most important step in decision tree learning.

The quality of a split is measured using **attribute selection measures**.

Common measures:

- Entropy
- Information Gain
- Gini Index
- Gain Ratio

The attribute with the best score is chosen for splitting.

## Entropy

Entropy measures the **uncertainty or impurity** in a dataset.

For a binary classification problem:

$$
Entropy(S)= -p_1\log_2 p_1 - p_2\log_2 p_2
$$

Where:

- $p_1$ = probability of class 1
- $p_2$ = probability of class 2

### Interpretation

| Entropy | Meaning |
| --- | --- |
| 0 | Pure dataset |
| 1 | Maximum uncertainty |

### Example

If a node contains:

- 4 positive examples
- 4 negative examples

Then:

$$
Entropy = -0.5\log_2(0.5)-0.5\log_2(0.5)=1
$$

The node is highly impure.

## Information Gain

Information Gain measures the **reduction in entropy** after splitting the dataset.

$$
Gain(S,A)=Entropy(S)-\sum \frac{|S_v|}{|S|}Entropy(S_v)
$$

Where:

- $S$ = original dataset
- $A$ = attribute
- $S_v$ = subset created by the split

### Interpretation

- Higher information gain indicates a better split.
- The attribute with the maximum information gain is selected.

## Example of Information Gain

Suppose the dataset has entropy:

$$
Entropy(S)=0.94
$$

After splitting on **Student**:

| Student | Entropy |
| --- | --- |
| Yes | 0.2 |
| No | 0.8 |

Weighted entropy:

$$
0.5(0.2)+0.5(0.8)=0.5
$$

Information Gain:

$$
0.94-0.5=0.44
$$

Since the entropy is reduced significantly, **Student** is a good splitting attribute.

## Gini Index

The **Gini Index** is another impurity measure commonly used in the **CART (Classification and Regression Trees)** algorithm.

$$
Gini(S)=1-\sum p_i^2
$$

For binary classification:

$$
Gini=1-(p_1^2+p_2^2)
$$

### Example

If:

- Positive = 0.7
- Negative = 0.3

$$
Gini=1-(0.7^2+0.3^2)=0.42
$$

Lower Gini values indicate purer nodes.

## Entropy vs Gini Index

| Entropy | Gini Index |
| --- | --- |
| Based on information theory | Based on probability |
| Uses logarithms | No logarithms |
| Used in ID3 and C4.5 | Used in CART |
| Slightly computationally expensive | Computationally efficient |

## Decision Tree Algorithms

### ID3 (Iterative Dichotomiser 3)

- Uses **Information Gain**
- Handles categorical attributes
- Produces classification trees

### C4.5

- Extension of ID3
- Uses **Gain Ratio**
- Handles continuous attributes
- Supports pruning

### CART

- Uses **Gini Index**
- Produces binary trees
- Supports classification and regression

## Stopping Criteria

Tree construction stops when:

- All samples belong to the same class.
- No attributes remain for splitting.
- Maximum tree depth is reached.
- Minimum number of samples is reached.
- Information gain becomes insignificant.

## Pruning of Decision Trees

Decision trees may become overly complex.

**Pruning** removes unnecessary branches to improve generalization.

### Why Pruning?

- Reduces overfitting
- Simplifies the model
- Improves prediction accuracy
- Reduces tree size

## Types of Pruning

### Pre-pruning (Early Stopping)

Stop tree growth before it becomes too large.

Examples:

- Maximum depth
- Minimum samples per node
- Minimum information gain

### Post-pruning

Build the full tree first and then remove unnecessary branches.

More commonly used because it generally produces better trees.

## Advantages of Decision Trees

- Easy to understand and interpret
- Can handle both numerical and categorical data
- Requires little data preprocessing
- Handles non-linear relationships
- Useful for feature selection
- Fast prediction

## Limitations of Decision Trees

- Can overfit the training data
- Sensitive to small changes in data
- May produce biased trees for imbalanced datasets
- Greedy splitting may not find the globally optimal tree
- Large trees become difficult to manage

## Applications of Decision Trees

### Healthcare

- Disease diagnosis
- Treatment recommendation

### Banking and Finance

- Credit approval
- Loan risk assessment

### Marketing

- Customer segmentation
- Purchase prediction

### Education

- Student performance prediction

### Agriculture

- Crop disease identification

### Fraud Detection

- Transaction classification

## Decision Tree Learning Algorithm (Simplified)

```text
DecisionTree(Data)

1. If all examples belong to one class:
       Return Leaf Node

2. Select the best attribute

3. Create a decision node

4. Split the dataset

5. Recursively build subtrees

6. Return the tree
```

## Comparison with Other Supervised Learning Methods

| Decision Tree | SVM | Neural Network |
| --- | ---- | --- |
| Highly interpretable | Less interpretable | Low interpretability |
| Fast training | Moderate | Slow |
| Handles categorical data | Limited | Requires encoding |
| Can overfit easily | More robust | May overfit |
| Suitable for rule extraction | No | No |

## Short Note

A **Decision Tree** is a supervised learning algorithm used for classification and regression. It represents decisions in a tree structure consisting of a root node, internal nodes, and leaf nodes. The tree is built by recursively selecting the best attribute using measures such as **Information Gain**, **Entropy**, or **Gini Index**. Decision trees are easy to understand and interpret, require little preprocessing, and can handle both categorical and numerical data. However, they may suffer from **overfitting**, which can be reduced using **pruning techniques**.

## Key Points

- Decision trees are supervised learning models.
- Used for **classification and regression**.
- Built using **recursive partitioning**.
- Important terms: **Root node, Internal node, Leaf node**.
- Attribute selection measures: **Entropy, Information Gain, Gini Index**.
- Popular algorithms: **ID3, C4.5, CART**.
- **Pruning** helps reduce overfitting.
- Major advantage: **high interpretability**.
