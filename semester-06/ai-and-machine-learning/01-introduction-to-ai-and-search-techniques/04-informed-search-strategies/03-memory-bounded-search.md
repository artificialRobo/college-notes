# Memory-Bounded Search

## Introduction

**Memory-bounded search** refers to a class of informed search algorithms designed to operate effectively when the available memory is limited. Traditional heuristic search algorithms, particularly **A\* search**, store all generated nodes in memory, which can become impractical for large search spaces.

Memory-bounded search algorithms reduce memory consumption while attempting to preserve the advantages of heuristic search, such as goal-directed exploration and solution quality.

## Definition

Memory-bounded search is an informed search strategy that uses a limited amount of memory and discards less promising nodes when memory becomes full.

These algorithms are especially important in real-world AI applications where memory is a major computational constraint.

## Need for Memory-Bounded Search

A\* search is optimal and complete under suitable heuristic conditions, but it has a significant limitation.

### Problem with A\*

A\* stores:

- All expanded nodes.
- All generated frontier nodes.
- Parent information for path reconstruction.

As the search space grows, memory usage increases rapidly.

Worst-case memory complexity:

```text
O(b^d)
```

Where:

- **b** = Branching factor
- **d** = Depth of the optimal solution

For large values of **b** and **d**, A\* may exhaust available memory before finding a solution.

Memory-bounded search algorithms overcome this limitation.

## Basic Idea

The algorithm maintains only a limited number of nodes in memory.

When memory becomes full:

1. Identify the least promising node.
2. Remove that node from memory.
3. Preserve enough information so the node can be regenerated later if necessary.

This process allows the search to continue within a fixed memory limit.

## General Working Principle

Memory-bounded search follows these steps:

1. Start from the initial node.
2. Generate successor nodes.
3. Evaluate nodes using a heuristic function.
4. Store nodes in memory.
5. If memory is full:
   - Delete the least promising node.
   - Update the parent with the best forgotten cost.
6. Continue searching until the goal is found.

## Characteristics of Memory-Bounded Search

A memory-bounded search algorithm:

- Uses heuristic information.
- Limits memory usage.
- May regenerate previously deleted nodes.
- Trades memory efficiency for additional computation time.

## Types of Memory-Bounded Search Algorithms

The most important memory-bounded search algorithms are:

- Recursive Best-First Search (RBFS)
- Simplified Memory-Bounded A\* (SMA\*)
- Iterative Deepening A\* (IDA\*)

In most university syllabi, **SMA\*** is the primary memory-bounded algorithm.

## Recursive Best-First Search (RBFS)

### Concept

RBFS performs a best-first search using recursion.

Instead of storing the entire search tree, it stores only the current path and the best alternative paths.

### Working

- Expand the best node.
- Recursively explore it.
- If the path becomes worse than an alternative path, backtrack.
- Continue with the next best alternative.

### Memory Complexity

```text
O(bd)
```

RBFS uses much less memory than A\*.

### Advantages

- Low memory usage.
- Complete under suitable conditions.
- Often finds good solutions.

### Disadvantages

- May repeatedly regenerate nodes.
- Can perform redundant computations.

## Simplified Memory-Bounded A\* (SMA\*)

### Concept

SMA\* is a modified version of A\* that uses a fixed amount of memory.

It behaves like A\* until memory becomes full.

When memory is exhausted, SMA\* deletes the **least promising node** and stores its evaluation value in its parent.

This allows the algorithm to regenerate the deleted node later if it becomes promising.

### Main Idea

- Use A\*-like evaluation.
- Keep memory usage within a predefined limit.
- Forget poor nodes.
- Remember their best cost estimate.

## Working of SMA\*

Suppose memory can store only **4 nodes**.

Current frontier:

| Node | f(n) |
| --- | --- |
| A | 5 |
| B | 8 |
| C | 12 |
| D | 15 |

Generate node **E** with

```text
f(E) = 6
```

Memory is full.

SMA\* deletes the node with the largest evaluation value:

Node **D**.

The value **15** is stored in D&apos;s parent.

New frontier:

| Node | f(n) |
| --- | --- |
| A | 5 |
| E | 6 |
| B | 8 |
| C | 12 |

The search continues with the best available node.

## Algorithm of SMA\*

```text
SMA*(start)

1. Insert start node into memory.
2. while memory is not empty do
3.     Select the node with the smallest f-value.
4.     if goal reached then
5.         return solution.
6.     Expand the selected node.
7.     if memory is full then
8.         Remove the node with the largest f-value.
9.         Store its best forgotten value in its parent.
10. return Failure
```

## Example

Consider the search tree:

```text
        S
       / \
      A   B
     / \   \
    C   D   G
```

Assume:

| Node | f(n) |
| --- | --- |
| A | 4 |
| B | 6 |
| C | 5 |
| D | 8 |
| G | 7 |

Memory limit = 3 nodes.

Process:

- Store A, B, C.
- Generate D.
- Memory full.
- Delete D (largest f-value).
- Continue search.
- Later regenerate D if needed.

## Evaluation Function

SMA\* uses the same evaluation function as A\*:

```text
f(n) = g(n) + h(n)
```

However, the **stored value of forgotten nodes** may be propagated upward.

Parent value becomes:

```text
f(parent) = max(f(parent), f(forgotten))
```

This prevents repeatedly exploring clearly inferior paths.

## Completeness

SMA\* is **complete** if enough memory exists to store the shallowest solution path.

If memory is extremely limited, completeness may be lost.

## Optimality

SMA\* is **optimal** if sufficient memory is available.

With insufficient memory, it returns the best solution that can be found within the memory limit.

## Time Complexity

Worst-case time complexity can be very high because deleted nodes may need to be regenerated multiple times.

Approximate worst case:

```text
O(b^d)
```

Repeated regeneration increases computation time.

## Space Complexity

Space complexity is determined by the memory limit.

If memory capacity is **M**, then:

```text
O(M)
```

This is the major advantage over A\*.

## Comparison of A\* and SMA\*

| Feature | A\* | SMA\* |
| --- | --- | --- |
| Uses heuristics | Yes | Yes |
| Memory limit | No | Yes |
| Complete | Yes | Yes* |
| Optimal | Yes | Yes* |
| Space complexity | O(bᵈ) | O(M) |
| Node regeneration | No | Yes |

\*Provided sufficient memory is available.

## Advantages of Memory-Bounded Search

- Operates within fixed memory limits.
- Suitable for large search spaces.
- More practical than A\* for memory-constrained systems.
- Can still use powerful heuristic information.
- Produces good-quality solutions.

## Disadvantages

- May regenerate deleted nodes.
- Increased computation time.
- Implementation is more complex.
- Optimality depends on available memory.
- Performance may degrade when memory is very small.

## Applications

Memory-bounded search is used in:

- Robot navigation
- Autonomous vehicles
- Game playing
- Route planning
- Scheduling problems
- Embedded AI systems
- Space-constrained devices
- Real-time decision-making systems

## Practical Significance

Modern AI systems often face both:

- Large search spaces.
- Limited memory.

Memory-bounded search algorithms allow intelligent systems to solve problems that would be impossible using standard A\* search.

They are particularly valuable when:

- Memory is expensive.
- Search spaces are enormous.
- Approximate optimality is acceptable.

## Key Points

- Memory-bounded search limits memory usage during heuristic search.
- It is designed to overcome the memory limitation of A\*.
- SMA\* is the most important memory-bounded search algorithm.
- SMA\* deletes the **least promising node** when memory becomes full.
- Deleted nodes can be regenerated later.
- SMA\* uses **f(n)=g(n)+h(n)**.
- Space complexity is **O(M)**, where **M** is the available memory.
- Memory-bounded search trades memory efficiency for additional computation time.
