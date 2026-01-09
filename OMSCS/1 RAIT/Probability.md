# Basics of Conditional Probability

Probability measures how likely an event is, between **0 and 1**.  
- 0 = impossible  
- 1 = certain  
- Example: Toss a fair coin → `P(H) = 0.5`.

## Conditional Probability
Conditional probability answers:  
**“What is the probability of event A happening, given that we already know event B happened?”**

Notation:
`P(A | B)`

Formula:
`P(A | B) = P(A ∩ B) / P(B),   where P(B) > 0`

- `P(A ∩ B)` = probability that both A and B occur  
- `P(B)` = probability that B occurs  
- Interpretation: Restrict the sample space to cases where **B** happened, then ask how many of those also satisfy **A**.

## Example
A die is rolled once:  
- Event A: number is even → `{2,4,6}`  
- Event B: number > 3 → `{4,5,6}`  

Calculations:
- `P(A ∩ B) = P({4,6}) = 2/6`  
- `P(B) = 3/6`  
- `P(A | B) = (2/6) / (3/6) = 2/3`

Interpretation: If you already know the outcome is greater than 3, then 2/3 of those outcomes are even.

## Important Results
**Law of Total Probability**  
`P(Y) = P(Y | X)P(X) + P(Y | ¬X)P(¬X)`

**Bayes’ Theorem**  
`P(A | B) = [ P(B | A) * P(A) ] / P(B)`

## Key Idea
Conditional probability is about **updating beliefs** when new information is given.
