# Imperfect Decisions

## Introduction

In many real-world games and decision-making problems, an intelligent agent cannot make a **perfect decision** because it does not have complete information about the environment or the opponent. Such situations involve **uncertainty, hidden information, randomness, or limited computational resources**.

An **imperfect decision** is a decision that is **not guaranteed to be optimal**, but is the **best possible decision based on the available information**.

Imperfect decision-making is important because most practical AI environments are uncertain and dynamic.

**Examples:** Poker, Bridge, autonomous driving, robotics, medical diagnosis, and financial trading systems.

## Definition

An **imperfect decision** is a decision made under **uncertainty, incomplete information, or limited computational resources**, where the agent selects the action with the **highest expected utility** instead of a guaranteed optimal outcome.

Unlike perfect decisions, imperfect decisions rely on:

- Probability theory
- Heuristic evaluation
- Prediction
- Approximate reasoning
- Learning from experience

## Why Perfect Decisions Are Not Always Possible

Perfect decisions require:

- Complete information
- Deterministic environment
- Rational opponents
- Unlimited computational resources

In real-world problems, these conditions rarely exist.

### Sources of Uncertainty

- Hidden information
- Random events
- Noisy observations
- Time limitations
- Unknown opponent strategies

Therefore, AI systems must make **imperfect but intelligent decisions**.

## Characteristics of Imperfect Decisions

Imperfect decision-making has the following characteristics:

- Incomplete information
- Uncertain outcomes
- Probabilistic reasoning
- Heuristic evaluation
- Approximate optimization
- Opponent prediction

The goal is to choose the **best expected action**, not necessarily the perfect action.

## Imperfect Information Games

A game is called an **imperfect information game** when some information is hidden from one or more players.

| Game | Imperfect Information |
| --- | --- |
| Poker | Yes |
| Bridge | Yes |
| Mahjong | Yes |
| Stratego | Yes |
| Chess | No |
| Tic-Tac-Toe | No |

In these games, the AI must estimate unknown information.

## Sources of Imperfection

### Hidden Information

The agent cannot observe the complete game state.

**Example:** Opponent’s cards in poker.

### Randomness

Chance events affect the outcome.

**Example:** Dice rolls in board games.

### Computational Limitations

The search space may be too large for exhaustive analysis.

### Time Constraints

The AI must make decisions quickly.

### Unpredictable Opponents

Opponents may not always behave optimally.

## Decision-Making Under Uncertainty

When outcomes are uncertain, AI uses the concept of **expected utility**.

### Expected Utility

Expected utility is the weighted average of all possible outcomes.

#### Formula

EU = ∑ P(i) × U(i)

Where:

- \(P(i)\) = probability of outcome \(i\)
- \(U(i)\) = utility of outcome \(i\)

The AI chooses the action with the **highest expected utility**.

## Example of Expected Utility

Suppose an AI has two possible moves.

| Move | Win Probability | Win Utility | Lose Probability | Lose Utility |
| --- | --- | --- | --- | --- |
| A | 0.8 | 10 | 0.2 | -5 |
| B | 0.5 | 20 | 0.5 | -5 |

### Move A

EU(A) = (0.8 × 10) + (0.2 × -5)

EU(A) = 8 - 1 = 7

### Move B

EU(B) = (0.5 × 20) + (0.5 × -5)

EU(B) = 10 - 2.5 = 7.5

Since **7.5 > 7**, the AI selects **Move B**.

## Heuristic Evaluation

When exact computation is impossible, AI uses **heuristic evaluation functions**.

A heuristic estimates the quality of a game state.

### Example

In a strategy game:

```
Evaluation = Resources + Army Strength + Territory Control - Enemy Threat
```

The AI chooses the move with the highest heuristic score.

## Search in Imperfect Decision Problems

Unlike the Minimax algorithm, imperfect decision-making involves:

- Probability
- Chance events
- Estimated opponent behavior

This leads to algorithms such as **Expectiminimax**.

## Expectiminimax Algorithm

Expectiminimax extends the Minimax algorithm by introducing **chance nodes**.

The game tree contains three types of nodes:

- **MAX nodes**
- **MIN nodes**
- **Chance nodes**

### Example Game Tree

```text
              MAX
             /   \
         Chance  Chance
         /   \    /   \
       0.5 0.5 0.5 0.5
       10  -2  6   8
```

### Expected Value Calculation

Left chance node:

EV = (0.5 × 10) + (0.5 × -2)

EV = 4

Right chance node:

EV = (0.5 × 6) + (0.5 × 8)

EV = 7

MAX chooses:

max(4, 7) = 7

Therefore, the AI selects the **right branch**.

## Probability-Based Decision Making

AI estimates probabilities using:

- Past observations
- Opponent modeling
- Bayesian inference
- Machine learning
- Reinforcement learning

These estimates improve decision quality over time.

## Opponent Modeling

The AI predicts the opponent’s future actions.

Common techniques include:

- Historical move analysis
- Pattern recognition
- Behavioral modeling
- Statistical learning

### Example

If a poker player frequently raises with strong hands, the AI updates its strategy accordingly.

## Bounded Rationality

Real AI systems have limited:

- Time
- Memory
- Processing power

**Bounded rationality** means the agent chooses a **satisfactory decision** within available computational resources.

This concept is widely used in:

- Real-time strategy games
- Robotics
- Autonomous systems

## Perfect Decisions vs Imperfect Decisions

| Perfect Decisions | Imperfect Decisions |
| --- | --- |
| Complete information | Incomplete information |
| Deterministic environment | Uncertain or stochastic environment |
| Optimal outcome | Best expected outcome |
| Uses Minimax | Uses Expectiminimax and probabilistic methods |
| Exact search | Heuristic and probabilistic search |
| Chess, Tic-Tac-Toe | Poker, Bridge |

## Advantages of Imperfect Decision-Making

- Handles uncertainty effectively.
- Works with incomplete information.
- Applicable to real-world environments.
- Supports probabilistic reasoning.
- More practical for complex problems.

## Limitations of Imperfect Decision-Making

### No Guaranteed Optimality

The selected action may not be the optimal action.

### Dependence on Probability Estimates

Incorrect estimates reduce decision quality.

### Computational Complexity

Probabilistic search may become expensive.

### Heuristic Errors

Poor evaluation functions can lead to weak decisions.

## Applications

Imperfect decision-making is used in:

- Poker-playing AI
- Autonomous vehicles
- Robotics
- Medical diagnosis
- Financial trading
- Military strategy
- Real-time strategy games
- Recommendation systems

## Key Terms

| Term | Meaning |
| --- | --- |
| Expected Utility | Probability-weighted average utility |
| Chance Node | Node representing random events |
| Heuristic | Estimated value of a state |
| Expectiminimax | Search algorithm with chance nodes |
| Opponent Modeling | Predicting opponent behavior |
| Bounded Rationality | Decision-making with limited resources |

## Decision Process in Imperfect Games

```text
Observe State
      |
      v
Estimate Hidden Information
      |
      v
Predict Opponent Actions
      |
      v
Calculate Expected Utilities
      |
      v
Evaluate Heuristics
      |
      v
Choose Best Expected Action
```

## Summary

**Imperfect decisions** are decisions made under uncertainty, incomplete information, or limited computational resources. Unlike perfect decisions, they do not guarantee an optimal outcome. AI uses **expected utility**, **probability theory**, **heuristic evaluation functions**, and algorithms such as **Expectiminimax** to select the action with the highest expected benefit. Imperfect decision-making is essential in real-world AI applications such as poker-playing systems, autonomous vehicles, robotics, medical diagnosis, and financial prediction.

## Important Questions

1. What are imperfect decisions in AI?
2. Why are perfect decisions not always possible?
3. Explain decision-making under uncertainty.
4. Define expected utility with an example.
5. Describe the Expectiminimax algorithm.
6. Explain heuristic evaluation in imperfect decision-making.
7. Differentiate between perfect and imperfect decisions.
8. Discuss the applications of imperfect decision-making in AI.
