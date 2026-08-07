# Depth-Limited Search (DLS)

## Definition

**Depth-Limited Search (DLS)** is an **uninformed search algorithm** that is a modified version of **Depth-First Search (DFS)**. In DLS, the search is restricted to a **predetermined depth limit**, and nodes beyond this limit are not expanded.

The main purpose of DLS is to prevent DFS from exploring infinitely deep paths and to control the search depth.

**Core Idea:** Explore nodes depth-first, but **do not expand nodes beyond a specified depth limit**.

## Key Characteristics

- **Search type:** Uninformed search
- **Expansion strategy:** Deepest node first within a fixed depth limit
- **Data structure used:** Stack (LIFO) or recursion
- **Completeness:** No (unless the depth limit is greater than or equal to the goal depth)
- **Optimality:** No

## Working Principle

Depth-Limited Search behaves like DFS but stops expanding nodes once the specified depth limit is reached.

If the goal node is found within the depth limit, the search succeeds. Otherwise, the algorithm returns either **failure** or **cutoff**, indicating that the search was terminated because the depth limit was reached.

### Algorithm Steps

1. Start from the initial node.
2. Expand nodes in a depth-first manner.
3. Keep track of the current depth.
4. If the current depth equals the depth limit:
   - Do not expand the node further.
   - Return **cutoff**.
5. If the goal node is found, return the solution.
6. If all paths within the depth limit are explored, return failure.

## DLS Algorithm (Pseudo Code)

```text
DLS(node, goal, limit):

    if node = goal:
        return solution

    else if limit = 0:
        return cutoff

    else:

        cutoff_occurred = false

        for each successor of node:

            result = DLS(successor, goal, limit - 1)

            if result = cutoff:
                cutoff_occurred = true

            else if result ≠ failure:
                return result

        if cutoff_occurred:
            return cutoff
        else:
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
      /
     H
```

Suppose the **depth limit = 2** and the goal node is **H**.

### Search Process

Nodes explored:

```text
A -> B -> D
```

At node **D**, the depth limit is reached.

Node **H** is **not expanded** because it lies at **depth 3**.

### Result

The algorithm returns **cutoff** because the goal exists beyond the specified depth limit.

## State Space Exploration

Assume depth limit = 2.

| Depth | Nodes Explored |
| --- | --- |
| 0 | A |
| 1 | B, C |
| 2 | D, E, F, G |
| 3 | Not explored |

Nodes at depth 3 and beyond are ignored.

## Cutoff vs Failure

A unique feature of DLS is that it distinguishes between **failure** and **cutoff**.

### Failure

Occurs when:

- the goal does not exist within the search space explored,
- and no cutoff occurred.

### Cutoff

Occurs when:

- the search reached the depth limit,
- and deeper nodes were not explored.

This distinction is important for algorithms such as **Iterative Deepening Search (IDS)**.

## Time and Space Complexity

Let:

- **b** = branching factor
- **l** = depth limit

### Time Complexity

DLS explores all nodes up to depth **l**.

```text
O(b^l)
```

### Space Complexity

DLS stores only the current search path.

```text
O(bl)
```

Like DFS, DLS is memory-efficient.

## Properties of DLS

| Property | DLS |
| --- | --- |
| Complete | No |
| Optimal | No |
| Time Complexity | O(b^l) |
| Space Complexity | O(bl) |
| Data Structure | Stack / Recursion |
| Search Direction | Depth-first with limit |

## Advantages of DLS

- Prevents infinite recursion.
- Uses less memory than BFS.
- Allows control over search depth.
- Suitable when the approximate depth of the goal is known.
- Forms the basis of **Iterative Deepening Search (IDS)**.

## Disadvantages of DLS

- May miss the goal if the depth limit is too small.
- Not optimal.
- Requires choosing an appropriate depth limit.
- Can return cutoff even when a solution exists deeper in the tree.

## Applications of DLS

Depth-Limited Search is used in:

- Game tree search
- Puzzle solving
- Robot navigation
- Constraint satisfaction problems
- Planning systems
- As a component of **Iterative Deepening Search (IDS)**

## DLS vs DFS

| DFS | DLS |
| --- | --- |
| No depth restriction | Has a depth limit |
| May enter infinite paths | Prevents infinite search |
| May consume more time in deep trees | Restricts search depth |
| No cutoff condition | Returns cutoff at depth limit |
| Better when depth is unknown | Better when depth is approximately known |

## Choosing the Depth Limit

The effectiveness of DLS depends on selecting a suitable depth limit.

- **Limit too small:** Goal may not be found.
- **Limit too large:** Behaves similarly to DFS.
- **Limit close to goal depth:** Efficient search with controlled memory.

## Conclusion

**Depth-Limited Search (DLS)** is an uninformed search algorithm that performs **Depth-First Search with a fixed depth limit**. It expands nodes only up to the specified depth and returns **cutoff** when the limit is reached. DLS has **time complexity O(b^l)** and **space complexity O(bl)**. It is memory-efficient and prevents infinite-depth exploration, but it is **not complete and not optimal** unless the depth limit is chosen appropriately.
