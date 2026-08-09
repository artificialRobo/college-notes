# Agent Design for Wumpus World

## Introduction

The **Agent Design for Wumpus World** describes how a knowledge-based intelligent agent perceives the environment, stores knowledge, performs logical reasoning, and selects actions to achieve its goal safely.

A Wumpus World agent is a **knowledge-based rational agent** because it makes decisions based on the knowledge stored in its **Knowledge Base (KB)** rather than acting only on immediate percepts.

The agent continuously updates its knowledge using percepts from the environment and applies **logical inference** to determine safe and unsafe locations.

## Definition

A **Wumpus World agent** is a knowledge-based rational agent that uses percepts, logical inference, and a knowledge base to navigate the environment, locate the gold, avoid hazards, and exit safely.

## Objectives of the Agent

The primary objectives of the Wumpus World agent are:

- **Find and collect the gold.**
- **Avoid pits.**
- **Avoid the Wumpus.**
- **Use the arrow effectively if necessary.**
- **Return safely to the starting square.**
- **Maximize the performance measure (score).**

## Architecture of a Wumpus World Agent

The Wumpus World agent follows the **Knowledge-Based Agent Architecture**.

```text
             Environment
                  |
                  | Percepts
                  v
         +-------------------+
         |      Sensors      |
         +-------------------+
                  |
                  v
         +-------------------+
         |   Knowledge Base  |
         +-------------------+
                  |
                  v
         +-------------------+
         | Inference Engine  |
         +-------------------+
                  |
                  v
         +-------------------+
         | Action Selection  |
         +-------------------+
                  |
                  v
             Actuators
                  |
                  v
             Environment
```

The agent receives percepts through sensors, updates the knowledge base, performs inference, selects an action, and executes it through actuators.

## Components of the Agent

### Sensors

Sensors receive percepts from the environment.

The percept sequence consists of:

- Stench
- Breeze
- Glitter
- Bump
- Scream

Example:

```text
(Stench, Breeze, Glitter, Bump, Scream)
```

A typical percept may be:

```text
(False, True, False, False, False)
```

This means:

- No stench
- Breeze present
- No glitter
- No bump
- No scream

### Knowledge Base (KB)

The **Knowledge Base** stores:

- facts,
- percepts,
- logical rules,
- inferred knowledge,
- visited locations,
- safe locations,
- possible hazard locations.

Example facts:

```text
Safe(1,1)
Visited(1,1)
Breeze(2,1)
```

The KB grows continuously as the agent explores the world.

### Inference Engine

The inference engine derives new knowledge from existing facts.

For example, if the agent knows:

```text
¬Breeze(1,1)
```

then it can infer:

```text
¬Pit(1,2)
¬Pit(2,1)
```

Similarly,

```text
Stench(2,2)
```

may imply that the Wumpus is in an adjacent square.

The inference engine typically uses:

- propositional logic,
- resolution,
- forward chaining,
- backward chaining,
- logical entailment.

### Action Selection Module

Based on inferred knowledge, the agent chooses the best action.

Possible actions include:

- Move Forward
- Turn Left
- Turn Right
- Grab
- Shoot
- Climb

The selected action should maximize expected utility and minimize risk.

## Internal State of the Agent

A Wumpus World agent maintains an internal model of the environment.

It stores information such as:

| Information | Purpose |
| --- | --- |
| Current location | Navigation |
| Current orientation | Movement planning |
| Visited squares | Avoid repeated exploration |
| Safe squares | Future movement |
| Possible pits | Hazard avoidance |
| Possible Wumpus location | Threat assessment |
| Arrow availability | Attack planning |
| Gold possession | Goal tracking |

Example:

```text
Location = (2,1)
Facing = East
Arrow = Available
Gold = Not Collected
Safe Squares = {(1,1), (2,1), (1,2)}
```

## Working of the Wumpus World Agent

The agent repeatedly performs the following cycle.

### Step 1: Receive Percept

Example:

```text
Breeze = True
Stench = False
```

### Step 2: Update Knowledge Base

The percept is added to the KB.

```text
Breeze(2,1)
```

### Step 3: Perform Inference

Using logical rules:

```text
Breeze(x,y)
```

implies

```text
Pit in an adjacent square
```

Possible pit locations are identified.

### Step 4: Identify Safe Squares

Squares that cannot contain pits or the Wumpus are marked safe.

Example:

```text
Safe(1,2)
```

### Step 5: Select an Action

The agent chooses a safe action.

Example:

```text
Move to (1,2)
```

### Step 6: Execute Action

The action is performed and a new percept is received.

This cycle continues until:

- gold is collected,
- the agent exits,
- or the agent dies.

## Knowledge Representation in Agent Design

The agent represents knowledge symbolically.

### Pit Representation

```text
P(x,y)
```

means a pit exists at square (x,y).

### Wumpus Representation

```text
W(x,y)
```

means the Wumpus exists at square (x,y).

### Breeze Rule

For square (x,y):

```text
B(x,y) ↔ Pit in an adjacent square
```

Example:

```text
B(2,2) ↔ P(1,2) ∨ P(3,2) ∨ P(2,1) ∨ P(2,3)
```

### Stench Rule

```text
S(x,y) ↔ Wumpus in an adjacent square
```

These rules allow systematic reasoning.

## Example of Agent Reasoning

Assume the following sequence.

### Initial State

Location:

```text
(1,1)
```

Percepts:

- No breeze
- No stench

Inference:

```text
Safe(1,2)
Safe(2,1)
```

### Move to (2,1)

Percept:

```text
Breeze
```

Inference:

Possible pit locations:

```text
(2,2)
(3,1)
```

### Move to (1,2)

Percept:

```text
No Breeze
```

Inference:

```text
No pit at (2,2)
```

Therefore,

```text
Pit(3,1)
```

The agent has successfully identified the pit location using logical reasoning.

## Decision-Making Strategy

The Wumpus World agent follows a **rational decision-making strategy**.

### Prefer Safe Squares

Always move to squares known to be safe.

### Avoid Known Hazards

Do not enter squares containing:

- confirmed pits,
- confirmed Wumpus.

### Handle Uncertainty

When no safe squares are available:

- choose the least risky square,
- or backtrack.

### Use Arrow Wisely

Shoot only when the Wumpus location is strongly inferred.

### Return After Collecting Gold

After grabbing the gold, plan a safe path back to (1,1).

## Algorithm of a Knowledge-Based Wumpus Agent

```text
Initialize Knowledge Base

Repeat

    Receive percept

    Add percept to KB

    Apply inference rules

    Mark safe squares

    Identify hazards

    If Glitter then
         Grab Gold

    Else if safe square exists then
         Move to safe square

    Else if Wumpus location known and arrow available then
         Shoot

    Else
         Backtrack

Until agent exits or dies
```

This algorithm represents the basic design of the Wumpus World agent.

## Agent Design Challenges

Designing an effective Wumpus agent involves several challenges.

### Partial Observability

The agent cannot directly observe hazards.

### Uncertainty

Percepts provide only indirect information.

### Efficient Inference

The agent must reason quickly.

### Exploration vs Safety

Exploring unknown areas may be dangerous.

### Planning

The agent must find a safe route to the gold and back.

## Advantages of the Knowledge-Based Design

- Handles incomplete information.
- Performs logical reasoning.
- Makes rational decisions.
- Avoids unnecessary risks.
- Explains its decisions logically.
- Suitable for symbolic AI systems.

## Limitations

- Requires accurate logical rules.
- Inference can become computationally expensive.
- Does not learn automatically from experience.
- Performance depends on the quality of the knowledge base.
- Difficult to scale to large uncertain environments.

## Applications of Wumpus Agent Design

The design principles are useful in:

- autonomous robot navigation,
- intelligent exploration systems,
- expert systems,
- game AI,
- decision support systems,
- diagnostic reasoning systems,
- logical planning systems.

## Summary

### Definition

A **Wumpus World agent** is a knowledge-based rational agent that uses percepts, a knowledge base, and logical inference to safely navigate the environment and achieve its goal.

### Main Components

- Sensors
- Knowledge Base
- Inference Engine
- Action Selection
- Actuators

### Working Cycle

**Percept -> Knowledge Base Update -> Inference -> Safe Action Selection -> Execute Action**

### Decision Strategy

- Move to safe squares.
- Avoid hazards.
- Infer pit and Wumpus locations.
- Grab gold when glitter is perceived.
- Return safely to the start.

### Importance

The **Agent Design for Wumpus World** demonstrates the complete working of a **knowledge-based intelligent agent**, integrating **knowledge representation, logical reasoning, inference, planning, and rational decision-making**, making it one of the most important models for understanding symbolic AI and intelligent agent architecture.
