# Depth-First Search (DFS)

## Definition

**Depth-First Search (DFS)** is an **uninformed (blind) search algorithm** that explores the **deepest node first** before backtracking to explore other branches. It follows one path from the initial state until it reaches a goal node, a dead end, or the maximum depth, and then returns to explore alternative paths.

DFS is widely used in Artificial Intelligence for searching large state spaces where memory efficiency is important.

## Key Characteristics

- **Search type:** Uninformed search
- **Expansion strategy:** Deepest unexpanded node first
- **Data structure used:** Stack (LIFO – Last In, First Out) or recursion
- **Completeness:** No (in infinite-depth spaces)
- **Optimality:** No

## Working Principle

DFS starts from the **initial node** and repeatedly explores one child node until it cannot proceed further. When a node has no unvisited successors, the algorithm **backtracks** to the previous node and explores another branch.

### Algorithm Steps

1. Insert the initial node into the stack.
2. Mark the initial node as visited.
3. Repeat until the stack becomes empty:
   - Remove the top node from the stack.
   - If it is the goal node, return the solution.
   - Otherwise, generate its successor nodes.
   - Push all unvisited successors onto the stack.
4. If the stack becomes empty, return failure.

## DFS Algorithm (Pseudo Code)

```text
DFS(start, goal):

    create an empty stack S
    push start into S
    mark start as visited

    while S is not empty:

        node = pop(S)

        if node = goal:
            return solution

        for each successor of node:

            if successor is not visited:
                mark successor as visited
                push(successor)

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

Suppose the goal node is **G**.

### Stack Operations

| Step | Stack |
| --- | --- |
| Start | A |
| Expand A | C, B |
| Expand B | C, E, D |
| Expand D | C, E |
| Expand E | C |
| Expand C | G, F |
| Expand F | G |
| Expand G | Goal Found |

### Order of Expansion

```text
A -> B -> D -> E -> C -> F -> G
```

DFS explores the left subtree completely before moving to the right subtree.

## State Space Exploration

DFS explores nodes by moving as deep as possible.

| Depth | Nodes Explored |
| --- | --- |
| 0 | A |
| 1 | B |
| 2 | D |
| Backtrack | E |
| Backtrack | C |
| 2 | F |
| 2 | G |

The algorithm backtracks whenever it reaches a leaf node or a node with no unexplored successors.

## Time and Space Complexity

Let:

- **b** = branching factor
- **m** = maximum depth of the search tree

### Time Complexity

In the worst case, DFS explores all nodes up to depth **m**.

```text
O(b^m)
```

### Space Complexity

DFS stores only the current path from the root to the deepest node.

```
O(bm)
```

DFS is significantly more memory-efficient than BFS.

## Properties of DFS

| Property | DFS |
| --- | --- |
| Complete | No |
| Optimal | No |
| Time Complexity | O(b^m) |
| Space Complexity | O(bm) |
| Data Structure | Stack (LIFO) |
| Search Direction | Deepest node first |

## Advantages of DFS

- Requires **less memory** than BFS.
- Simple and easy to implement.
- Suitable for exploring deep search spaces.
- Useful for topological sorting, cycle detection, and graph traversal.
- Can reach a solution quickly if it lies deep in the search tree.

## Disadvantages of DFS

- Does not guarantee the shortest path.
- Not optimal.
- May get stuck in infinite paths if the search space is unbounded.
- May explore a very deep branch unnecessarily before finding the goal.

## Applications of DFS in Artificial Intelligence

Depth-First Search is commonly used in:

- Puzzle solving
- Maze navigation
- Game tree exploration
- Graph traversal
- Cycle detection
- Topological sorting
- Constraint satisfaction problems

## DFS vs BFS

| DFS | BFS |
|-----|-----|
| Uses Stack | Uses Queue |
| Explores depth first | Explores level by level |
| Low memory usage | High memory usage |
| Not optimal | Optimal (equal costs) |
| May not be complete | Complete |
| Better for deep solutions | Better for shallow solutions |

## Limitations

DFS becomes inefficient when:

- the search tree contains infinite paths,
- the goal is located near the root,
- the shortest path is required,
- the search space has many deep branches.

To overcome some of these limitations, **Depth-Limited Search (DLS)** and **Iterative Deepening Search (IDS)** are often used.

## Conclusion

**Depth-First Search (DFS)** is an uninformed search algorithm that expands the **deepest unexpanded node first** using a **stack (LIFO)**. It explores one branch completely before backtracking to explore other branches. DFS has **time complexity O(b^m)** and **space complexity O(bm)**. It is memory-efficient and suitable for deep search problems, but it is **not complete and not optimal**, and it does not guarantee the shortest path.
