# Goal-Based Agents

## Introduction

A **Goal-Based Agent** is an intelligent agent that selects actions based on the achievement of specific goals. Unlike a simple reflex agent that responds directly to percepts, a goal-based agent considers the **future consequences of its actions** before making a decision.

The agent uses information about the current state of the environment and the desired goal state to determine the sequence of actions that will achieve the objective. This approach enables the agent to perform **planning, reasoning, and problem-solving**.

Goal-based agents are an important category of intelligent agents because they exhibit **purpose-oriented behavior** and can choose among multiple possible actions by evaluating which action leads closer to the goal.

## Definition

A **Goal-Based Agent** is an intelligent agent that chooses actions by considering their ability to achieve a specified goal, often using search and planning techniques.

## Characteristics of Goal-Based Agents

Goal-based agents possess the following characteristics:

- **Goal-oriented behavior**
- **Planning capability**
- **Evaluation of future states**
- **Decision-making based on outcomes**
- **Flexibility in action selection**
- **Ability to solve complex problems**

Unlike reflex agents, goal-based agents do not simply react to the current percept; they reason about **how actions affect future states**.

## Basic Architecture of a Goal-Based Agent

A goal-based agent maintains knowledge of the environment and uses goals to guide action selection.

```text
          Environment
               |
               | Percepts
               v
        +---------------+
        |    Sensors    |
        +---------------+
               |
               v
        +---------------+
        | State Update  |
        +---------------+
               |
               v
      +------------------+
      | Goal Information |
      +------------------+
               |
               v
      +------------------+
      | Search / Planning|
      +------------------+
               |
               v
      +------------------+
      | Action Selection |
      +------------------+
               |
               v
           Actuators
               |
               v
          Environment
```

The agent receives percepts, updates its internal state, considers the goal, plans a sequence of actions, and executes the chosen action.

## Components of a Goal-Based Agent

### Sensors

Sensors receive percepts from the environment.

Examples:

- location,
- obstacles,
- available resources,
- current conditions.

### Internal State

The agent maintains an internal representation of the environment.

The internal state stores:

- current location,
- known environment information,
- previous observations,
- available actions.

### Goal

A **goal** specifies the desired state that the agent wants to achieve.

Examples:

- reach a destination,
- collect an object,
- solve a puzzle,
- exit a maze.

### Search and Planning Module

This module determines the sequence of actions that transforms the current state into the goal state.

Common techniques include:

- Breadth-First Search (BFS),
- Depth-First Search (DFS),
- Uniform Cost Search,
- A* Search,
- heuristic search methods.

### Action Selection

The agent chooses the action that contributes most effectively toward achieving the goal.

## Working of a Goal-Based Agent

The operation of a goal-based agent follows a systematic process.

### Step 1: Perceive the Environment

The agent receives percepts.

Example:

```text
Current location = Room A
```

### Step 2: Update Internal State

The agent updates its knowledge.

```text
State = Room A
Door B is open
Door C is blocked
```

### Step 3: Identify the Goal

Example:

```text
Goal = Reach Room D
```

### Step 4: Search for a Plan

The agent evaluates possible action sequences.

Example:

```text
A → B → D
```

### Step 5: Select the Best Action

The first action of the chosen plan is executed.

Example:

```text
Move to Room B
```

### Step 6: Repeat

After execution, the environment is perceived again and the process continues until the goal is achieved.

## State Space Representation

Goal-based agents often represent problems using a **state space**.

A state space consists of:

- initial state,
- goal state,
- available actions,
- transition model.

Example:

```text
A ---- B ---- D
 \     |
  \    |
    C
```

Initial state:

```text
A
```

Goal state:

```text
D
```

Possible paths:

```text
A -> B -> D
A -> C -> B -> D
```

The agent searches for the most appropriate path.

## Goal Formulation

A goal must be clearly specified.

A good goal is:

- **well-defined,**
- **achievable,**
- **measurable,**
- **consistent.**

Example:

```text
Goal: Reach square (4,4)
```

Poor goal:

```text
Move somewhere useful
```

Precise goals enable efficient planning.

## Problem Formulation

To achieve a goal, the agent formulates the problem.

A problem consists of:

| Component | Description |
| --- | --- |
| Initial State | Current situation |
| Actions | Available operations |
| Transition Model | Result of each action |
| Goal Test | Checks whether the goal is reached |
| Path Cost | Cost of actions |

Example:

| Component | Example |
| --- | --- |
| Initial State | (1,1) |
| Goal State | (4,4) |
| Actions | Up, Down, Left, Right |
| Path Cost | 1 per move |

## Goal-Based Agent in Wumpus World

The Wumpus World agent can be designed as a goal-based agent.

### Goal

```text
Collect the gold and return safely.
```

### Planning

The agent:

- identifies safe squares,
- searches for a safe path,
- collects gold,
- plans a return path.

Example:

```text
(1,1) -> (2,1) -> (2,2) -> Gold
```

The agent chooses actions that move it closer to the goal while avoiding hazards.

## Example: Maze Solving Agent

Consider the maze.

```text
S - A - B
    |   |
    C - G
```

Where:

- **S** = Start
- **G** = Goal

The agent explores paths.

Possible paths:

```text
S -> A -> B -> G
S -> A -> C -> G
```

Using search algorithms, the agent selects an appropriate route.

## Difference Between Reflex Agent and Goal-Based Agent

| Feature | Reflex Agent | Goal-Based Agent |
| --- | --- | --- |
| Decision Basis | Current percept | Goal achievement |
| Planning | No | Yes |
| Future Consideration | No | Yes |
| Flexibility | Low | High |
| Problem Solving | Limited | Strong |
| Computational Cost | Low | Higher |

A goal-based agent is more intelligent because it evaluates the consequences of actions.

## Search in Goal-Based Agents

Search is the core mechanism of goal-based agents.

### Uninformed Search

Uses no additional knowledge.

Examples:

- BFS,
- DFS,
- Uniform Cost Search.

### Informed Search

Uses heuristics.

Examples:

- Greedy Best-First Search,
- A* Search.

Heuristics improve efficiency by estimating the distance to the goal.

## Advantages of Goal-Based Agents

- Flexible behavior.
- Intelligent decision-making.
- Can solve complex problems.
- Supports planning.
- Adapts to different goals.
- More rational than reflex agents.

## Limitations of Goal-Based Agents

- Computationally expensive.
- Search may be time-consuming.
- Requires an accurate environment model.
- Difficult in highly dynamic environments.
- Performance depends on the quality of planning algorithms.

## Applications of Goal-Based Agents

Goal-based agents are widely used in:

- robot navigation,
- autonomous vehicles,
- route planning,
- game playing,
- logistics optimization,
- intelligent assistants,
- industrial automation,
- search and rescue systems.

## Goal-Based Agent Algorithm

```text
Initialize State

Repeat

    Perceive Environment

    Update Internal State

    If Goal Achieved then
         Stop

    Formulate Goal

    Search for Action Sequence

    Select Best Action

    Execute Action

Until Goal Achieved
```

This algorithm emphasizes continuous planning and goal-directed action.

## Important Points

### Definition

A **Goal-Based Agent** is an intelligent agent that selects actions based on their ability to achieve a specified goal.

### Main Components

- Sensors
- Internal State
- Goal
- Search and Planning
- Action Selection
- Actuators

### Working Cycle

**Perception → State Update -> Goal Formulation -> Planning/Search -> Action Selection -> Execution**

### Key Feature

The agent evaluates **future consequences of actions** and chooses the action that moves it closer to the goal.

### Advantages

- Planning capability.
- Flexible decision-making.
- Problem-solving ability.
- Intelligent goal-directed behavior.

### Importance

Goal-based agents form the foundation of **AI planning, search algorithms, autonomous robotics, and intelligent decision-making systems**, making them one of the most important agent architectures in Artificial Intelligence.
