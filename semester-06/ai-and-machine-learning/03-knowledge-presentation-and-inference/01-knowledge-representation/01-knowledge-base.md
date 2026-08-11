# Knowledge Base

## Introduction

A **Knowledge Base (KB)** is a centralized repository that stores facts, rules, relationships, and information about a specific domain. In Artificial Intelligence (AI), a knowledge base enables a system to perform **reasoning, decision-making, problem-solving, and query answering** using stored knowledge.

A knowledge base is a fundamental component of **knowledge-based systems and expert systems**.

## Definition

A **Knowledge Base (KB)** is an organized collection of knowledge represented in a structured form that allows a computer system to process information and perform intelligent reasoning.

## Purpose of a Knowledge Base

The primary objective of a knowledge base is to store domain knowledge in a structured manner so that an AI system can:

- Solve problems
- Make decisions
- Draw logical conclusions
- Provide recommendations
- Answer queries
- Assist human experts

For example, a medical expert system stores information about diseases, symptoms, diagnostic rules, and treatments.

## Components of a Knowledge Base

A knowledge base generally consists of two major components:

| Component | Description |
| --- | --- |
| **Facts** | Known information about the domain |
| **Rules** | Logical relationships used for reasoning |

### Facts

Facts are statements that represent information known to be true.

**Examples:**

- Sky is blue.
- Water freezes at 0°C.
- Fever is a symptom of influenza.

### Rules

Rules describe how new knowledge can be inferred from existing facts.

**General form:**

```text
IF condition THEN conclusion
```

**Example:**

```text
IF fever AND cough THEN influenza
```

## Structure of a Knowledge Base

A knowledge base stores information in a structured format.

```text
Knowledge Base

Facts:
F1: Fever(Patient)
F2: Cough(Patient)

Rules:
R1: IF Fever AND Cough THEN Flu
R2: IF Flu THEN Recommend(Rest)
```

The **inference engine** uses these facts and rules to derive new conclusions.

## Representation of Knowledge in a Knowledge Base

Knowledge can be represented in several forms.

| Representation Technique | Example |
| --- | --- |
| Logical statements | Human(x) → Mortal(x) |
| Production rules | IF A THEN B |
| Frames | Object with attributes |
| Semantic networks | Graph of relationships |

In this unit, **production-based systems** and **frame-based systems** are particularly important.

## Working of a Knowledge Base

A knowledge base works together with an **inference engine**.

```text
Input Facts
     │
     v
Knowledge Base
(Facts + Rules)
     │
     v
Inference Engine
     │
     v
Derived Conclusion / Decision
```

The inference engine examines the stored facts and rules and derives new knowledge.

## Example of a Knowledge Base

Consider a simple medical diagnosis system.

### Facts

- Patient has fever.
- Patient has cough.

### Rules

```text
R1: IF fever AND cough THEN flu
R2: IF flu THEN prescribe rest
R3: IF flu THEN prescribe fluids
```

### Reasoning Process

Given facts:

```text
fever = true
cough = true
```

Applying **Rule R1**:

```text
flu = true
```

Applying **Rules R2 and R3**:

```text
prescribe rest
prescribe fluids
```

Thus, the system recommends appropriate treatment.

## Characteristics of a Good Knowledge Base

A well-designed knowledge base should possess the following properties:

### 1. Correctness

Knowledge should be accurate and reliable.

### 2. Completeness

It should contain sufficient knowledge to solve the intended problems.

### 3. Consistency

Rules should not contradict one another.

### 4. Efficiency

Knowledge retrieval and reasoning should be fast.

### 5. Modifiability

New facts and rules should be added easily.

### 6. Maintainability

The knowledge base should be easy to update and manage.

## Types of Knowledge Stored in a Knowledge Base

A knowledge base may contain different categories of knowledge.

| Type of Knowledge | Description |
| --- | --- |
| **Declarative knowledge** | Facts and information |
| **Procedural knowledge** | How to perform tasks |
| **Heuristic knowledge** | Rules of thumb |
| **Meta-knowledge** | Knowledge about knowledge |

### Examples

- **Declarative:** Delhi is the capital of India.
- **Procedural:** To diagnose flu, check fever and cough.
- **Heuristic:** Persistent high fever often indicates infection.

## Knowledge Base in Expert Systems

An **expert system** consists of the following components:

- Knowledge base
- Inference engine
- User interface
- Explanation module

```text
User
 │
 v
User Interface
 │
 v
Inference Engine
 │
 v
Knowledge Base
 │
 v
Domain Expert Knowledge
```

The knowledge base stores the expertise of human specialists.

## Advantages of a Knowledge Base

- Stores expert knowledge permanently
- Supports automated decision-making
- Produces consistent conclusions
- Reduces human effort
- Improves problem-solving efficiency
- Enables knowledge sharing
- Can be updated with new knowledge

## Limitations of a Knowledge Base

- Knowledge acquisition is difficult
- Requires continuous updating
- May become inconsistent if poorly designed
- Limited by the quality of stored knowledge
- Cannot reason beyond available knowledge without advanced learning mechanisms

## Applications of Knowledge Bases

Knowledge bases are widely used in AI applications.

- Medical diagnosis systems
- Customer support systems
- Recommendation systems
- Intelligent tutoring systems
- Legal advisory systems
- Industrial troubleshooting
- Financial decision support systems
- Robotics

## Difference Between Database and Knowledge Base

| Database | Knowledge Base |
| --- | --- |
| Stores raw data | Stores facts and rules |
| Supports data retrieval | Supports reasoning and inference |
| Uses queries | Uses logical inference |
| No intelligence | Enables intelligent decision-making |
| Example: Student records | Example: Medical expert system |

## Advantages Over Traditional Databases

A knowledge base not only stores information but also derives **new knowledge** through reasoning.

For example:

**Stored facts:**

```text
Fever
Cough
```

**Stored rule:**

```text
IF Fever AND Cough THEN Flu
```

**Derived conclusion:**

```text
Flu
```

A traditional database can retrieve stored facts, whereas a knowledge base can infer the diagnosis.

## Examination-Oriented Summary

### Definition

A **Knowledge Base (KB)** is a structured repository of facts and rules used by an AI system to perform reasoning, inference, and intelligent decision-making.

### Key Components

- Facts
- Rules

### Functions

- Store knowledge
- Support inference
- Solve problems
- Assist decision-making

### Major Applications

- Expert systems
- Medical diagnosis
- Recommendation systems
- Intelligent decision support

## Conclusion

A **knowledge base** is the foundation of intelligent AI systems. It organizes domain knowledge into facts and rules that can be processed by an **inference engine** to generate logical conclusions. Knowledge bases enable expert systems to emulate human expertise, provide consistent decisions, and solve complex problems efficiently. Understanding knowledge bases is essential before studying **knowledge representation techniques**, which define how knowledge is encoded and structured within AI systems.
