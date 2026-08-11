# Backward Chaining

## Definition of Backward Chaining

**Backward chaining** is a **goal-driven inference technique** in which reasoning starts with the **desired goal or conclusion** and works backward through the knowledge base to determine whether the goal can be proven using available facts and rules.

It is called **backward chaining** because the inference process moves **backward from the goal toward the supporting facts**.

> **Backward chaining is a goal-driven reasoning method that begins with a goal and works backward through inference rules to verify whether the goal can be satisfied by existing facts.**

## Basic Idea of Backward Chaining

In backward chaining, the inference engine first identifies the goal to be achieved. It then searches for rules that can produce that goal as a conclusion.

For each such rule, the engine attempts to prove the rule’s conditions. These conditions become **sub-goals**, and the process continues recursively until the sub-goals are matched with known facts or can no longer be proven.

The process stops when:

- The goal is successfully proven.
- The goal cannot be proven.
- No applicable rules remain.

## Goal-Driven Reasoning

Backward chaining is known as **goal-driven reasoning** because the reasoning process is initiated by a **specific objective** rather than by available data.

For example, if the goal is:

```text
Patient has flu
```

The system works backward to determine whether the symptoms required for flu are present.

## Working Principle of Backward Chaining

The backward chaining process consists of the following steps:

1. **Select the goal** to be proved.
2. **Search for rules** whose conclusion matches the goal.
3. **Identify the rule conditions**.
4. **Treat the conditions as sub-goals**.
5. **Verify each sub-goal** using known facts or additional rules.
6. **Conclude whether the goal is true or false**.

### General Rule Format

```text
IF condition(s) THEN conclusion
```

Example:

```text
IF fever AND cough THEN flu
```

Goal:

```text
flu
```

The engine checks whether `fever` and `cough` can be established.

## Backward Chaining Algorithm

The algorithm can be expressed as follows:

```text
1. Set the desired goal.
2. Check whether the goal is already a known fact.
3. If not, find rules that conclude the goal.
4. For each rule:
      a. Prove all conditions.
      b. If all conditions are true,
         conclude that the goal is true.
5. If no rule can prove the goal,
   conclude that the goal is false.
```

## Example of Backward Chaining

Consider the following knowledge base.

### Rules

```text
R1: IF A THEN B
R2: IF B THEN C
R3: IF C THEN D
```

### Known Fact

```text
A
```

### Goal

```text
D
```

### Inference Process

The engine works backward.

To prove `D`:

Use R3.

Need to prove:

```text
C
```

To prove `C`:

Use R2.

Need to prove:

```text
B
```

To prove `B`:

Use R1.

Need to prove:

```text
A
```

`A` is already known.

Therefore:

```text
A => B => C => D
```

Hence the goal `D` is successfully proven.

## Step-by-Step Example

### Knowledge Base

Rules:

```text
R1: IF rain THEN wet_ground
R2: IF wet_ground THEN slippery_road
R3: IF slippery_road THEN drive_carefully
```

Known fact:

```text
rain
```

### Goal

```text
drive_carefully
```

### Execution

**Step 1**

Goal:

```text
drive_carefully
```

Apply R3.

Need to prove:

```text
slippery_road
```

**Step 2**

Goal:

```text
slippery_road
```

Apply R2.

Need to prove:

```text
wet_ground
```

**Step 3**

Goal:

```text
wet_ground
```

Apply R1.

Need to prove:

```text
rain
```

**Step 4**

`rain` is a known fact.

Therefore:

```text
rain => wet_ground => slippery_road => drive_carefully
```

The goal is proven.

## Backward Chaining Search Tree

The reasoning process can be represented as a goal tree.

```text
      drive_carefully
              |
             R3
              |
      slippery_road
              |
             R2
              |
        wet_ground
              |
             R1
              |
            rain
```

The search proceeds **from the top (goal) downward toward known facts**.

## Recursive Nature of Backward Chaining

Backward chaining is naturally **recursive**.

A goal may generate several sub-goals, and each sub-goal may generate additional sub-goals.

Example:

```text
Goal: D
```

Requires:

```text
C
```

Requires:

```text
B
```

Requires:

```text
A
```

The recursion ends when:

- A known fact is found.
- No supporting rule exists.

## Sub-goals in Backward Chaining

Sub-goals are intermediate conditions that must be proven before the main goal can be established.

Example:

Rule:

```text
IF engine_turns AND fuel_available THEN car_starts
```

Goal:

```text
car_starts
```

Sub-goals:

- engine_turns
- fuel_available

Both must be verified.

## Working Memory in Backward Chaining

Working memory stores:

- Known facts.
- Proven sub-goals.
- Intermediate results.

Unlike forward chaining, backward chaining usually stores **only the information needed to prove the current goal**.

## Rule Matching in Backward Chaining

The inference engine searches for rules whose **conclusion matches the current goal**.

Example:

Goal:

```text
flu
```

Rules:

```text
R1: IF fever AND cough THEN flu
R2: IF headache THEN flu
R3: IF cold THEN cough
```

Matching rules:

- R1
- R2

The engine attempts to prove the conditions of these rules.

---

## AND/OR Goal Trees

Backward chaining often uses **AND/OR trees**.

### AND Relationship

Rule:

```text
IF fever AND cough THEN flu
```

Both conditions must be true.

```text
       flu
      /   \
   fever cough
```

### OR Relationship

Rules:

```text
R1: IF fever AND cough THEN flu
R2: IF virus_test_positive THEN flu
```

Either rule can prove the goal.

```text
           flu
          /   \
        R1     R2
```

## Advantages of Backward Chaining

### 1. Efficient for Specific Goals

Searches only the rules relevant to the desired conclusion.

### 2. Reduced Computation

Avoids generating unnecessary facts.

### 3. Memory Efficient

Stores only goal-related information.

### 4. Suitable for Diagnostic Systems

Excellent for question-answering and diagnosis.

### 5. Natural Human Reasoning

Humans often reason backward from a desired conclusion.

## Disadvantages of Backward Chaining

### 1. Goal Required

Cannot start reasoning without a specific goal.

### 2. Recursive Complexity

Deep rule chains may increase recursion.

### 3. Repeated Searches

The same sub-goals may be evaluated multiple times.

### 4. Less Suitable for Dynamic Data

Not ideal when facts continuously change.

## Applications of Backward Chaining

Backward chaining is widely used in:

- Medical diagnosis.
- Legal reasoning.
- Troubleshooting systems.
- Technical support systems.
- Intelligent tutoring systems.
- Query processing.
- Logic programming.
- The Prolog programming language.

## Backward Chaining in Expert Systems

A medical expert system may use backward chaining.

### Goal

```text
malaria
```

### Rule

```text
IF fever AND chills THEN malaria
```

The system asks:

- Does the patient have fever?
- Does the patient have chills?

If both answers are yes, malaria is diagnosed.

Thus backward chaining naturally supports **interactive consultation systems**.

## Forward Chaining vs Backward Chaining

| Feature | Forward Chaining | Backward Chaining |
| --- | --- | --- |
| **Approach** | Data-driven | Goal-driven |
| **Starting Point** | Known facts | Desired goal |
| **Direction** | Facts → Goal | Goal → Facts |
| **Fact Generation** | Generates many facts | Generates only relevant facts |
| **Efficiency** | Better for broad inference | Better for specific queries |
| **Memory Usage** | Higher | Lower |
| **Applications** | Monitoring, control, prediction | Diagnosis, query answering, expert consultation |

## Advantages and Disadvantages Summary

| Advantages | Disadvantages |
| --- | --- |
| Goal-directed reasoning | Requires a predefined goal |
| Efficient for specific queries | Recursive complexity |
| Reduced unnecessary inference | Possible repeated sub-goal evaluation |
| Memory efficient | Less suitable for dynamic environments |
| Ideal for diagnosis | Depends on goal formulation |

## Summary

**Backward chaining** is a **goal-driven inference mechanism** in which reasoning begins with the desired conclusion and works backward through inference rules to verify whether the goal can be satisfied by known facts. The inference engine selects rules that conclude the goal, treats their conditions as sub-goals, and recursively attempts to prove each sub-goal. Backward chaining is widely used in expert systems, medical diagnosis, troubleshooting systems, and logic programming. Its main advantage is efficient goal-oriented reasoning, while its major limitation is that it requires a predefined goal and may involve recursive rule evaluation.
