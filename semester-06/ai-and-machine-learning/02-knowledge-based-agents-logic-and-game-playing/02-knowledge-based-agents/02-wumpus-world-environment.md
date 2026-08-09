# Wumpus World Environment

## Introduction

The **Wumpus World** is a classical artificial intelligence (AI) problem introduced by **Stuart Russell and Peter Norvig** to explain the concepts of **knowledge-based agents, logical reasoning, inference, and decision-making under uncertainty**.

It is a **grid-based environment** in which an intelligent agent must explore a cave, collect a piece of gold, avoid dangerous pits and the Wumpus monster, and safely exit the environment.

The Wumpus World is widely used in AI because it provides a simple but powerful framework for understanding **knowledge representation, propositional logic, and intelligent agent design**.

## Definition 
The **Wumpus World** is a partially observable, deterministic, sequential, static, and discrete environment in which an intelligent agent uses logical reasoning to locate gold while avoiding pits and the Wumpus.

## Structure of the Wumpus World

The environment is usually represented as a **4 × 4 grid** of rooms or squares.

```
+----+----+----+----+
|    | P  |    | G  |
+----+----+----+----+
| W  |    | P  |    |
+----+----+----+----+
|    |    |    |    |
+----+----+----+----+
| A  |    |    |    |
+----+----+----+----+
```

Where:

- **A** = Agent
- **W** = Wumpus
- **P** = Pit
- **G** = Gold

The agent initially knows only its starting location and must infer the locations of hazards through percepts.

## Components of the Environment

| Component | Description |
| --- | --- |
| Agent | Starts at square (1,1) |
| Wumpus | A dangerous monster that kills the agent |
| Pit | A bottomless pit causing death |
| Gold | The goal object to be collected |
| Walls | Boundaries of the cave |

## Properties of the Wumpus World Environment

The Wumpus World is classified according to the standard AI environment properties.

| Property | Nature |
| --- | --- |
| Observability | Partially observable |
| Determinism | Deterministic |
| Episodic/Sequential | Sequential |
| Static/Dynamic | Static |
| Discrete/Continuous | Discrete |
| Number of agents | Single-agent |

### Explanation of Properties

### Partially Observable

The agent cannot directly observe the entire environment. It receives only local percepts from its current square.

### Deterministic

Every action has a predictable result.

### Sequential

Current decisions affect future states and outcomes.

### Static

The environment does not change while the agent is reasoning.

### Discrete

The environment consists of distinct grid cells and discrete actions.

### Single-Agent

Only one intelligent agent operates in the environment.

## Percepts in the Wumpus World

A **percept** is information received by the agent from the environment.

The agent receives **five possible percepts**.

| Percept | Meaning |
| --- | --- |
| **Stench** | Wumpus is in an adjacent square |
| **Breeze** | Pit is in an adjacent square |
| **Glitter** | Gold is in the current square |
| **Bump** | Agent has hit a wall |
| **Scream** | Wumpus has been killed |

Adjacent squares include only **up, down, left, and right** (not diagonal).

## Stench

If the Wumpus occupies a square, all adjacent squares contain a **stench**.

Example:

```
+---+---+---+
|   | S |   |
+---+---+---+
| S | W | S |
+---+---+---+
|   | S |   |
+---+---+---+
```

The stench helps the agent infer the possible location of the Wumpus.

## Breeze

If a pit exists in a square, all adjacent squares contain a **breeze**.

Example:

```
+---+---+---+
|   | B |   |
+---+---+---+
| B | P | B |
+---+---+---+
|   | B |   |
+---+---+---+
```

The breeze provides indirect information about nearby pits.

## Glitter

A square containing gold produces **glitter**.

When the agent perceives glitter, it can execute the **Grab** action to collect the gold.

## Bump

A bump occurs when the agent attempts to move into a wall.

This percept helps the agent determine the boundaries of the environment.

## Scream

If the agent shoots its arrow and kills the Wumpus, a **scream** is heard throughout the environment.

The scream indicates that the Wumpus is dead and no longer poses a threat.

## Rules of the Wumpus World

### Initial Conditions

- The agent starts at **(1,1)**.
- The starting square is always safe.
- The agent possesses **one arrow**.
- There is **one Wumpus**.
- There is **one piece of gold**.
- There may be multiple pits.

### Possible Actions

The agent can perform the following actions.

| Action | Description |
| --- | --- |
| Move Forward | Move one square ahead |
| Turn Left | Rotate left |
| Turn Right | Rotate right |
| Grab | Pick up the gold |
| Shoot | Fire the arrow |
| Climb | Exit the cave from the starting square |

## Performance Measure

The objective of the agent is to maximize its score.

A typical scoring system is:

| Event | Score |
| --- | --- |
| Obtain gold | +1000 |
| Fall into pit | -1000 |
| Killed by Wumpus | -1000 |
| Each action | -1 |
| Shoot arrow | -10 |

Therefore, the agent must:

- find the gold,
- avoid hazards,
- minimize unnecessary actions,
- exit safely.

## Knowledge Available to the Agent

The agent maintains a **Knowledge Base (KB)** containing facts and rules.

Initially, the KB includes:

- Agent is at (1,1)
- (1,1) is safe
- No pit at (1,1)
- No Wumpus at (1,1)

As percepts are received, new information is added to the KB.

## Logical Representation

The Wumpus World is commonly represented using **propositional logic**.

### Symbols

| Symbol | Meaning |
| --- | --- |
| P(x,y) | Pit at (x,y) |
| W(x,y) | Wumpus at (x,y) |
| B(x,y) | Breeze at (x,y) |
| S(x,y) | Stench at (x,y) |
| G(x,y) | Gold at (x,y) |

## Breeze Rule

A square has a breeze **if and only if** an adjacent square contains a pit.

For square (1,1):

```
B(1,1) ↔ P(1,2) ∨ P(2,1)
```

This means that a breeze at (1,1) implies a pit in one of the neighboring squares.

## Stench Rule

Similarly,

```
S(1,1) ↔ W(1,2) ∨ W(2,1)
```

A stench indicates that the Wumpus is in an adjacent square.

## Example of Logical Reasoning

Suppose the agent starts at **(1,1)**.

### Percepts

- No Breeze
- No Stench

### Inference

```
¬B(1,1) → ¬P(1,2) ∧ ¬P(2,1)
```

Therefore,

- (1,2) is safe.
- (2,1) is safe.

The agent can safely move to either square.

Suppose the agent moves to (2,1).

### New Percept

- Breeze

The pit must be in one of the adjacent squares.

Possible pit locations:

- (2,2)
- (3,1)

By combining information from multiple locations, the agent can eventually determine the exact pit location.

This process is called **logical inference**.

## Knowledge-Based Reasoning Process

The agent follows the cycle:

1. Receive percept.
2. Update knowledge base.
3. Apply logical inference.
4. Determine safe squares.
5. Select the next action.

Example:

```
Percept -> Knowledge Base -> Inference -> Safe Action
```

This makes the Wumpus World an excellent example of a **knowledge-based agent**.

## Importance of the Wumpus World in AI

The Wumpus World demonstrates several fundamental AI concepts.

### Knowledge Representation

Information is represented symbolically.

### Logical Reasoning

The agent derives new facts from existing knowledge.

### Decision Making

Actions are selected based on inferred knowledge.

### Planning

The agent plans a safe route to obtain the gold.

### Intelligent Behavior

The agent acts rationally despite incomplete information.

## Advantages of the Wumpus World

- Simple and easy to understand.
- Demonstrates logical reasoning effectively.
- Supports propositional and first-order logic.
- Useful for teaching knowledge-based agents.
- Provides a foundation for intelligent planning systems.

## Limitations of the Wumpus World

- Small and simplified environment.
- Deterministic rather than uncertain.
- Hazards are stationary.
- Limited real-world complexity.
- Does not inherently include learning mechanisms.

## Applications

The concepts of the Wumpus World are applied in:

- autonomous robot navigation,
- intelligent exploration systems,
- expert systems,
- reasoning engines,
- game AI,
- search and rescue planning,
- knowledge-based decision support systems.

## Important Points

### Definition

The **Wumpus World Environment** is a partially observable grid-based environment in which an intelligent agent uses logical reasoning to locate gold and avoid pits and the Wumpus.

### Environment Characteristics

- Partially observable
- Deterministic
- Sequential
- Static
- Discrete
- Single-agent

### Main Percepts

- Stench
- Breeze
- Glitter
- Bump
- Scream

### Goal of the Agent

- Collect the gold.
- Avoid pits.
- Avoid the Wumpus.
- Exit the cave safely.

### AI Significance

The Wumpus World provides a fundamental model for **knowledge representation, propositional logic, logical inference, and knowledge-based agent design**, making it one of the most important educational environments in Artificial Intelligence.
