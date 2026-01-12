
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
