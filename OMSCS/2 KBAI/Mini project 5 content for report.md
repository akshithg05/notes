# 🧱 3. Agent Performance (10 points)

### Include:

- How many test cases passed (e.g., 20/20)
- Whether:
    - always found correct solution
    - always minimal solution

### Then:

## 🔹 Strengths

- Works well when:
    - solution size is small
    - diseases don’t conflict heavily

## 🔹 Weaknesses

- Struggles when:
    - many diseases interact
    - larger combinations needed

👉 Even if it works perfectly:

- still mention **theoretical weaknesses**

---

# 🧱 4. Efficiency Analysis (5 points)

### Include:

## 🔹 Time Complexity

- Worst case:
    - O(2ⁿ)
- Why:
    - exploring subsets

## 🔹 Practical Performance

- BFS stops early
- small n (≤ 24)

## 🔹 Growth Behavior

- As diseases increase:
    - exponential growth
    - slower runtime

👉 Bonus:

- mention constant factor (26 vitamins)

---

# 🧱 5. Optimizations / Clever Ideas (Important signal)

### Include:

- vector representation (instead of strings)
- early stopping via BFS
- avoiding duplicate permutations using index
- no unnecessary recomputation

👉 Even if simple — present it as intentional design

---

# 🧱 6. Human Comparison (10 points — HIGH IMPACT)

### Structure:

## 🔹 Similarities

- Humans also:
    - consider combinations
    - eliminate inconsistent explanations

## 🔹 Differences

- Humans:
    - use heuristics (intuition)
    - don’t explore all combinations
- Agent:
    - exhaustive but systematic

## 🔹 Performance Comparison

- Agent:
    - more accurate
    - slower in worst case
- Humans:
    - faster heuristically
    - may miss optimal solution

👉 This section must show **depth** — not generic

---

# 🧱 7. Conclusion (Short)

### Include:

- Restate:
    - search-based approach works well
- Key takeaway:
    - correct representation + BFS = effective solution