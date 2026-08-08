# Heuristic Functions

## Introduction

A **heuristic function** is a mathematical function that estimates the cost of reaching the goal state from a given node. It is one of the most important concepts in **informed search algorithms** because it helps the search process move toward the goal more efficiently.

In Artificial Intelligence, heuristics represent **domain-specific knowledge** that guides the search algorithm by estimating how close a state is to the goal.

## Definition

A heuristic function **h(n)** estimates the minimum cost from node **n** to the goal state.

The value of **h(n)** is an estimate, not necessarily the exact cost.

## Role of Heuristic Functions

Heuristic functions improve the efficiency of search algorithms by reducing the number of nodes that need to be explored.

Without heuristics, algorithms such as Breadth-First Search (BFS) and Uniform Cost Search (UCS) may explore a large number of unnecessary nodes.

With heuristics, the search algorithm can prioritize nodes that are more likely to lead to the goal.

General evaluation function:

```text
f(n) = g(n) + h(n)
```

Where:

- **g(n)** = Actual cost from the start node to node **n**
- **h(n)** = Estimated cost from node **n** to the goal
- **f(n)** = Estimated total cost of the solution path through **n**

## Example of a Heuristic Function

Consider the following map:

```text
      A
     / \
    B   C
     \ /
      D
      |
      G
```

Suppose the estimated distances to the goal are:

| Node | h(n) |
| --- | --- |
| A | 6 |
| B | 4 |
| C | 3 |
| D | 1 |
| G | 0 |

The heuristic suggests that **D** is closest to the goal and should receive higher priority during search.

## Properties of Heuristic Functions

A good heuristic function should provide estimates that help the search algorithm efficiently reach the goal.

### Admissible Heuristic

A heuristic is **admissible** if it never overestimates the true cost to reach the goal.

Mathematically,

```text
h(n) ≤ h*(n)
```

Where:

- **h(n)** = Estimated cost
- **h\*(n)** = Actual optimal cost

An admissible heuristic is called an **optimistic heuristic**.

Example:

Actual cost from A to G = 8

| Heuristic | Admissible? |
| --- | --- |
| h(A)=6 | Yes |
| h(A)=8 | Yes |
| h(A)=10 | No |

A* search guarantees optimal solutions when the heuristic is admissible.

### Consistent (Monotonic) Heuristic

A heuristic is **consistent** if the estimated cost satisfies the triangle inequality.

```text
h(n) ≤ c(n,n') + h(n')
```

Where:

- **c(n,n')** = Cost from node **n** to successor **n'**

Consistency ensures that the estimated cost never decreases by more than the step cost.

Example:

| Transition | Cost |
| --- | --- |
| A → B | 2 |

If

```text
h(A) = 5, h(B) = 4
```

Then

```text
5 ≤ 2 + 4
```

which is true.

Consistent heuristics are always admissible.

## Characteristics of a Good Heuristic

A useful heuristic should have the following properties:

- **Accurate** – Close to the true cost.
- **Computationally inexpensive** – Easy to calculate.
- **Informative** – Distinguishes promising nodes from poor ones.
- **Consistent** – Satisfies the monotonicity condition.
- **Admissible** – Does not overestimate.

A perfect heuristic equals the actual cost:

```text
h(n) = h*(n)
```

In this case, the search expands only nodes on the optimal path.

## Types of Heuristic Functions

### Exact Heuristic

Provides the true remaining cost.

```text
h(n) = h*(n)
```

Advantages:

- Expands minimum possible nodes.
- Finds optimal solution efficiently.

Disadvantage:

- Usually impossible or very expensive to compute.

### Approximate Heuristic

Provides an estimated remaining cost.

Most practical AI systems use approximate heuristics.

Advantages:

- Faster computation.
- Reduced search effort.

Disadvantages:

- May not be optimal.
- Performance depends on estimate quality.

## Heuristic Functions in Different Search Algorithms

### Greedy Best-First Search

Uses

```text
f(n)=h(n)
```

The algorithm selects the node with the smallest heuristic value.

Advantages:

- Fast search.

Disadvantages:

- May produce non-optimal solutions.

### A* Search

Uses

``text
f(n) = g(n) + h(n)
```

Advantages:

- Optimal with admissible heuristics.
- Complete under suitable conditions.

Disadvantages:

- Higher memory usage.

## Example of Heuristic Evaluation

Consider the graph:

```text
S ---- A ---- G
 \          /
  \        /
    B ----
```

Assume:

Actual costs:

| Edge | Cost |
|------|------|
| S–A | 2 |
| A–G | 5 |
| S–B | 3 |
| B–G | 2 |

Heuristic values:

| Node | h(n) |
|------|------|
| S | 4 |
| A | 5 |
| B | 2 |
| G | 0 |

For A*:

For node A:

```text
f(A) = 2 + 5 = 7
```

For node B:

```text
f(B) = 3 + 2 = 5
```

Since **f(B) < f(A)**, node **B** is expanded first.

## Common Heuristic Functions

### Straight-Line Distance (Euclidean Distance)

Used in map navigation.

```text
h(n) = √((x₂ - x₁)² + (y₂ - y₁)²)
```

Applications:

- GPS navigation
- Robot path planning

### Manhattan Distance

Used in grid-based pathfinding.

```text
h(n) = |x₂ - x₁| + |y₂ - y₁|
```

Applications:

- Sliding tile puzzles
- Grid navigation
- Warehouse robots

### Hamming Distance

Counts the number of misplaced components.

Applications:

- String comparison
- Error correction
- Puzzle solving

## Heuristic Dominance

Suppose two admissible heuristics:

```text
h₁(n), h₂(n)
```

If

```text
h₂(n) ≥ h₁(n)
```

for all nodes, and both are admissible, then **h₂ dominates h₁**.

A dominant heuristic is generally better because it provides more accurate estimates and expands fewer nodes.

Example:

| Node | h₁ | h₂ |
| --- | --- | --- |
| A | 2 | 3 |
| B | 4 | 5 |
| C | 1 | 2 |

Here **h₂** dominates **h₁**.

## Designing Heuristic Functions

Common methods include:

### Relaxed Problems

Remove some constraints from the original problem.

Example:

In the 8-puzzle, allow tiles to move freely.

### Problem Decomposition

Break a complex problem into simpler subproblems.

### Pattern Databases

Precompute exact costs for important subproblems and store them for future use.

Pattern databases provide very powerful heuristics for puzzles and planning problems.

## Advantages of Heuristic Functions

- Significantly reduce search time.
- Reduce the number of expanded nodes.
- Improve scalability.
- Make complex AI problems solvable.
- Enable efficient pathfinding and planning.

## Limitations of Heuristic Functions

- May require domain knowledge.
- Poor heuristics can mislead the search.
- Computing heuristics may be expensive.
- Inadmissible heuristics may produce non-optimal solutions.
- Performance varies across problem domains.

## Comparison of Heuristic Quality

| Heuristic Type | Accuracy | Computation Cost | Optimality |
| --- | --- | --- | --- |
| Zero heuristic | Very low | Very low | Yes |
| Weak heuristic | Low | Low | Usually |
| Good heuristic | High | Moderate | Yes |
| Perfect heuristic | Exact | Very high | Yes |

## Applications

Heuristic functions are used in:

- Route planning
- Robot navigation
- Game playing
- Puzzle solving
- Automated planning
- Machine learning optimization
- Network routing
- Scheduling problems

## Key Points

- A heuristic function estimates the cost from a node to the goal.
- It is represented as **h(n)**.
- **Admissible heuristics** never overestimate the true cost.
- **Consistent heuristics** satisfy the triangle inequality.
- A* uses **f(n)=g(n)+h(n)**.
- Better heuristics reduce the number of expanded nodes.
- Common heuristics include **Euclidean distance, Manhattan distance, and Hamming distance**.
- Heuristic quality directly affects the efficiency of informed search algorithms.
 