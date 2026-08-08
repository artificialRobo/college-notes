# Simplified Memory-Bounded A* (SMA*)

## Introduction

**Simplified Memory-Bounded A\* (SMA\*)** is an informed search algorithm designed to overcome the major limitation of **A\* search**, which is its high memory consumption. SMA\* is a **memory-bounded version of A\*** that uses a fixed amount of memory while still attempting to find an optimal solution.

Unlike A\*, which stores all generated nodes in memory, SMA\* removes less promising nodes when memory becomes full and retains only the most promising nodes.

## Definition

Simplified Memory-Bounded A\* (SMA\*) is a heuristic search algorithm that operates within a fixed memory limit by deleting the least promising nodes and storing their evaluation values for possible future regeneration.

SMA\* is particularly useful in large search spaces where A\* cannot operate efficiently due to memory limitations.

## Motivation for SMA*

A\* search has excellent search properties but requires large amounts of memory.

### Problem with A*

A\* stores:

- Every generated node.
- Every frontier node.
- Parent information for path reconstruction.

Memory complexity of A\*:

```text
O(b^d)
```

Where:

- **b** = Branching factor
- **d** = Depth of the optimal solution

For large search spaces, memory may become exhausted before the goal is reached.

SMA\* was developed to solve this problem.

## Basic Idea of SMA*

SMA\* behaves exactly like A\* until memory becomes full.

When the memory limit is reached:

1. Identify the **least promising node**.
2. Remove that node from memory.
3. Store its best evaluation value in its parent.
4. Continue the search.

If the forgotten node becomes promising later, it can be **regenerated**.

Thus, SMA\* trades **memory efficiency** for **additional computation time**.

## Evaluation Function

SMA\* uses the same evaluation function as A\*.

```text
f(n) = g(n) + h(n)
```

Where:

- **g(n)** = Actual path cost.
- **h(n)** = Estimated remaining cost.
- **f(n)** = Estimated total solution cost.

The algorithm always expands the node with the **smallest f-value**.

## Working Principle

SMA\* maintains a priority queue similar to A\*.

The main difference is memory management.

### When Memory Is Available

- Expand the best node.
- Generate successors.
- Insert successors into memory.

### When Memory Is Full

- Remove the node with the **highest f-value** (least promising).
- Save its best forgotten cost in the parent.
- Free memory for new nodes.

## Memory Management

Suppose memory can store only **5 nodes**.

Current memory:

| Node | f(n) |
| --- | --- |
| A | 5 |
| B | 7 |
| C | 9 |
| D | 12 |
| E | 15 |

Generate node **F** with

```text
f(F) = 6
```

Memory is full.

SMA\* deletes node **E** because it has the highest f-value.

The value **15** is stored in E&apos;s parent.

New memory:

| Node | f(n) |
| --- | --- |
| A | 5 |
| F | 6 |
| B | 7 |
| C | 9 |
| D | 12 |

## Algorithm of SMA*

**Input:** Start node, goal node, memory limit

**Output:** Best path found within memory constraints

```text
SMA*(start, goal, memory_limit)

1. Insert start node into memory.
2. while memory is not empty do
3.     Select node n with the smallest f-value.
4.     if n is the goal node then
5.         return solution path.
6.     Expand n.
7.     Generate successors.
8.     Compute f-values.
9.     Insert successors into memory.
10.    if memory exceeds memory_limit then
11.         Delete the node with the largest f-value.
12.         Store its forgotten value in its parent.
13. return Failure
```

## Example of SMA*

Consider the search tree:

```text
           S
         /   \
       A       B
      / \     / \
     C   D   E   G
```

Assume:

Edge costs:

| Edge | Cost |
| --- | --- |
| S–A | 2 |
| S–B | 3 |
| A–C | 4 |
| A–D | 5 |
| B–E | 6 |
| B–G | 2 |

Heuristic values:

| Node | h(n) |
| --- | --- |
| S | 5 |
| A | 4 |
| B | 2 |
| C | 3 |
| D | 2 |
| E | 1 |
| G | 0 |

Memory limit = **4 nodes**.

### Step 1

Memory:

| Node | f |
| --- | --- |
| S | 5 |

### Step 2

Expand S.

Generate A and B.

| Node | g | h | f |
| --- | --- | --- | --- |
| A | 2 | 4 | 6 |
| B | 3 | 2 | 5 |

Expand **B**.

### Step 3

Generate E and G.

Memory now contains:

| Node | f |
| --- | --- |
| A | 6 |
| E | 10 |
| G | 5 |

Expand **G**.

Goal reached.

## Forgotten Node Mechanism

The most important feature of SMA\* is **remembering forgotten costs**.

Suppose node D is deleted.

Before deletion:

```text
      A
     / \
    C   D
```

If

```text
f(D) = 12
```

then parent A stores

```text
Forgotten(A) = 12
```

If later all remaining children become worse than 12, SMA\* can regenerate D.

This mechanism prevents permanently losing potentially useful paths.

## Regeneration of Nodes

Deleted nodes are not completely forgotten.

When necessary:

- The parent recreates the deleted child.
- The stored f-value is restored.
- The search continues.

Regeneration allows SMA\* to recover from earlier memory-based decisions.

## Properties of SMA*

### Completeness

SMA\* is **complete** if enough memory exists to store the shallowest solution path.

If memory is too small, the algorithm may fail.

### Optimality

SMA\* is **optimal** if sufficient memory is available.

When memory is insufficient:

- It returns the best solution reachable within the memory limit.
- Optimality is not guaranteed.

## Time Complexity

Worst-case time complexity:

```text
O(b^d)
```

However, repeated regeneration may significantly increase computation time.

In some cases, SMA\* may regenerate the same nodes many times.

## Space Complexity

Space complexity is limited by available memory.

If memory capacity is **M**:

```text
O(M)
```

This is the major advantage of SMA\*.

## Comparison with A*

| Feature | A\* | SMA\* |
| --- | --- | --- |
| Evaluation function | g+h | g+h |
| Memory limit | No | Yes |
| Deletes nodes | No | Yes |
| Regenerates nodes | No | Yes |
| Complete | Yes | Yes* |
| Optimal | Yes | Yes* |
| Space complexity | O(bᵈ) | O(M) |

\*When sufficient memory is available.

## Comparison with RBFS

| Feature | RBFS | SMA\* |
| --- | --- | --- |
| Uses recursion | Yes | No |
| Fixed memory limit | No | Yes |
| Node deletion | Implicit | Explicit |
| Node regeneration | Yes | Yes |
| Practical memory control | Moderate | Excellent |

## Advantages of SMA*

- Uses limited memory.
- Suitable for large search spaces.
- Retains heuristic guidance.
- More practical than A\* in memory-constrained environments.
- Can recover deleted nodes.
- Produces high-quality solutions.

## Disadvantages of SMA*

- May repeatedly regenerate nodes.
- Increased computation time.
- More complex implementation.
- Optimality depends on available memory.
- Performance may degrade under very tight memory limits.

## Applications

SMA\* is used in:

- Robot navigation
- Autonomous systems
- Game AI
- Route planning
- Scheduling problems
- Embedded intelligent systems
- Mobile robotics
- Resource-constrained AI applications

## Practical Significance

Modern AI systems often operate with limited memory.

Examples:

- Mobile devices
- Embedded controllers
- Drones
- Autonomous robots

SMA\* allows heuristic search to remain effective even when memory resources are severely constrained.

## Key Points

- SMA\* is a **memory-bounded version of A\***.
- It uses **f(n)=g(n)+h(n)**.
- When memory becomes full, SMA\* deletes the **least promising node**.
- The deleted node&apos;s **f-value is stored in its parent**.
- Deleted nodes can be **regenerated later**.
- Space complexity is **O(M)**.
- Time complexity may increase due to regeneration.
- SMA\* is complete and optimal only when sufficient memory is available.
- The main objective of SMA\* is to **balance heuristic search efficiency with limited memory usage**.
