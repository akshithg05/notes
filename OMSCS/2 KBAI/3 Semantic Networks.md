
# Knowledge Representation — Big Picture

## Lesson Preview

This unit focuses on:
- **Knowledge Representations**
- **Semantic Networks**
- **Problem-solving using Semantic Networks**
- **Represent & Reason** (core AI idea)

The key idea throughout the lesson is:

> **How do we represent knowledge so that a machine can reason with it?**

---

## What is Knowledge Representation (KR)?

**Knowledge Representation** is how an AI system:
1. **Stores information about the world**
2. **Uses that information to reason, infer, and solve problems**

In simple terms:
> KR is the bridge between **raw information** and **intelligent behavior**.

---

## Two Core Components of Knowledge Representation

Every knowledge representation has **two essential parts**:
### 1. Language (Vocabulary & Structure)

This defines:
- **What symbols exist**
- **How they can be connected**
- **What kinds of statements can be expressed**

Examples:

- Nodes and links (Semantic Networks)
- Predicates and variables (Logic)
- Slots and values (Frames)

Think of this as:

> **The grammar and vocabulary of thought**


Example : F = ma , here equal (=) is the language representing some entity 

---

### 2. Content (What Goes Into the Representation)

This is the **actual knowledge** encoded using the language:
- Facts
- Relationships
- Properties
- Rules

Example:

- “A dog is an animal”
- “Birds can fly”
- “Tweety is a bird”
    
Think of this as:

> **What the AI knows about the world**

---

### Key Insight ⭐

> The **same content** can be expressed using **different representation languages**,  
> and each language makes **some kinds of reasoning easier and others harder**.

---

## Why Do We Need Multiple Knowledge Representations?

AI has developed **many different representations** because:

- No single representation is best for all problems
- Different problems require different trade-offs:
    - Expressiveness
    - Efficiency
    - Ease of inference
    - Human interpretability

---

## Constituents of a Knowledge Representation

Each representation defines its own **constituents** (building blocks):

Examples:

- **Semantic Networks** → nodes, links, inheritance
- **Logic** → predicates, variables, quantifiers
- **Frames** → slots, fillers, defaults
- **Rules** → if–then statements

These constituents determine:

- What can be represented easily
- What kinds of reasoning are natural
- What kinds of reasoning are difficult or impossible
    

---

## Represent & Reason (Central AI Theme)

AI is not just about storing knowledge.

It is about:

1. **Representing knowledge**
2. **Reasoning over that knowledge**
3. **Deriving new knowledge**

> A representation is only useful if it supports **reasoning**.

This is why the course pairs:
- **Representation** (Semantic Networks)
- **Reasoning** (Problem-solving with them)
    

---

## Mental Model to Keep in Mind (Very Important)

Think of knowledge representation as:
`World → Representation → Reasoning → Decisions`
- If the representation is weak → reasoning fails
- If the representation is strong → reasoning becomes simple

---

## Interview / Exam Nuggets 💡

- Knowledge representation = **language + content**
- Different representations exist because **different problems need different biases**
- Representation choice directly affects **what reasoning is easy**
- Semantic networks are an **early but foundational** KR approach


# Semantic Networks examlpe

![[Pasted image 20260116155744.png]]

Example 2
![[Pasted image 20260116160028.png]]


Quiz
![[Pasted image 20260116160110.png]]

Answer 
![[Pasted image 20260116160250.png]]

Quiz
![[Pasted image 20260116160353.png]]

Answer
![[Pasted image 20260116160445.png]]


### Structure of a semantic networks

![[Pasted image 20260116161223.png]]

![[Pasted image 20260116161629.png]]


### Guards and prisoners problem 

![[Pasted image 20260116161953.png]]


### Guards and prisoners representation
![[Pasted image 20260116162313.png]]

Quiz
possible moves
![[Pasted image 20260116162901.png]]

These are illegal-
![[Pasted image 20260116163024.png]]


Quiz -
![[Pasted image 20260116163130.png]]

Answer 
![[Pasted image 20260116163712.png]]

Collapse into 1
![[Pasted image 20260116163833.png]]

Answer for next step -
![[Pasted image 20260116183136.png]]


Redundant states
![[Pasted image 20260116183217.png]]

Full answer - 11
![[Pasted image 20260116183402.png]]


Question and answer
![[Pasted image 20260116212508.png]]


#### Here below we can have multiple answers

![[Pasted image 20260116212620.png]]


Weights
![[Pasted image 20260116214658.png]]

Both are correct but, whichever has higher will get preference, hence answer 5 is correct.


![[Pasted image 20260117154826.png]]

