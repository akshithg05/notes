# 🧾 Milestone D Journal — Sections + What to Write

---

# 1️⃣ INTRODUCTION

### Write about:

- Goal of Milestone D
- Mention:
    - Set D problems are **more complex**
    - require **structured reasoning**
- Your approach:
    - still rule-based
    - but **extended**
- 🔥 IMPORTANT:
    - explicitly say what’s new:

👉 Points to include:

- extension from previous milestone
- handling:
    - grid partitioning
    - logical operations
    - pattern completion

---

# 2️⃣ AGENT DESIGN AND WORKING (MOST IMPORTANT — 3 pts)

---

## 2.1 Overall Workflow

Write:

- input: training pairs + test input
- for each rule:
    - apply on training
    - compare with output
    - validate rule
- apply valid rule to test input
- rule ordering (simple → complex)

---

## 2.2 What Changed in Milestone D (🔥 critical)

Write:

- earlier:
    - simple transformations
- now:
    - more structured reasoning

👉 Explicitly mention:

- grid partitioning
- logical reasoning
- pattern completion
- frequency reasoning

---

## 2.3 Types of Transformations (Use YOUR RULES)

Break into categories:

---

### 🔹 A. Logical Grid Operations

Write about:

- AND / OR logic across grids
- combining two halves

👉 Mention rules:

- divide_and_and
- sideways_or

👉 Explain:

- compares corresponding cells
- generates output based on logic

---

### 🔹 B. Grid Partitioning

Write:

- splitting input into sub-grids
- processing separately
- merging results

👉 Mention:

- merge_sideways

---

### 🔹 C. Pattern Completion / Connectivity

Write:

- connecting points
- filling lines
- row / column / diagonal logic

👉 Mention:

- join_plusses
- join_reds

👉 Explain:

- detect endpoints
- fill path between them

---

### 🔹 D. Frequency-Based Reasoning

Write:

- counting colors
- using counts to construct output

👉 Mention:

- sep_grid
- fit_in_slot

👉 Explain:

- mapping frequency → structure

---

### 🔹 E. Object / Boundary Detection

Write:

- detecting borders
- extracting inner region

👉 Mention:

- blue_square_extract

---

### 🔹 F. Symmetry Expansion

Write:

- mirroring across axes
- expanding grid

👉 Mention:

- mirrors_8_sides

---

## 2.4 Prediction Strategy

Write:

- max 3 predictions allowed
- your agent usually returns 1
- why:
    - one rule fits completely

---

# 3️⃣ AGENT PERFORMANCE (1 pt)

Write:

- Training D: X / 16
- Test D: X / 16

Also mention:

- number of rules added
- how many problems covered

---

# 4️⃣ PROBLEMS THE AGENT PERFORMS WELL ON (1.5 pts)

⚠️ IMPORTANT → explain **WHY**, not just WHAT

---

Write categories:

- partition-based problems
- logical combination problems
- pattern completion problems
- symmetry problems
- frequency-based problems

---

For each category explain:

👉 WHY it works:

- consistent transformation
- uniform rule across grid
- structure is predictable

---

# 5️⃣ PROBLEMS THE AGENT STRUGGLES WITH (1.5 pts)

Write:

---

### 🔹 Multi-object reasoning

- multiple shapes
- need separate processing

---

### 🔹 Multi-step transformations

- need sequence of operations
- agent assumes single rule

---

### 🔹 Conditional transformations

- different rules for different regions

---

### 🔹 Unseen patterns

- rule not present in library

---

👉 IMPORTANT: always add **WHY**

Example points:

- rule-based limitation
- no chaining
- no abstraction

---

# 6️⃣ AGENT EFFICIENCY (1 pt)

Write:

---

### Time Complexity

- per rule: O(mn)
- total: O(k × mn)

👉 k = number of rules

---

### Space Complexity

- O(mn)

---

### Runtime behavior

- fast due to small grids
- under a second

---

### Important addition (for D):

- more rules → more runtime
- still manageable

---

# 7️⃣ FUTURE IMPROVEMENTS (🔥 2 pts — VERY IMPORTANT)

⚠️ This section must be **strong and specific**

---

Write:

---

### 🔹 Multi-step reasoning

- allow chaining rules

---

### 🔹 Object detection

- connected components
- apply rules per object

---

### 🔹 Rule selection improvement

- scoring instead of first match

---

### 🔹 Pattern detection layer

- detect type before applying rules

---

### 🔹 Generalization

- reduce hardcoding
- more abstract rules

---

👉 Tie improvements to your struggles

---

# 8️⃣ EXPECTED PERFORMANCE / GENERALIZATION

Write:

- performs well on:
    - structured transformations
- struggles with:
    - unseen / complex tasks
- improvement over C
- still limited by rule-based design

---

# 9️⃣ FEEDBACK REQUESTED

Write:

- need help with:
    - multi-step reasoning
    - generalization
    - pattern detection
- difficulty in:
    - handling unseen problems