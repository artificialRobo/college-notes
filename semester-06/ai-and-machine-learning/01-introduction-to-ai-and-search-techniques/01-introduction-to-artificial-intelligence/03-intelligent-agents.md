# Intelligent Agents

## Introduction

An **Intelligent Agent (IA)** is an autonomous entity that perceives its environment through **sensors** and acts upon that environment through **actuators** to achieve specific goals. Intelligent agents are the fundamental building blocks of Artificial Intelligence because they provide a framework for designing systems that can make decisions and perform tasks intelligently.

The concept of intelligent agents is central to modern AI, where intelligence is viewed as **goal-directed behavior** rather than simply performing computations.

According to Stuart Russell and Peter Norvig:

>An agent is anything that can perceive its environment through sensors and act upon that environment through actuators.»

An intelligent agent selects actions that maximize the chances of achieving its objectives.

## Agent and environment

An intelligent agent operates within an **environment**. The agent continuously interacts with the environment through a perception–action cycle.

        Environment
             ▲
             │
      Actuators (Actions)
             │
             │
          Intelligent
             Agent
             │
             │
      Sensors (Percepts)
             ▼
        Environment

The agent receives information from the environment, processes it, and performs appropriate actions.

## Components of an intelligent agent

An intelligent agent consists of the following major components:

### Sensors

Sensors collect information from the environment.

Examples:

- Camera
- Microphone
- Keyboard
- Temperature sensor
- GPS receiver

The information received by sensors is called a **percept**.

### Actuators

Actuators allow the agent to perform actions.

Examples:

- Robot wheels
- Robotic arms
- Display screen
- Speaker
- Motor controls

### Agent function

The **agent function** maps the percept history to an action.

Mathematically,

Agent Function:

f : P* -> A

Where:

- P* = sequence of percepts
- A = set of actions

The agent function determines what action should be taken based on the entire percept history.

### Agent program

The **agent program** is the implementation of the agent function on a physical architecture.

- Agent function = abstract mapping.
- Agent program = actual software implementation.

## Characteristics of intelligent agents

An intelligent agent should possess the following properties:

### Autonomy

The agent operates without continuous human intervention.

### Rationality

The agent selects actions that maximize expected performance.

### Reactivity

The agent responds to changes in the environment.

### Proactiveness

The agent takes initiative rather than merely reacting.

### Learning ability

The agent improves performance through experience.

### Social ability

The agent communicates and cooperates with humans or other agents.

## Rational agent

A **rational agent** performs the right action, that is, the action expected to maximize its performance measure given the available percepts and knowledge.

A rational agent is not necessarily omniscient (all-knowing). It makes the **best possible decision based on available information**.

### Factors affecting rationality

Rationality depends on:

- Performance measure.
- Prior knowledge.
- Available actions.
- Percept sequence.

## Performance measure

A **performance measure** evaluates the success of an agent.

Examples:

| Agent | Performance measure|
| --- | --- |
| Vacuum cleaner | Percentage of clean rooms |
| Chess program | Number of games won |
| Self-driving car | Safety, travel time, fuel efficiency |
| Medical diagnosis system | Accuracy of diagnosis |

A well-designed performance measure encourages the desired behavior.

## Percepts and percept sequence

### Percept

A percept is the information received by the agent at a particular instant.

Example:

- Current room is dirty.
- Temperature = 30°C.
- Obstacle detected ahead.

### Percept sequence

The complete history of percepts received by the agent.

Example:

(Room A dirty, move right, Room B clean, move left)

Agents often make decisions based on the **entire percept sequence**, not just the current percept.

## Agent architecture

The **architecture** is the physical or computational platform on which the agent program runs.

Examples:

- Robot hardware.
- Computer system.
- Smartphone.
- Autonomous vehicle.
- Embedded controller.

The relationship can be expressed as:

**Agent = Architecture + Agent Program**

## Examples of intelligent agents

### Vacuum cleaning robot

Sensors:

- Dirt detector.
- Position sensor.

Actuators:

- Wheels.
- Vacuum motor.

Goal:

- Clean all accessible areas efficiently.

### Autonomous car

Sensors:

- Cameras.
- LiDAR.
- Radar.
- GPS.

Actuators:

- Steering.
- Brakes.
- Accelerator.

Goal:

- Reach destination safely and efficiently.

### Medical diagnosis agent

Sensors:

- Patient symptoms.
- Laboratory results.
- Medical history.

Actuators:

- Diagnostic recommendations.
- Treatment suggestions.

Goal:

- Maximize diagnostic accuracy.

### Chess-playing agent

Sensors:

- Current board configuration.

Actuators:

- Chess move.

Goal:

- Win the game.

## Intelligent agents versus ordinary programs

| Ordinary program | Intelligent agent |
| --- | --- |
| Executes predefined instructions | Makes decisions based on percepts |
| Limited adaptability | Can adapt to changing environments |
| No learning | May learn from experience |
| Fixed behavior | Goal-directed behavior |
| Minimal interaction | Continuous interaction with environment |

## PEAS representation

A common method for describing intelligent agents is **PEAS**.

PEAS stands for:

- **P** – Performance measure
- **E** – Environment
- **A** – Actuators
- **S** – Sensors

### Example: autonomous taxi

| Component | Description |
| --- | --- |
| Performance measure| Safe, fast, economical travel |
| Environment| Roads, traffic, pedestrians |
| Actuators| Steering, accelerator, brakes |
| Sensors| Cameras, GPS, radar, LiDAR |

PEAS helps define the requirements of an intelligent agent systematically.

## Learning in intelligent agents

Many intelligent agents improve through learning.

A learning agent generally contains:

- **Performance element** – selects actions.
- **Learning element** – improves performance.
- **Critic** – evaluates performance.
- **Problem generator** – suggests exploratory actions.

```
Environment
      │
      ▼
Performance Element
      │
      ▼
   Actions
      │
      ▼
Environment

Learning Element
      ▲
      │
    Critic
```

The learning element modifies the performance element based on feedback.

## Importance of intelligent agents in AI

Intelligent agents provide a unified framework for AI because they:

- Integrate perception, reasoning, and action.
- Support decision-making under uncertainty.
- Form the basis of robotics and autonomous systems.
- Enable learning and adaptation.
- Provide the foundation for search algorithms studied later in the course.

Most modern AI systems, including recommendation systems, virtual assistants, autonomous robots, and self-driving cars, can be viewed as intelligent agents.

## Key Points

**Agent**: An entity that perceives its environment through sensors and acts upon it through actuators.

**Intelligent agent**: An agent that acts rationally to achieve specified goals.

**Rational agent**: An agent that selects actions maximizing expected performance based on available percepts.

**Percept**: Information received by an agent from the environment.

**Performance measure**: A criterion used to evaluate the success of an agent.

## Conclusion

Intelligent agents are the core entities in Artificial Intelligence. They perceive the environment, process percepts, and perform actions that maximize goal achievement. The concepts of **rationality, percepts, performance measures, PEAS representation, and agent architecture** form the theoretical foundation for designing AI systems. Understanding intelligent agents is essential because search algorithms, problem-solving methods, and decision-making techniques in AI are all developed from the rational agent perspective.
