# Simulated Annealing

## Introduction

**Simulated Annealing (SA)** is a **probabilistic local search algorithm** used for solving optimization problems. It is an extension of the **Hill Climbing algorithm** that allows occasional moves to worse states in order to escape local optima and continue exploring the search space.

The algorithm is inspired by the **annealing process in metallurgy**, where a material is heated to a high temperature and then cooled slowly to obtain a strong crystalline structure with minimum internal energy.

## Definition

Simulated Annealing is a local search algorithm that explores the search space by accepting both better and, with a certain probability, worse neighboring states, thereby increasing the likelihood of finding the global optimum.

Unlike Hill Climbing, Simulated Annealing can escape local maxima and local minima, making it more effective for complex optimization problems.

## Motivation for Simulated Annealing

Hill Climbing always moves to a better neighboring state.

This creates a major limitation.

Example:

```text
        Global Maximum
             *
            / \
           /   \
      *---*     \____
     /
    *
Local Maximum
```

Hill Climbing becomes trapped at the **local maximum**.

Simulated Annealing solves this problem by occasionally allowing **downhill moves**.

## Physical Analogy

In metallurgy:

1. Heat the material.
2. At high temperature, atoms move freely.
3. Slowly reduce the temperature.
4. Atoms settle into a low-energy configuration.

In optimization:

| Physical Process | Optimization |
| --- | --- |
| Material state | Candidate solution |
| Energy | Objective function |
| Temperature | Search randomness |
| Cooling | Reduced randomness |

The algorithm initially explores widely and gradually focuses on exploitation.

## Basic Idea

Simulated Annealing starts with:

- An initial solution.
- A high temperature.

At each iteration:

1. Generate a neighboring solution.
2. Compute the change in objective value.
3. Accept better solutions.
4. Sometimes accept worse solutions.
5. Gradually decrease the temperature.

As temperature decreases, the probability of accepting worse solutions becomes smaller.

## Working Principle

```text
Initial Solution
        |
        v
Generate Neighbor
        |
        v
Better Solution?
   /           \
Yes             No
 |               |
Accept        Accept with
Solution      Probability
        \     /
         v   v
     Update State
         |
         v
Decrease Temperature
         |
         v
Repeat Until Temperature Is Low
```

## Acceptance Probability

Suppose:

- Current state value = **E**
- Neighbor value = **E'**

For a minimization problem:

```text
ΔE = E' - E
```

### Better Solution

If

```text
ΔE < 0
```

always accept.

### Worse Solution

If

```text
ΔE > 0
```

accept with probability

```text
P = e^(-ΔE/T)
```

Where:

- **T** = Current temperature.
- **e** = Euler's constant.

This probability decreases as:

- Temperature decreases.
- The deterioration becomes larger.

## Acceptance Probability Example

Suppose:

```text
ΔE = 5
```

### At High Temperature

```text
T = 100
```

```text
P = e^(-5/100) = e^(-0.05) ≈ 0.951
```

Very high probability of acceptance.

### At Low Temperature

```text
T = 1
```

```text
P = e^(-5) ≈ 0.0067
```

Very low probability of acceptance.

Thus, the algorithm becomes increasingly conservative.

## Simulated Annealing Algorithm

**Input:** Initial state

**Output:** Approximate global optimum

```text
SimulatedAnnealing(initial_state)

1. current ← initial_state
2. T ← initial temperature

3. while T > Tmin do
4.     neighbor ← random neighbor
5.     ΔE ← cost(neighbor) - cost(current)

6.     if ΔE < 0 then
7.          current ← neighbor
8.     else
9.          accept neighbor with probability e^(−ΔE/T)

10.    decrease temperature

11. return current
```

## Example

Suppose we minimize the cost.

Current state:

```text
Cost = 20
```

Neighbor:

```text
Cost = 23
```

Then

```text
ΔE = 3
```

Assume

```text
T = 10
```

Acceptance probability:

```text
P = e^(-3/10)
```

```text
P ≈ 0.741
```

There is a **74.1% chance** of accepting the worse solution.

## Cooling Schedule

The **cooling schedule** determines how temperature decreases.

It is a crucial component of Simulated Annealing.

### Exponential Cooling

```text
T_new = αT
```

Where

```text
0 < α < 1
```

Example:

```text
α = 0.95
```

Temperatures:

```text
100
95
90.25
85.74
...
```

### Linear Cooling

```text
T_new = T - c
```

Where **c** is a constant.

### Logarithmic Cooling

```text
T = T₀ / log(1 + k)
```

Provides stronger theoretical convergence guarantees.

## Temperature and Search Behavior

### High Temperature

- Accepts many worse solutions.
- Strong exploration.
- Escapes local optima easily.

### Medium Temperature

- Balanced exploration and exploitation.

### Low Temperature

- Rarely accepts worse solutions.
- Behaves similarly to Hill Climbing.

## Graphical Illustration

```text
Value
 ^
 |
 |          *
 |        *   *
 |      *      *
 |   *
 | *
 +------------------------> State
```

Hill Climbing:

- Stops at the first peak.

Simulated Annealing:

- Can move downhill temporarily.
- May reach the higher peak.

## Comparison with Hill Climbing

| Feature | Hill Climbing | Simulated Annealing |
| --- | --- | --- |
| Moves only to better states | Yes | No |
| Accepts worse states | No | Yes |
| Escapes local optima | Poor | Good |
| Randomization | Minimal | Significant |
| Global optimum probability | Low | Higher |

## Advantages

- Escapes local optima.
- Explores the search space effectively.
- Applicable to large optimization problems.
- Simple implementation.
- Requires very little memory.
- Can approach the global optimum.

## Disadvantages

- Performance depends on the cooling schedule.
- May converge slowly.
- Parameter tuning is important.
- No guarantee of finding the global optimum in finite time.
- Can waste time exploring poor solutions.

## Time Complexity

Let:

- **I** = Number of temperature levels.
- **N** = Iterations per temperature.

Time complexity:

```text
O(I × N)
```

Actual performance depends on the cooling schedule.

## Space Complexity

Only the current state and a neighbor are stored.

Space complexity:

```text
O(1)
```

## Choice of Parameters

### Initial Temperature

Should be sufficiently high to allow exploration.

### Cooling Rate

Common values:

```text
0.8 ≤ α ≤ 0.99
```

Slow cooling usually produces better solutions.

### Minimum Temperature

The algorithm stops when:

```text
T ≤ T_min
```

### Iterations per Temperature

More iterations improve solution quality but increase computation time.

## Applications

Simulated Annealing is widely used in:

- Traveling Salesman Problem
- Job scheduling
- Timetable generation
- Circuit design
- VLSI layout optimization
- Resource allocation
- Vehicle routing
- Image processing
- Neural network optimization
- Robotics

## Practical Example: Traveling Salesman Problem

Current tour:

```text
A -> B -> C -> D -> A
```

Distance:

100 km.

Neighboring tour:

```text
A -> C -> B -> D -> A
```

Distance:

105 km.

Hill Climbing:

- Rejects immediately.

Simulated Annealing:

- May accept the longer tour.
- This may later lead to a tour of 90 km.

## Theoretical Convergence

With **infinitely slow cooling**, Simulated Annealing converges to the **global optimum** with probability approaching **1**.

In practice, finite cooling schedules are used, so the algorithm provides an approximate solution.

## Performance Characteristics

### Completeness

Not complete in finite time.

### Optimality

Not guaranteed in finite time.

Can approach the global optimum under suitable cooling schedules.

### Memory Usage

Very low.

### Robustness

Much more robust than Hill Climbing.

## Key Points

- Simulated Annealing is a **probabilistic local search algorithm**.
- It is inspired by the **annealing process in metallurgy**.
- It uses the acceptance probability

```text
P = e^(-ΔE/T)
```

- Better solutions are always accepted.
- Worse solutions may be accepted probabilistically.
- High temperature encourages exploration.
- Low temperature encourages exploitation.
- The **cooling schedule** controls the search behavior.
- Space complexity is **O(1)**.
- Simulated Annealing is more effective than Hill Climbing for avoiding local optima.
- It is widely used for **optimization problems** such as TSP, scheduling, routing, and circuit design.
