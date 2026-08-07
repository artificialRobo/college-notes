# Uniform Cost Search (UCS)

## Definition

**Uniform Cost Search (UCS)** is an **uninformed search algorithm** that expands the node with the **lowest cumulative path cost** from the initial state. Unlike Breadth-First Search (BFS), which expands nodes based on depth, UCS expands nodes based on the **total cost required to reach them**.

UCS is particularly useful when the **step costs are different**, and the objective is to find the **minimum-cost path** from the start state to the goal state.

**Core Idea:** Expand the node with the **smallest path cost**.

## Characteristics of UCS

- **Search Type:** Uninformed search
- **Expansion Strategy:** Lowest path cost first
- **Data Structure Used:** Priority Queue (Min-Priority Queue)
- **Completeness:** Yes (if all step costs are positive)
- **Optimality:** Yes (always finds the least-cost solution)

## Path Cost Function

In UCS, every node has an associated **path cost**, represented as:

```text
g(n)
```

Where:

- **g(n)** = total cost from the initial state to node **n**

The algorithm always selects the node with the **minimum value of g(n)** for expansion.

## Working Principle

Uniform Cost Search starts from the initial node with path cost **0**. It repeatedly removes the node with the **lowest cumulative cost** from the priority queue.

### Algorithm Steps

1. Insert the start node into the priority queue with cost **0**.
2. Remove the node with the lowest path cost.
3. If the node is the goal state, return the solution.
4. Otherwise, generate all successor nodes.
5. Calculate the cumulative cost for each successor.
6. Insert or update the successor in the priority queue if a lower-cost path is found.
7. Repeat until the goal is reached or the queue becomes empty.

## UCS Algorithm (Pseudo Code)

```text
UCS(start, goal):

    create a priority queue PQ
    insert start into PQ with cost 0

    while PQ is not empty:

        node = remove node with minimum cost

        if node = goal:
            return solution

        for each successor of node:

            new_cost = cost(node) + step_cost(node, successor)

            if successor is not visited
               or new_cost is lower than previous cost:

                update successor cost
                insert successor into PQ

    return failure
```

## Example

Consider the following weighted graph:

```text
        A
      /   \
   1 /     \ 5
    B       C
   / \     / \
 2/   \4 1/   \2
 D     E F     G
```

Suppose the goal node is **G**.

### Execution of UCS

Queue operations:

| Step | Expanded Node | Priority Queue (Cost) |
| --- | --- | --- |
| Start | A | A(0) |
| 1 | A | B(1), C(5) |
| 2 | B | D(3), C(5), E(5) |
| 3 | D | C(5), E(5) |
| 4 | C | E(5), F(6), G(7) |
| 5 | E | F(6), G(7) |
| 6 | F | G(7) |
| 7 | G | Goal Found |

### Solution Path

The minimum-cost path is:

```text
A -> C -> G
```

Total path cost:

```text
5 + 2 = 7
```

## Why UCS is Optimal

Uniform Cost Search always expands nodes in **increasing order of path cost**.

A goal node is accepted only when it is removed from the priority queue. At that moment, no other frontier node has a lower path cost, so the obtained solution is guaranteed to be the **least-cost solution**.

## Time and Space Complexity

Let:

- **b** = branching factor
- **C\*** = cost of the optimal solution
- **ε** = minimum positive step cost

### Time Complexity

```text
O(b^(1 + [C*/ε]))
```

### Space Complexity

```text
O(b^(1 + [C*/ε]))
```

UCS requires significant memory because all frontier nodes are stored in the priority queue.

## Properties of UCS

| Property | UCS |
| --- | --- |
| Complete | Yes |
| Optimal | Yes |
| Uses Heuristic | No |
| Data Structure | Priority Queue |
| Evaluation Function | g(n) |
| Suitable for | Weighted graphs |

## Advantages of UCS

- Finds the **minimum-cost path**.
- Works with **unequal step costs**.
- Complete when all edge costs are positive.
- Guarantees the optimal solution.
- Widely used in shortest-path problems.

## Disadvantages of UCS

- Requires a priority queue.
- High memory consumption.
- Can be slower than BFS when many low-cost paths exist.
- May expand a large number of nodes before reaching the goal.

## Uniform Cost Search vs Breadth-First Search

| Breadth-First Search (BFS) | Uniform Cost Search (UCS) |
| --- | --- |
| Expands shallowest node | Expands lowest-cost node |
| Uses Queue (FIFO) | Uses Priority Queue |
| Assumes equal step costs | Handles variable step costs |
| Optimal only for equal costs | Optimal for positive costs |
| Simpler to implement | Slightly more complex |

## Relationship with Dijkstra’s Algorithm

Uniform Cost Search is closely related to **Dijkstra’s shortest path algorithm**.

Both algorithms:

- expand the node with the lowest cumulative cost,
- use a priority queue,
- update path costs,
- find the shortest (minimum-cost) path.

## Applications of UCS

Uniform Cost Search is used in:

- Route finding and navigation systems
- Robot path planning
- Network routing
- Transportation and logistics
- Game AI
- Cost optimization problems

## Conclusion

**Uniform Cost Search (UCS)** is an uninformed search algorithm that expands the node having the **lowest cumulative path cost**. It uses a **priority queue** and the evaluation function **g(n)**. UCS is **complete and optimal** for problems with positive step costs and is mainly used to find the **minimum-cost path in weighted graphs**. The major limitation of UCS is its **high time and memory requirements**.
