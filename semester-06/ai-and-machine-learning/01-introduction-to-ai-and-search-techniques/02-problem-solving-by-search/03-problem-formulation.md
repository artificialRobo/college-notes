# Problem formulation

## Introduction

**Problem formulation** is the process of converting a real-world problem into a formal representation that can be solved by an Artificial Intelligence (AI) system. It is one of the most important steps in AI because the efficiency and correctness of the solution largely depend on how the problem is represented.

A problem-solving agent cannot search for a solution until the problem has been formulated properly. Problem formulation defines the **initial state, possible actions, transition model, goal state, and path cost**, which together form the basis of search algorithms such as **BFS, DFS, Uniform Cost Search, and A\***.

A well-formulated problem reduces unnecessary search, improves computational efficiency, and enables the agent to find an optimal solution.

---

## Definition

**Problem formulation** is the process of representing a problem in terms of states, actions, transitions, goals, and costs so that an AI agent can search for a sequence of actions that leads from the initial state to the goal state.

---

## Purpose of problem formulation

The main objectives of problem formulation are:

- To clearly define the problem.
- To represent the problem mathematically or symbolically.
- To identify all possible states.
- To specify allowable actions.
- To define the goal condition.
- To enable systematic search for a solution.

---

## Why problem formulation is important

Problem formulation determines:

- What the agent searches.
- Where the search begins.
- When the search ends.
- Which solution is considered optimal.

A poor problem formulation may:

- Increase time complexity.
- Increase memory usage.
- Produce incorrect solutions.
- Make the search impossible.

---

## Components of problem formulation

A search problem is formally defined by **five major components**.

### 1. Initial state

The initial state specifies the starting condition of the agent.

It represents the state from which the search begins.

**Example**

A robot is located at position **A**.

Initial state:

**A**

### 2. State space

The **state space** is the set of all possible states reachable from the initial state by applying available actions.

Example

For a route-finding problem:

```
Patna
 │
Varanasi
 │
Prayagraj
 │
Kanpur
 │
Delhi
```

The state space includes all cities reachable through available roads.

A large state space increases search complexity.

### 3. Actions (operators)

Actions define the possible operations that can be performed in a given state.

Actions transform one state into another.

**Example**

For a robot:

- Move left
- Move right
- Move forward
- Pick object

For route planning:

- Travel to a neighboring city

### 4. Transition model

The **transition model** describes the result of performing an action in a particular state.

It is represented as:

```Result(State, Action) -> New State```

**Example**

```
Result(Patna, Travel to Varanasi)
        ↓
Varanasi
```

The transition model defines the connectivity between states.

### 5. Goal test

The **goal test** determines whether the current state satisfies the desired objective.

It returns:

- TRUE if the goal is reached.
- FALSE otherwise.

**Example**

Goal: Reach Delhi

```
Current State = Delhi
Goal Test = TRUE
```

### 6. Path cost function

The path cost function assigns a numerical cost to each path.

The total cost is usually the sum of individual action costs.

### Example

| Route | Cost |
| --- | --- |
| Patna -> Varanasi | 250 |
| Varanasi -> Prayagraj | 120 |
| Prayagraj -> Kanpur | 200 |
| Kanpur -> Delhi | 450 |

Total path cost:

250 + 120 + 200 + 450 = 1020

The objective is often to **minimize path cost**.

---

## Formal representation of a search problem

A problem is represented as:

```P = (S, A, T, G, C)```

Where:

- **S** = State space
- **A** = Actions
- **T** = Transition model
- **G** = Goal test
- **C** = Path cost

This formal representation is used by AI search algorithms.

---

## Problem formulation process

The process of problem formulation involves the following steps.

### Step 1: Understand the problem

Identify:

- The objective
- Constraints
- Available information

### Step 2: Define the state space

Determine all possible configurations of the environment.

### Step 3: Specify actions

Identify all actions available to the agent.

### Step 4: Define transitions

Determine how actions change states.

### Step 5: Specify the goal

Clearly define the desired final state.

### Step 6: Define the cost function

Determine the cost associated with each action or path.

---

## Example: route-finding problem

Consider the problem of traveling from Patna to Delhi.

### Initial state

Patna

### Goal state

Delhi

### State space

```
Patna
 │
Varanasi
 │
Prayagraj
 │
Kanpur
 │
Delhi
```

### Actions

Travel to connected cities.

### Transition model

```
Result(Patna, Go to Varanasi)
    |
    V
Varanasi
```

### Goal test

Current State = Delhi

### Path cost

Distance traveled.

The search algorithm will determine the lowest-cost route.

---

## Example: vacuum cleaner problem

A vacuum-cleaning robot operates in two rooms.

### States

The state consists of:

- Robot location
- Cleanliness of both rooms

### Example:

```(Room A, Dirty, Clean)```

---

### Initial state

```(Room A, Dirty, Dirty)```

### Goal state

```(Room A or B, Clean, Clean)```

### Actions

- Move Left
- Move Right
- Suck

### Transition example

```
Result((A, Dirty, Dirty), Suck)
        ↓
(A, Clean, Dirty)
```

### Path cost

Number of actions performed.

---

## Example: 8-puzzle problem

The 8-puzzle consists of eight numbered tiles and one blank space.

### Initial state

1 2 3
4 _ 6
7 5 8

### Goal state

1 2 3
4 5 6
7 8 _

### Actions

Move the blank:

- Up
- Down
- Left
- Right

### Transition model

Moving the blank changes the tile configuration.

### Goal test

Check whether the current arrangement matches the goal configuration.

---

## Good problem formulation

A good problem formulation should satisfy the following properties.

### Complete

All necessary information is included.

### Consistent

Actions and transitions do not contradict each other.

### Efficient

Irrelevant states are excluded.

### Simple

The representation should be easy to understand and implement.

---

## State-space representation

A problem can be represented as a **state-space graph**.

```
      A
    /   \
   B     C
  / \   / \
 D   E F   G
```

Where:

- Nodes represent states.
- Edges represent actions.

Search algorithms explore this graph to find a path from the initial state to the goal state.

---

## Types of problem formulation

### Single-state formulation

The agent has complete knowledge of the current state.

Example:

Chess.

### Multiple-state formulation

The exact current state is uncertain.

Example:

Medical diagnosis with incomplete information.

### Contingency formulation

Future actions depend on observations.

Example:

Robot navigation with sensors.

### Exploration formulation

The state space is initially unknown.

Example:

A robot exploring a new environment.

---

## Advantages of proper problem formulation

- Reduces search complexity.
- Improves solution quality.
- Enables optimal search.
- Saves computation time.
- Reduces memory usage.
- Simplifies algorithm design.

---

## Limitations

- Complex real-world problems are difficult to formulate.
- Large state spaces may cause state-space explosion.
- Dynamic environments require reformulation.
- Incomplete information may lead to uncertainty.

---

## Comparison: problem formulation vs goal formulation

| Goal Formulation | Problem Formulation |
| --- | --- |
| Decides what to achieve | Decides how to represent the problem |
| Defines objective | Defines states, actions, goals, and costs |
| High-level decision | Formal representation |
| Example: Reach Delhi | Define cities, roads, distances, and actions |

---

## Important definitions

### Problem formulation

Representing a problem in terms of states, actions, transitions, goals, and costs.

### Initial state

The starting state of the search.

### Goal state

The desired final state.

### Transition model

A function describing the result of an action.

### Path cost

The total cost of reaching the goal.

---

## Practice Questions

### 2-mark questions

- Define problem formulation.
- What is a state space?
- What is a transition model?
- What is a goal test?
- Define path cost.

### 7-mark questions

- Explain the components of problem formulation.
- Describe the route-finding problem formulation.
- Explain state-space representation.

### 14-mark questions

- Explain problem formulation in AI with suitable examples.
- Discuss the components of a search problem in detail.
- Explain the formulation of the 8-puzzle problem.

---

## Conclusion

**Problem formulation** is a fundamental step in Artificial Intelligence that transforms a real-world task into a structured search problem. By defining the **initial state, state space, actions, transition model, goal test, and path cost**, it provides the framework required by search algorithms to solve problems efficiently. A well-formulated problem significantly reduces search complexity and improves the quality of solutions. Therefore, problem formulation serves as the foundation for **uninformed search, informed search, heuristic search, planning, and optimization techniques** in Artificial Intelligence.
