
## 1. Fundamental Conundrums of AI (CS7637)
![[Pasted image 20260112222940.png]]

- **Limited resources**  
    Intelligent agents are bounded by time, memory, and computation. Exhaustive search is usually infeasible, so agents rely on heuristics and approximations. “Good enough” solutions are often preferable to perfect but impractical ones.
    
- **Local computation, global constraints**  
    Agents typically reason using partial, local information, even though problems are defined by global constraints. Effective intelligence requires combining local observations into a coherent global interpretation.
    
- **Limits of deductive logic**  
    Pure deductive reasoning is insufficient for many real-world problems. Intelligent behavior often involves abductive reasoning, analogy, and heuristic-driven approaches rather than strict symbolic logic.
    
- **Dynamic world, limited knowledge**  
    Agents operate under uncertainty in environments that change over time. They must revise beliefs, update hypotheses, and adapt as new information becomes available. Incomplete knowledge is expected.
    
- **Explanation is harder than reasoning**  
    Solving a problem is often easier than clearly explaining the reasoning behind the solution. Understanding, justification, and communication of reasoning are central challenges in AI.



## 2. Characteristics of AI Problems

![[Pasted image 20260112223318.png]]

- **Incremental knowledge**  
    Information about a problem often becomes available gradually rather than all at once. Agents must reason and act with partial knowledge and update their understanding over time.
    
- **Recurring patterns**  
    Many AI problems exhibit patterns that repeat across instances. Recognizing and exploiting these patterns is central to intelligent behavior.
    
- **Multiple levels of granularity**  
    Problems can be viewed and solved at different levels of detail, from high-level abstractions to low-level specifics. Effective reasoning often requires switching between these levels.
    
- **Computational intractability**  
    Many AI problems are too complex to solve optimally within reasonable time or space limits, making approximations and heuristics necessary.
    
- **Dynamic world, static knowledge**  
    The environment may change continuously, while the agent’s internal knowledge representation may lag behind or remain fixed unless explicitly updated.
    
- **Open-ended world, limited knowledge**  
    The real world has no fixed boundaries, but an agent’s knowledge is always incomplete, requiring assumptions and generalization.


## 3. Characteristics of AI Agents
![[Pasted image 20260112223722.png]]

- **Limited computing power**  
    AI agents operate under constraints on time, memory, and processing capability, which  restricts the complexity of reasoning they can perform.
    
- **Limited sensors**  
    Agents perceive the world through incomplete and imperfect inputs, meaning their view of  the environment is always partial.
    
- **Limited attention**  
    Agents cannot consider all available information simultaneously and must selectively focus  on relevant aspects of the problem.
    
- **Deductive computational logic**  
    The underlying computational mechanisms of AI systems are primarily deductive, even when  applied to problems that require more flexible forms of reasoning.
    
- **Incomplete knowledge**  
    An agent’s internal knowledge representation is always incomplete relative to the true state of the world.


## KBAI
![[Pasted image 20260112225820.png]]

A KBAI system is a **cognitive system** composed of interacting components:

### 1. **Reasoning (Deliberation)**
- Central process that uses knowledge to draw conclusions, make decisions, and solve problems.
- Acts as the “thinking” component of the agent.
### 2. **Memory**
- Stores knowledge, experiences, rules, cases, or representations.
- Reasoning depends on memory, and reasoning can also update memory.
### 3. **Learning**
- Acquires new knowledge or modifies existing knowledge based on experience.
- Learning feeds into memory and improves future reasoning.

These three form a **closed loop**:
- Reasoning uses memory
- Learning updates memory
- Memory influences future reasoning

This loop is called **deliberation**.

## Beyond normal reasoning 

![[Pasted image 20260112230023.png]]

## Beyond deliberation: the full cognitive system

The larger diagram adds two more layers:

### 4. **Reaction**
- Fast, automatic responses to inputs.
- Does not involve deep reasoning (e.g., reflexes or simple rules).

### 5. **Metacognition**

- “Thinking about thinking.”
- Monitors and controls reasoning and learning.
- Decides:
    - when to reason deeply
    - when to rely on memory
    - when to learn something new

---

## Input → Output flow

- **Input** enters the system (perception, problem instance).
- The agent may:
    - react immediately
    - deliberate using reasoning, memory, and learning
    - reflect via metacognition
- **Output** is the agent’s action or solution.


## Four Schools of Artificial Intelligence
![[Pasted image 20260112231608.png]]
![[Pasted image 20260112231613.png]]


AI approaches can be categorized along two dimensions:

- **Thinking vs Acting**
- **Optimally vs Like Humans**

This creates four schools of AI.

---

### 1. **Agents that think optimally**

- Focus on **correct reasoning** according to formal logic.
- Intelligence is defined by producing _logically valid conclusions_.
- Emphasis is on symbolic reasoning, proofs, and formal representations.

**Example:**

- Machine learning models optimized for accuracy or loss minimization (as shown in the diagram).

**Key idea:**

> Intelligence = rational thought.

---

### 2. **Agents that think like humans**

- Aim to model **human cognitive processes**.
- Concerned with how people actually reason, not how they _should_ reason.
- Often informed by psychology and cognitive science.

**Example:**
- Semantic web systems that encode structured human knowledge.

**Key idea:**

> Intelligence = human-like thinking.
---

### 3. **Agents that act optimally**

- Focus on **rational action**, not internal reasoning.
- An agent is intelligent if it selects actions that maximize performance or utility.
- Internal processes are less important than outcomes.

**Example:**

- Airplane autopilot systems.

**Key idea:**

> Intelligence = optimal behavior.

---

### 4. **Agents that act like humans**

- Aim to behave in ways that appear **human-like**, even if not optimal.
- Often interactive, adaptive, and expressive.
- Success is judged by believability rather than correctness.

**Example:**

- Improvisational robots.

**Key idea:**

> Intelligence = human-like behavior.

---

## Where Knowledge-Based AI fits

Knowledge-Based AI primarily aligns with:

- **Thinking like humans**
- With influence from **thinking optimally**

It emphasizes:

- explicit knowledge representations
- reasoning processes
- explanations of thought

rather than purely optimal action or black-box behavior.
---
### One-line summary

> The four schools of AI differ in whether they prioritize **thought or action**, and whether intelligence is defined as **optimal performance or human-like behavior**.

If you want, next we can:

- Contrast this with **modern ML-heavy AI**, or
- Discuss **why CS7637 emphasizes “thinking” over “acting.”**


[[2026-01-13]]

Quiz 
![[Pasted image 20260113161804.png]]

Answers -
![[Pasted image 20260113161939.png]]


## 1. Cognitive Systems

![[Pasted image 20260113162615.png]]


Cognitive systems are **systems that exhibit human-like intelligence** through the interaction of processes such as **learning, reasoning, and memory**.

## 2. Cognitive Systems Architecture

![[Pasted image 20260113164042.png]]
The system takes input from the physical world and outputs the results back to the physical world.

![[Pasted image 20260113164112.png]]

There can be multiple cognitive systems in the world and each ones' output has the ability to determine and influence the input/ output of the other system.

Architecture
![[Pasted image 20260113164211.png]]

The three layer architecture of the cognitive system - 

#### Layer 1 Reaction

The **reaction layer** handles:
- fast
- automatic
- low-latency responses
It does **not** involve deep reasoning.

**Your example (braking when the car in front brakes)** fits perfectly:
- You perceive the red brake lights
- You respond immediately
- No planning or analysis is required
This is classic **reactive behavior**.

#### Layer 2 Deliberation

The **deliberation layer** is responsible for:
- reasoning
- planning
- evaluating alternatives
- making informed decisions using knowledge and memory

Your lane-change example works well:
- You assess traffic in adjacent lanes
- Consider safety constraints
- Choose whether and when to change lanes

This involves:
- memory (driving rules, past experience)
- reasoning (is there enough space?)
- possibly learning (adjusting behavior over time)

So yes — lane changing is a **deliberative process**.


#### Layer 3 Metacognition

Metacognition is **not just reacting when something goes wrong**.

It is:
- monitoring the reasoning process
- evaluating whether the current strategy is working
- deciding _how_ to think, not _what_ to do

In your driving analogy:

- Realizing that your lane-change strategy is too risky in heavy traffic
- Deciding to switch from “change lanes” to “slow down and wait”
- Choosing to rely more on reaction than deliberation in a stressful situation

So metacognition:

- oversees deliberation
- can modify or redirect it
- operates at a higher level of control


### Summary

The reaction layer handles fast, automatic responses to stimuli without deep reasoning, such as braking immediately when the car in front slows down.

The deliberation layer involves reasoning and planning, such as analyzing surrounding traffic and deciding whether it is safe to change lanes.

Metacognition monitors and controls the deliberation process itself, evaluating whether the current reasoning strategy is effective and adjusting it when necessary.


## KBAI Topics and course structure

![[Pasted image 20260113165700.png]]

1. Fundamentals
![[Pasted image 20260113165751.png]]

2. Planning
![[Pasted image 20260113165812.png]]

3. Common Sense Reasoning
![[Pasted image 20260113200040.png]]

4. Learning 
![[Pasted image 20260113200057.png]]

5. Analogical Reasoning 
![[Pasted image 20260113200126.png]]

6.
![[Pasted image 20260113200206.png]]

7. Design and creativity
![[Pasted image 20260113200228.png]]

8. Metacognition
![[Pasted image 20260113200256.png]]


## Two Approaches to Artificial Intelligence

### 1. Knowledge-Based AI (KBAI)

- Rooted in **cognitive science, psychology, and human reasoning**.
- Focuses on:
    - explicit knowledge representations
    - reasoning processes
    - explanations and justification
- Models intelligence at a **high level of abstraction**, closer to how humans _think_.

In short:
> Intelligence is studied by modeling cognition directly.


Cognition is the set of mental processes by which an agent perceives, thinks, learns, and makes decisions.


---

### 2. Machine Learning–Based AI
- Rooted in **neuroscience, statistics, and optimization**.
- Focuses on:
    
    - learning from data
    - pattern recognition
    - neural networks and deep learning
- Models intelligence at a **low level of abstraction**, inspired by how the brain _learns_.

In short:
> Intelligence is studied by training systems to behave intelligently.
---

## Reductionism vs Holism

- **Machine Learning** is largely **reductionist**:
    - Break intelligence down into neurons, weights, gradients, and loss functions.
    - Intelligence emerges from low-level mechanisms.

- **Knowledge-Based AI** is more **holistic**:
    - Treats reasoning, memory, and learning as interacting cognitive processes.
    - Focuses on the system as a whole rather than its smallest components.

---

## Convergence (Open Question)

In theory:
- High-level cognitive models (KBAI)
- and low-level learning models (ML)

**should converge** toward a unified theory of intelligence.

In practice:

- We do **not yet know**
    - where this convergence will happen
    - how it will happen
    - or what the correct level of abstraction is

This gap is an **open research question**, not a solved problem.