# Introduction to Inference

## Definition of Inference

Inference is the process of **deriving new knowledge or conclusions from existing knowledge** stored in a knowledge base. In Artificial Intelligence, inference enables a system to reason about known facts and apply logical rules to solve problems, answer questions, or make decisions.

A knowledge-based system becomes useful only when it can infer information that is **not explicitly stored** in the knowledge base.

> **Inference is the logical process of obtaining new facts from known facts using inference rules.**

## Need for Inference in AI

Knowledge representation stores information, but AI systems must also **reason with that information**. Inference provides the reasoning capability that allows intelligent behavior.

Inference is required to:

- Derive implicit knowledge.
- Solve logical problems.
- Make predictions.
- Support decision-making.
- Provide explanations.
- Build expert systems.

### Example

If the knowledge base contains:

- All humans are mortal.
- Socrates is a human.

The inference mechanism concludes:

- Socrates is mortal.

This conclusion is inferred even though it was not directly stored.

## Components of an Inference System

An inference system consists of the following components:

| Component | Function |
| --- | --- |
| **Knowledge Base** | Stores facts and rules |
| **Inference Engine** | Applies logical reasoning |
| **Working Memory** | Stores current facts |
| **Control Strategy** | Determines which rule to apply |

The **inference engine** is the central reasoning component that examines available facts and applies appropriate rules.

## Knowledge Base and Inference Engine

### Knowledge Base

The knowledge base contains:

- **Facts** (known information)
- **Rules** (relationships between facts)

#### Example

Facts:

- Fever
- Cough

Rule:

- IF fever AND cough THEN flu

### Inference Engine

The inference engine performs the reasoning process by:

1. Matching facts with rule conditions.
2. Selecting applicable rules.
3. Executing the rules.
4. Adding newly derived facts to the knowledge base.

## How Inference Works

The inference process generally follows these steps:

1. **Input facts** are stored in working memory.
2. The inference engine searches for rules whose conditions are satisfied.
3. Matching rules are fired.
4. New facts are generated.
5. The process continues until the goal is reached or no more rules can be applied.

### Example

Knowledge base:

- **R1:** IF A THEN B
- **R2:** IF B THEN C

Initial fact:

- A

Inference process:

A -> B -> C

Final inferred fact:

- C

Thus, inference can derive multiple conclusions through chained reasoning.

## Types of Inference

Inference in AI can be classified into several types.

### 1. Deductive Inference

Derives logically certain conclusions from general rules.

#### Example

- All birds have wings.
- A sparrow is a bird.

**Conclusion:** A sparrow has wings.

This is the most common type used in rule-based AI systems.

### 2. Inductive Inference

Derives general rules from specific observations.

#### Example

- Swan 1 is white.
- Swan 2 is white.
- Swan 3 is white.

**Possible conclusion:** All swans are white.

The conclusion is probable but not guaranteed.

### 3. Abductive Inference

Finds the most likely explanation for observed facts.

#### Example

Observation:

- The grass is wet.

Possible explanation:

- It rained.

Abductive reasoning is widely used in diagnosis and fault detection.

## Inference Rules

Inference rules are logical rules that specify how new knowledge can be derived.

A general production rule is:

**IF condition THEN conclusion**

### Example

IF temperature > 38°C THEN fever

Inference rules form the basis of **production-based expert systems**.

## Rule Application Process

The inference engine repeatedly performs:

### Pattern Matching

Identify rules whose conditions match current facts.

### Rule Selection

Choose one rule when multiple rules are applicable.

### Rule Firing

Execute the selected rule and generate new facts.

This process is known as the **recognize–act cycle**.

## Recognize–Act Cycle

The recognize–act cycle consists of three phases.

### Recognize

Match facts with rule conditions.

### Resolve

Select one rule among competing rules.

### Act

Execute the selected rule and update working memory.

#### Example

Facts:

- Rain
- Cold

Rules:

- **R1:** IF rain THEN wet road
- **R2:** IF cold THEN wear jacket

The system recognizes both rules, resolves any conflict, and executes the selected rule(s).

## Conflict Resolution

When multiple rules can fire simultaneously, the inference engine must choose one.

Common conflict resolution strategies:

- **Rule priority** – higher priority rules execute first.
- **Specificity** – more specific rules are preferred.
- **Recency** – rules using recently added facts are preferred.
- **First applicable rule** – the first matching rule is selected.

Conflict resolution improves efficiency and consistency.

## Inference in Expert Systems

Expert systems use inference to simulate human expert reasoning.

The inference engine:

- Asks questions.
- Collects facts.
- Applies rules.
- Reaches conclusions.
- Provides recommendations.

### Example

Medical expert system

Rules:

- IF fever AND cough THEN influenza
- IF influenza THEN prescribe antiviral medicine

The inference engine derives the diagnosis and treatment recommendation.

## Advantages of Inference Mechanisms

- Derives hidden knowledge.
- Automates reasoning.
- Supports intelligent decision-making.
- Improves consistency.
- Enables expert system development.
- Reduces manual analysis.

## Limitations of Inference

- Depends on the quality of the knowledge base.
- May become slow with large rule sets.
- Conflict resolution can be complex.
- Uncertain or incomplete knowledge may affect conclusions.
- Maintaining large rule bases is difficult.

## Applications of Inference

Inference mechanisms are used in:

- Medical diagnosis.
- Fault detection.
- Legal reasoning.
- Financial decision systems.
- Recommendation systems.
- Intelligent tutoring systems.
- Robotics.
- Industrial expert systems.

## Comparison of Reasoning Types

| Reasoning Type | Nature of Conclusion |
| --- | --- |
| **Deductive** | Certain |
| **Inductive** | Probable |
| **Abductive** | Most likely explanation |

## Summary

**Inference** is the reasoning process used by an AI system to derive new facts from existing knowledge. It is performed by the **inference engine**, which applies logical rules stored in the knowledge base. The inference process involves matching facts with rule conditions, selecting applicable rules, firing the rules, and generating new conclusions. Common types of reasoning include **deductive, inductive, and abductive inference**. Inference mechanisms are widely used in expert systems, diagnosis systems, and intelligent decision-support applications.
