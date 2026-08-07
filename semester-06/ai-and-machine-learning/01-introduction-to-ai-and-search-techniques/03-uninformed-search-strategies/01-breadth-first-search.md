# Breadth-First Search (BFS)

## Definition

**Breadth-First Search (BFS)** is an **uninformed (blind) search algorithm** that explores the search tree **level by level**. It expands all nodes at the current depth before moving to nodes at the next depth level.

BFS is one of the most fundamental search algorithms in Artificial Intelligence and is widely used when the goal is expected to be close to the initial state.

**Core Idea:** Expand the **shallowest unexpanded node first**.

## Characteristics of BFS

- **Search Type:** Uninformed search
- **Expansion Strategy:** Level-order traversal
- **Data Structure Used:** Queue (FIFO – First In, First Out)
- **Completeness:** Yes (if the branching factor is finite)
- **Optimality:** Yes (when all step costs are equal)

## Working Principle

BFS starts from the **initial state (root node)** and explores all neighboring nodes before moving to the next level.

The algorithm maintains a **queue** containing nodes that have been generated but not yet expanded.

### Algorithm Steps

1. Insert the initial node into the queue.
2. Mark the initial node as visited.
3. Repeat until the queue becomes empty:
   - Remove the front node from the queue.
   - If it is the goal node, terminate and return the solution.
   - Otherwise, generate all successor nodes.
   - Add all unvisited successor nodes to the rear of the queue.

## BFS Algorithm (Pseudo Code)

```text
BFS(start, goal):

    create an empty queue Q
    enqueue start into Q
    mark start as visited

    while Q is not empty:

        node = dequeue(Q)

        if node = goal:
            return solution

        for each successor of node:

            if successor is not visited:
                mark successor as visited
                enqueue(successor)

    return failure
```

## Example

Consider the following search tree:

```text
            A
          /   \
         B     C
        / \   / \
       D   E F   G
```

Suppose the goal node is **F**.

### BFS Traversal

Queue Operations:

| Step | Queue |
| --- | --- |
| Start | A |
| Expand A | B, C |
| Expand B | C, D, E |
| Expand C | D, E, F, G |
| Expand D | E, F, G |
| Expand E | F, G |
| Expand F | Goal Found |

### Order of Expansion

```text
A -> B -> C -> D -> E -> F
```

The goal **F** is found at **depth 2**.

## State Space illustration

BFS explores nodes level by level.

| Depth | Nodes |
| --- | --- |
| 0 | A |
| 1 | B, C |
| 2 | D, E, F, G |

Since BFS explores all nodes at a given depth before moving deeper, it always finds the **shortest path (minimum number of edges)** in an unweighted graph.

---

## Time and Space Complexity

Let:

- **b** = branching factor (maximum number of children per node)
- **d** = depth of the shallowest goal node

### Time Complexity

BFS generates all nodes up to depth **d**.

```text
1 + b + b^2 + ... + b^d
```

Therefore,

```text
O(b^d)
```

### Space Complexity

BFS stores all generated frontier nodes in memory.

```text
O(b^d)
```

The **space requirement is the major drawback** of BFS.

## Properties of BFS

| Property | BFS |
| --- | --- |
| Complete | Yes |
| Optimal | Yes (equal step cost) |
| Time Complexity | O(b^d) |
| Space Complexity | O(b^d) |
| Data Structure | Queue (FIFO) |
| Search Direction | Shallowest node first |

## Advantages of BFS

- Guaranteed to find a solution if one exists.
- Finds the shortest path in an unweighted graph.
- Simple and easy to implement.
- Useful when the goal is near the initial state.
- Explores the search space systematically.

## Disadvantages of BFS

- Requires a large amount of memory.
- Not suitable for very large search spaces.
- Expands many unnecessary nodes.
- Performance decreases when the goal is located at a large depth.

## Applications of BFS in Artificial Intelligence

Breadth-First Search is widely used in:

- Pathfinding in unweighted graphs
- Robot navigation
- Web crawling
- Social network analysis
- Puzzle solving (8-puzzle, water jug problem, etc.)
- Broadcasting and communication networks

## BFS vs DFS

| BFS | DFS |
| --- | --- |
| Uses Queue | Uses Stack |
| Explores level by level | Explores depth first |
| Complete | May not be complete |
| Optimal (equal costs) | Not optimal |
| High memory usage | Low memory usage |
| Better for shallow solutions | Better for deep solutions |

## Limitations

BFS becomes inefficient when:

- the branching factor is very high,
- the search depth is large,
- memory resources are limited.

In such cases, algorithms such as **Depth-First Search (DFS)**, **Uniform Cost Search (UCS)**, or **A\* Search** are often preferred.

## Conclusion

**Breadth-First Search (BFS)** is an uninformed search algorithm that expands the **shallowest node first** using a **FIFO queue**. It explores the search tree level by level and is **complete** and **optimal** when all step costs are equal. BFS has **time complexity O(b^d)** and **space complexity O(b^d)**. It is commonly used for finding the **shortest path in unweighted graphs**, but its major limitation is **high memory consumption**.
