# A* Search Algorithm

## Introduction

The **A\* (A-star) Search Algorithm** is one of the most important and widely used **informed search algorithms** in Artificial Intelligence. It combines the advantages of **Uniform Cost Search (UCS)** and **Greedy Best-First Search** by considering both the actual path cost and the estimated cost to the goal.

A\* search is designed to find the **least-cost (optimal) path** from a start node to a goal node.

## Definition

A\* search is an informed search algorithm that selects the node with the minimum estimated total cost, where the total cost is the sum of the path cost from the start node and the heuristic estimate to the goal.

The algorithm is widely used in **pathfinding, navigation systems, robotics, game development, and automated planning**.

## Basic Idea of A\*

A\* evaluates each node using the function:

```text
f(n) = g(n) + h(n)
```

Where:

- **g(n)** = Actual cost from the start node to node **n**
- **h(n)** = Estimated cost from node **n** to the goal
- **f(n)** = Estimated total cost of the solution path through node **n**

The algorithm always expands the node with the **smallest f(n) value**.

## Components of the Evaluation Function

### Path Cost g(n)

Represents the exact cost from the initial node to the current node.

Example:

```text
S ----2---- A ----3---- B
```

Then

```text
g(A) = 2, g(B) = 5
```

### Heuristic Cost h(n)

Represents the estimated remaining cost to reach the goal.

The heuristic is problem-dependent.

Examples:

- Straight-line distance
- Manhattan distance
- Euclidean distance

### Total Cost f(n)

Represents the estimated total solution cost.

Example:

```text
g(n) = 4, h(n) = 5
```

Then

```text
f(n) = 4 + 5 = 9
```

## Working Principle of A\*

A\* maintains two lists.

### OPEN List

Contains generated nodes that are candidates for expansion.

### CLOSED List

Contains nodes that have already been expanded.

At each step:

1. Select the node with the lowest **f(n)**.
2. Remove it from OPEN.
3. Add it to CLOSED.
4. Generate its successors.
5. Update costs.
6. Repeat until the goal is reached.

## A\* Search Algorithm

**Input:** Start node, goal node

**Output:** Optimal path from start to goal

```text
A*(start, goal)

1. OPEN ← {start}
2. CLOSED ← ∅
3. g(start)=0
4. f(start)=h(start)

5. while OPEN is not empty do
6.     n ← node with minimum f(n)
7.     if n is goal then
8.         return solution path
9.     move n from OPEN to CLOSED
10.    generate successors of n
11.    for each successor s do
12.        compute g(s)
13.        compute f(s)=g(s)+h(s)
14.        if s is not in OPEN or CLOSED then
15.            insert s into OPEN
16.        else if better path found then
17.            update parent and costs
18. return Failure
```

## Example of A\* Search

Consider the graph:

```text
        S
      /   \
     A     B
    / \     \
   C   D     G
```

Edge costs:

| Edge | Cost |
| --- | --- |
| S–A | 1 |
| S–B | 4 |
| A–C | 2 |
| A–D | 5 |
| B–G | 2 |
| D–G | 1 |

Heuristic values:

| Node | h(n) |
| --- | --- |
| S | 4 |
| A | 3 |
| B | 2 |
| C | 4 |
| D | 1 |
| G | 0 |

### Step 1

Start node:

| Node | g | h | f |
| --- | --- | --- | --- |
| S | 0 | 4 | 4 |

OPEN = {S}

### Step 2

Expand **S**.

Generate A and B.

| Node | g | h | f |
| --- | --- | --- | --- |
| A | 1 | 3 | 4 |
| B | 4 | 2 | 6 |

OPEN = {A, B}

Choose **A**.

### Step 3

Expand A.

Generate C and D.

| Node | g | h | f |
| --- | --- | --- | --- |
| C | 3 | 4 | 7 |
| D | 6 | 1 | 7 |
| B | 4 | 2 | 6 |

Choose **B**.

### Step 4

Expand B.

Generate G.

| Node | g | h | f |
| --- | --- | --- | --- |
| G | 6 | 0 | 6 |
| C | 3 | 4 | 7 |
| D | 6 | 1 | 7 |

Choose **G**.

Goal reached.

Optimal path:

```text
S -> B -> G
```

Total cost:

```text
4 + 2 = 6
```

## Search Tree Illustration

```text
          S(4)
         /    \
      A(4)   B(6)
      /  \      \
   C(7) D(7)   G(6)
```

The node with the **smallest f-value** is expanded first.

## Properties of A\*

### Completeness

A\* is **complete** if:

- The branching factor is finite.
- Edge costs are positive.

### Optimality

A\* is **optimal** when the heuristic is **admissible**.

An admissible heuristic satisfies

```text
h(n) ≤ h*(n)
```

where **h\*(n)** is the true remaining cost.

### Optimal Efficiency

Among all optimal search algorithms using the same heuristic, A\* expands the fewest nodes.

## Time Complexity

Worst-case time complexity:

```text
O(b^d)
```

Where:

- **b** = Branching factor
- **d** = Depth of the optimal solution

The actual performance depends heavily on heuristic quality.

## Space Complexity

A\* stores all generated nodes.

Worst-case space complexity:

```text
O(b^d)
```

Memory consumption is the major limitation of A\*.

## Effect of Heuristic Quality

### h(n)=0

A\* becomes **Uniform Cost Search**.

### Perfect Heuristic

```text
h(n) = h*(n)
```

A\* expands only the nodes on the optimal path.

### Overestimating Heuristic

If

```text
h(n) > h*(n)
```

the heuristic becomes **inadmissible**.

A\* may lose optimality.

## Admissible and Consistent Heuristics

### Admissible

Never overestimates.

Guarantees optimal solutions.

### Consistent

Satisfies

```text
h(n) ≤ c(n,n') + h(n')
```

Consistency ensures:

- No need to reopen closed nodes.
- More efficient implementation.

Every consistent heuristic is admissible.

## Comparison with Other Search Algorithms

| Algorithm | Uses Heuristic | Optimal | Complete |
| --- | --- | --- | --- |
| BFS | No | Yes | Yes |
| DFS | No | No | No |
| UCS | No | Yes | Yes |
| Greedy Best-First | Yes | No | Not always |
| A\* | Yes | Yes* | Yes* |

\*With an admissible and consistent heuristic.

## Advantages of A\*

- Finds optimal paths.
- Uses heuristic information effectively.
- Complete under suitable conditions.
- Widely applicable.
- More efficient than uninformed search algorithms.

## Disadvantages of A\*

- Very high memory consumption.
- Performance depends on heuristic quality.
- Can be slow in extremely large search spaces.
- May require sophisticated heuristic design.

## Applications

A\* is extensively used in:

- GPS navigation systems
- Robot motion planning
- Video game pathfinding
- Autonomous vehicles
- Network routing
- Automated planning
- Logistics optimization
- Puzzle solving

## Practical Example: GPS Navigation

When finding the shortest route:

- **g(n)** = Distance traveled so far.
- **h(n)** = Straight-line distance to the destination.
- **f(n)** = Estimated total travel distance.

A\* chooses the road segment with the smallest estimated total distance.

## Key Points

- A\* is an **informed search algorithm**.
- It uses the evaluation function **f(n)=g(n)+h(n)**.
- **g(n)** is the actual path cost.
- **h(n)** is the heuristic estimate.
- The node with the **minimum f(n)** is expanded first.
- A\* is **complete and optimal** with an admissible heuristic.
- Memory complexity is **O(b^d)**.
- A\* combines the strengths of **Uniform Cost Search** and **Greedy Best-First Search**.
- The quality of the heuristic directly affects search efficiency.
