# Alpha-Beta Pruning

## Introduction

The **Minimax algorithm** guarantees an optimal decision in deterministic games, but it becomes computationally expensive because it explores **every possible node in the game tree**. In games such as chess, the number of possible game states is extremely large, making exhaustive search impractical.

**Alpha-Beta Pruning** is an optimization technique for the Minimax algorithm that **reduces the number of nodes evaluated** during the search process. It eliminates branches of the game tree that **cannot affect the final decision**, thereby improving search efficiency while producing the **same optimal result** as the Minimax algorithm.

## Definition

**Alpha-Beta Pruning** is a search optimization algorithm used in adversarial game playing that **prunes unnecessary branches of the game tree**, allowing the AI to compute the **optimal move with fewer node evaluations**.

It improves the efficiency of Minimax without changing the final decision.

## Need for Alpha-Beta Pruning

The Minimax algorithm has a time complexity of:

O(b^d)

Where:

- **b** = branching factor
- **d** = depth of the game tree

As the branching factor and depth increase, the number of nodes grows exponentially. Alpha-Beta pruning reduces this search space and allows the AI to search **deeper levels of the game tree within the same time limit**.

## Basic Idea of Alpha-Beta Pruning

During the Minimax search, the algorithm maintains two values:

- **Alpha (α):** The best value that the MAX player can guarantee.
- **Beta (β):** The best value that the MIN player can guarantee.

Whenever it becomes clear that a branch **cannot improve the current decision**, that branch is **pruned (cut off)** and no further nodes in that branch are explored.

## Alpha (α) and Beta (β) Values

### Alpha (α)

Alpha represents the **highest value found so far** for the MAX player.

Initially:

α = -∞

The value of α increases whenever MAX discovers a better move.

### Beta (β)

Beta represents the **lowest value found so far** for the MIN player.

Initially:

β = +∞

The value of β decreases whenever MIN discovers a better move.

## Pruning Condition

A branch is pruned when:

α ≥ β

This condition indicates that further exploration of the branch **cannot influence the final decision**.

## Working of Alpha-Beta Pruning

Consider the following game tree.

```text
                 MAX
               /     \
            MIN      MIN
           /   \     /   \
          3     5   2     9
```

### Step 1: Initialize

- α = -∞
- β = +∞

### Step 2: Evaluate Left MIN Node

Evaluate **3**.

β = min(+∞, 3) = 3

Evaluate **5**.

β = min(3, 5) = 3

Left MIN node returns **3**.

### Step 3: Update MAX Node

α = max(-∞, 3) = 3

### Step 4: Evaluate Right MIN Node

Current values:

- α = 3
- β = +∞

Evaluate **2**.

β = min(+∞, 2) = 2

Now:

- α = 3
- β = 2

Since:

**α ≥ β**

3 ≥ 2

The remaining node **9** is **pruned**.

## Pruned Game Tree

```text
                 MAX
               /     \
            MIN      MIN
           /   \     /
          3     5   2
                    ×
```

The node **9** is never evaluated.

The final decision remains the same as the Minimax algorithm.

## Step-by-Step Example

Consider the following game tree.

```text
                    MAX
              /       |       \
            MIN      MIN      MIN
           /  \      /  \     /  \
          5    6    7    4   5    8
```

### First MIN Node

MIN chooses:

min(5, 6) = 5

MAX updates:

α = 5

### Second MIN Node

Evaluate **7**.

β = 7

Evaluate **4**.

β = 4

MIN returns **4**.

MAX still has:

α = 5

### Third MIN Node

Evaluate **5**.

β = 5

Now:

- α = 5
- β = 5

Since:

**α ≥ β**

The node **8** is pruned.

## Alpha-Beta Pruning Algorithm

### Pseudocode

```text
ALPHA-BETA(state, depth, α, β, maximizingPlayer)

if terminal state then
    return utility(state)

if maximizingPlayer then
    value = -∞

    for each child do
        value = max(value,
                    ALPHA-BETA(child,
                               depth-1,
                               α,
                               β,
                               false))

        α = max(α, value)

        if α ≥ β then
            break

    return value

else
    value = +∞

    for each child do
        value = min(value,
                    ALPHA-BETA(child,
                               depth-1,
                               α,
                               β,
                               true))

        β = min(β, value)

        if α ≥ β then
            break

    return value
```

## Alpha-Beta Search Process

```text
Start Search
      ↓
Initialize α = -∞
Initialize β = +∞
      ↓
Explore Child Nodes
      ↓
Update α and β
      ↓
Check α ≥ β
      ↓
Prune Remaining Branches
      ↓
Return Optimal Move
```

## Time Complexity

Assume:

- **b** = branching factor
- **d** = depth of the game tree

### Worst Case

If no pruning occurs:

O(b^d)

This is identical to Minimax.

### Best Case

With perfect move ordering:

O(b^(d/2))

This allows the AI to search approximately **twice as deep** as Minimax within the same computational time.

### Average Case

Performance depends on the **order in which moves are explored**.

Better move ordering results in **more pruning** and faster search.

## Space Complexity

Alpha-Beta pruning performs **depth-first search**, so the space complexity is:

O(bd)

This is the same as the Minimax algorithm.

## Effect of Move Ordering

The efficiency of Alpha-Beta pruning strongly depends on move ordering.

### Good Move Ordering

- Best moves explored first
- Maximum pruning
- Faster search
- Deeper exploration

### Poor Move Ordering

- Worst moves explored first
- Minimal pruning
- Performance close to Minimax

Modern chess engines use sophisticated **move-ordering heuristics** to maximize pruning.

## Advantages of Alpha-Beta Pruning

- Produces the **same optimal decision as Minimax**.
- Explores significantly fewer nodes.
- Reduces computation time.
- Enables deeper game-tree searches.
- Improves performance in complex games.
- Widely used in game-playing AI systems.

## Limitations of Alpha-Beta Pruning

### Depends on Move Ordering

Poor move ordering reduces pruning efficiency.

### Still Exponential

Worst-case complexity remains exponential.

### Less Effective in Very Large Games

Games such as Go require additional techniques such as **Monte Carlo Tree Search (MCTS)**.

### Not Suitable for Chance Nodes

Games involving randomness require algorithms such as **Expectiminimax**.

## Minimax vs Alpha-Beta Pruning

| Feature | Minimax | Alpha-Beta Pruning |
| --- | --- | --- |
| Explores all nodes | Yes | No |
| Optimal decision | Yes | Yes |
| Prunes branches | No | Yes |
| Worst-case time | O(b^d) | O(b^d) |
| Best-case time | O(b^d) | O(b^(d/2)) |
| Search efficiency | Lower | Higher |

## Applications

Alpha-Beta pruning is widely used in:

- Chess engines
- Checkers programs
- Othello AI
- Strategic board games
- Adversarial search systems
- Automated planning

## Key Terms

| Term | Meaning |
| --- | --- |
| Alpha (α) | Best value guaranteed for MAX |
| Beta (β) | Best value guaranteed for MIN |
| Pruning | Eliminating unnecessary branches |
| Cutoff | Stopping exploration of a branch |
| Move Ordering | Order of exploring child nodes |
| Adversarial Search | Search involving competing players |

---

# Example of Pruning

```text
               MAX
             /     \
          MIN      MIN
         /  \      / \
        4    6    2   9
```

Evaluation:

- Left MIN returns **4**
- α = 4

Right MIN evaluates **2**

β = 2

Since:

**α = 4 ≥ β = 2**

The node **9** is pruned.

## Summary

**Alpha-Beta pruning** is an optimization technique for the **Minimax algorithm** that eliminates branches of the game tree that cannot affect the final decision. It maintains two values: **alpha (α)**, representing the best value for the MAX player, and **beta (β)**, representing the best value for the MIN player. A branch is pruned when **α ≥ β**. Alpha-Beta pruning produces the same optimal move as Minimax while exploring fewer nodes, reducing computation time and allowing deeper searches. Its best-case time complexity is **O(b^(d/2))**, making it significantly more efficient than the standard Minimax algorithm.

## Important Questions

1. What is Alpha-Beta pruning in AI?
2. Explain the concepts of alpha and beta values.
3. Describe the pruning condition **α ≥ β**.
4. Explain the working of Alpha-Beta pruning with an example.
5. Write the pseudocode of the Alpha-Beta pruning algorithm.
6. Compare Minimax and Alpha-Beta pruning.
7. Discuss the time and space complexity of Alpha-Beta pruning.
8. Explain the effect of move ordering on Alpha-Beta pruning efficiency.
