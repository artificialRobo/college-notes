# Best-First Search

## Introduction

**Best-First Search (BeFS)** is an **informed search algorithm** that selects the most promising node for expansion based on an **evaluation function**. Unlike uninformed search strategies, Best-First Search uses **heuristic information** to guide the search toward the goal more efficiently.

The algorithm maintains a priority queue of frontier nodes and always expands the node that appears to be closest to the goal according to the evaluation function.

## Definition

Best-First Search is a search strategy that expands the node with the lowest evaluation value first, where the evaluation function estimates the desirability of a node.

## Basic Idea

At each step, the algorithm:

1. Generates successor nodes.
2. Evaluates each successor.
3. Inserts them into the frontier.
4. Selects the node with the **best (lowest) evaluation value** for the next expansion.

The evaluation function is generally written as:

```text
f(n)
```

where **f(n)** measures how promising node **n** is.

Different versions of Best-First Search use different evaluation functions.

| Search Strategy | Evaluation Function |
| --- | --- |
| Greedy Best-First Search | \(f(n) = h(n)\) |
| A* Search | \(f(n) = g(n) + h(n)\) |

Where:

- **g(n)** = Cost from the start node to node **n**
- **h(n)** = Estimated cost from node **n** to the goal

## Search Process

Consider the following search tree:

```text
        A
      / | \
     B  C  D
     |     |
     E     G
```

Suppose heuristic values are:

| Node | \(h(n)\) |
| --- | --- |
| A | 5 |
| B | 4 |
| C | 2 |
| D | 6 |
| E | 3 |
| G | 0 |

Expansion order:

1. Expand **A**
2. Choose **C** (lowest heuristic value)
3. Expand **C**
4. Generate **G**
5. Goal reached

Expansion sequence:

```text
A -> C -> G
```

## Algorithm

### Best-First Search Algorithm

**Input:** Initial state, goal test, evaluation function \(f(n)\)

**Output:** Path from start node to goal node

```text
BestFirstSearch(start, goal)

1. Create an empty priority queue OPEN
2. Insert start node into OPEN
3. Create an empty CLOSED list

4. while OPEN is not empty do
5.     Remove node n with the lowest f(n)
6.     if n is the goal node then
7.         return solution path
8.     Add n to CLOSED
9.     Generate successors of n
10.    for each successor s do
11.        Compute f(s)
12.        if s is not in OPEN or CLOSED then
13.            Insert s into OPEN
14. return Failure
```

## Priority Queue Implementation

The frontier is usually implemented using a **priority queue (min-heap)**.

Example:

| Node | \(f(n)\) |
|------|----------|
| B | 7 |
| C | 3 |
| D | 5 |

The next node selected is **C** because it has the smallest evaluation value.

## Evaluation Function

The efficiency of Best-First Search depends heavily on the evaluation function.

### Greedy Best-First Search

Uses only the heuristic estimate.

```text
f(n) = h(n)
```

The algorithm always chooses the node that appears closest to the goal.

### A* Search

Uses both the path cost and heuristic estimate.

```text
f(n) = g(n) + h(n)
```

A* is a special case of Best-First Search and generally provides optimal solutions under suitable heuristic conditions.

## Example

Consider the graph:

```text
        S
       / \
      A   B
      |   |
      C   G
```

Heuristic values:

| Node | \(h(n)\) |
| --- | --- |
| S | 5 |
| A | 4 |
| B | 1 |
| C | 3 |
| G | 0 |

Execution:

- OPEN = {S}
- Expand S
- OPEN = {A(4), B(1)}
- Select B
- Expand B
- Generate G
- Select G
- Goal reached

Solution path:

```text
S -> B -> G
```

## Characteristics of Best-First Search

### Completeness

- Depends on the implementation.
- Greedy Best-First Search is **not always complete** in infinite search spaces.
- It may get trapped in loops if repeated-state checking is not used.

### Optimality

- Greedy Best-First Search is **not optimal**.
- It may choose a path that appears promising but has a high actual cost.

### Time Complexity

In the worst case:

```text
O(b^m)
```

Where:

- **b** = Branching factor
- **m** = Maximum depth

Performance improves significantly when the heuristic function is informative.

### Space Complexity

Best-First Search stores all generated nodes in memory.

Worst-case space complexity:

```text
O(b^m)
```

Therefore, memory consumption can become very large.

## Advantages

- Uses domain knowledge through heuristics.
- Often finds solutions much faster than uninformed search.
- Can dramatically reduce the number of expanded nodes.
- Flexible framework that includes several search algorithms.

## Disadvantages

- Strongly dependent on heuristic quality.
- Poor heuristics may lead to inefficient search.
- High memory consumption.
- Greedy variants may produce non-optimal solutions.
- May become trapped in local minima or misleading paths.

## Comparison with Other Search Algorithms

| Algorithm | Uses Heuristic | Optimal | Complete |
|-----------|---------------|---------|----------|
| BFS | No | Yes | Yes |
| DFS | No | No | No |
| Uniform Cost Search | No | Yes | Yes |
| Greedy Best-First Search | Yes | No | Not always |
| A* Search | Yes | Yes* | Yes* |

\*When the heuristic is admissible and consistent.

## Applications

Best-First Search is widely used in AI and optimization problems.

Common applications include:

- Route planning
- Robot navigation
- Game playing
- Automated reasoning
- Pathfinding in maps
- Network routing
- Scheduling and planning problems

## Key Points

- Best-First Search is an **informed search algorithm**.
- It selects the node with the **lowest evaluation value**.
- The frontier is maintained as a **priority queue**.
- Greedy Best-First Search uses **\(h(n)\)** only.
- A* Search is a **Best-First Search algorithm** with **\(f(n) = g(n) + h(n)\)**.
- Greedy Best-First Search is generally **not optimal** and may not be complete.
- Memory usage is a major limitation because all frontier nodes are stored.
