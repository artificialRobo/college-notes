# Knowledge-Based Agents

## Introduction

A **Knowledge-Based Agent (KBA)** is an intelligent agent that uses **stored knowledge about the world** to make decisions and perform actions. Unlike simple reflex agents that respond only to current percepts, a knowledge-based agent **reasons, infers new information, and chooses actions based on knowledge**.

Knowledge-based agents are a fundamental concept in Artificial Intelligence because they can solve problems in **complex and partially observable environments**.

## Definition

A **Knowledge-Based Agent** is an AI agent that maintains a **knowledge base**, updates it with percepts from the environment, uses an **inference mechanism** to derive conclusions, and selects actions based on logical reasoning.

## Basic Idea

A knowledge-based agent performs reasoning using two primary operations:

- **TELL**: Adds new information (percepts) to the knowledge base.
- **ASK**: Queries the knowledge base to determine what action should be taken.

The agent continuously updates its knowledge and uses logical reasoning to improve decision-making.

## Architecture of a Knowledge-Based Agent

```text
          Environment
                |
             Sensors
                |
                v
     +---------------------+
     | Knowledge-Based     |
     | Agent               |
     |                     |
     | Knowledge Base      |
     | Inference Engine    |
     | Decision Module     |
     +---------------------+
                |
             Actuators
                |
                v
          Environment
```

### Explanation

The agent:

1. Receives percepts through sensors.
2. Updates the knowledge base.
3. Performs reasoning using the inference engine.
4. Selects the best action.
5. Executes the action through actuators.

## Components of a Knowledge-Based Agent

### 1. Knowledge Base (KB)

The **knowledge base** stores information about the environment.

It contains:

- facts,
- rules,
- relationships,
- previous observations.

#### Example

- `Rain`
- `Rain → WetRoad`

The knowledge base is updated whenever the agent receives new percepts.

### 2. Inference Engine

The **inference engine** derives new information from existing knowledge.

Common reasoning techniques include:

- Modus Ponens,
- Resolution,
- Forward Chaining,
- Backward Chaining.

#### Example

Knowledge:

- `Rain`
- `Rain → WetRoad`

Inference:

- `WetRoad`

## 3. Percepts

A **percept** is an observation received from the environment.

Examples:

- There is a breeze.
- The temperature is 30°C.
- A wall is detected.

Percepts are added to the knowledge base using the **TELL** operation.

### 4. Actions

After reasoning, the agent selects an action.

Examples:

- move forward,
- turn left,
- pick up an object,
- stop,
- open a door.

## Working of a Knowledge-Based Agent

The agent operates in a continuous perception-reasoning-action cycle.

### Step-by-Step Process

1. Receive a percept from the environment.
2. Add the percept to the knowledge base (**TELL**).
3. Update internal knowledge.
4. Query the knowledge base (**ASK**).
5. Use inference to determine the best action.
6. Execute the action.
7. Repeat the process.

### Algorithm

```text
Initialize KB

Loop:
    percept = GetPercept()
    TELL(KB, percept)
    action = ASK(KB)
    Execute(action)
```

## TELL and ASK Operations

### TELL

The **TELL** operation inserts new information into the knowledge base.

#### Example

Percept:

```text
Breeze at (2,1)
```

Operation:

```text
TELL(KB, Breeze(2,1))
```

### ASK

The **ASK** operation retrieves information or determines actions.

#### Example

```text
ASK(KB, Safe(2,2))
```

The inference engine checks whether square `(2,2)` can be proven safe.

## Example: Room-Cleaning Knowledge-Based Agent

Consider a cleaning robot.

### Knowledge Base

Rules:

- `Dirty(RoomA) → Clean(RoomA)`
- `Obstacle(RoomA) → Avoid(RoomA)`

### Percepts

- `Dirty(RoomA)`
- `NoObstacle(RoomA)`

### Reasoning

The agent concludes that **RoomA should be cleaned**.

### Action

```text
Vacuum(RoomA)
```

This demonstrates reasoning beyond simple stimulus-response behavior.

## Knowledge Representation

Knowledge can be represented in different forms.

| Representation | Example |
| --- | --- |
| Propositional Logic | `P → Q` |
| First-Order Logic | `Human(x) → Mortal(x)` |
| Semantic Networks | Graph-based relationships |
| Production Rules | IF condition THEN action |
| Frames | Structured object representation |

In this unit, the primary focus is on **Propositional Logic** and **First-Order Logic**.

## Advantages of Knowledge-Based Agents

### 1. Better Decision Making

Uses logical reasoning rather than simple reactions.

### 2. Handles Incomplete Information

Can infer hidden facts from available evidence.

### 3. Easy to Update

New knowledge can be added without redesigning the entire system.

### 4. Explainable Reasoning

The reasoning process can be logically traced.

### 5. Flexible Behavior

The same inference engine can operate in different environments.

## Limitations of Knowledge-Based Agents

### 1. Knowledge Acquisition Problem

Creating a complete knowledge base is difficult and time-consuming.

### 2. Computational Complexity

Logical inference may become expensive for large knowledge bases.

### 3. Incomplete Knowledge

Missing or incorrect knowledge can lead to poor decisions.

### 4. Dynamic Environments

Rapidly changing environments require continuous updates.

## Comparison with Simple Reflex Agents

| Simple Reflex Agent | Knowledge-Based Agent |
| --- | --- |
| Uses current percept only | Uses stored knowledge |
| No reasoning | Performs logical inference |
| Limited flexibility | Highly flexible |
| Suitable for simple environments | Suitable for complex environments |
| No memory | Maintains a knowledge base |

## Real-World Applications

Knowledge-based agents are widely used in AI systems.

### Expert Systems

Medical diagnosis and advisory systems.

### Intelligent Tutoring Systems

Personalized education and learning assistance.

### Robotics

Navigation, planning, and autonomous decision-making.

### Automated Reasoning

Theorem proving and logical verification.

### Virtual Assistants

Question answering and intelligent decision support.

### Industrial Automation

Fault diagnosis and process control.

## Key Characteristics

A knowledge-based agent should possess:

- **Knowledge representation**
- **Logical reasoning ability**
- **Learning and updating capability**
- **Goal-directed behavior**
- **Decision-making under uncertainty**

## Important Points

### Definition

A **Knowledge-Based Agent** uses a **knowledge base** and an **inference engine** to determine actions.

### Main Operations

- **TELL**
- **ASK**

### Main Components

- Knowledge Base
- Inference Engine
- Sensors
- Actuators

### Advantages

- Reasoning capability
- Flexibility
- Explainability

### Limitations

- Knowledge acquisition problem
- Computational cost
- Incomplete knowledge
