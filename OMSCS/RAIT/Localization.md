


Total probability
![[Pasted image 20250818193106.png]]

Probability after sence
![[Pasted image 20250818200615.png]]

Normalized Distribution
![[Pasted image 20250818201332.png]]

![[Pasted image 20250818202623.png]]

Visualizing our code(for code see localization.py in notes)
![[Pasted image 20250818205733.png]]

What we have learnt till now:

### 🚩 What your `sense` function is doing

- You start with a **prior distribution** `p` (your belief about where you might be before sensing).
- Then you take a **measurement** `Z` (like “red” or “green”).
- The function updates the prior using **Bayes’ rule**:

p(Xi∣Z)  =  p(Z∣Xi) p(Xi)∑jp(Z∣Xj) p(Xj)p(X_i \mid Z) \;=\; \frac{p(Z \mid X_i)\,p(X_i)}{\sum_j p(Z \mid X_j)\,p(X_j)}p(Xi​∣Z)=∑j​p(Z∣Xj​)p(Xj​)p(Z∣Xi​)p(Xi​)​

This new distribution is called the **posterior distribution**.

---
### 🌍 Intuition in plain words
You are calculating:
> “Given my prior belief about where I am, and given the new sensor reading Z, what is my updated belief about where I am?”

- **Prior** = “Before seeing the sensor, I thought all positions were equally likely.”
- **Likelihood** = “How likely is it to see `Z` (red/green) if I were at each position?” (this is what `pHit` and `pMiss` encode).
- **Posterior** = “After considering the evidence, here’s my new belief distribution over positions.”

**Bayesian Sense Function (Robot Localization)**
- **p** → Prior distribution: belief about position before sensing (e.g., `[0.2,0.2,0.2,0.2,0.2]`).
- **world** → Map of the environment (e.g., `['green','red','red','green','green']`).
- **Z** → Sensor measurement/observation (e.g., `'red'`).
- **pHit** → Weight applied if measurement matches the world (sensor correct).
- **pMiss** → Weight applied if measurement does not match the world (sensor incorrect).

**Process:**
1. Multiply each prior probability by `pHit` if `world[i] == Z`, else by `pMiss`.
2. Normalize so the new probabilities sum to 1.
3. The result is the **posterior distribution**: updated belief after sensing.

**Formula:**

![[Pasted image 20250818210637.png]]
👉 In short: _Update your belief about position using the sensor reading._


Nice — you’ve just extended your code to handle **multiple sensor measurements** in sequence 🎉

Let’s break down exactly what’s happening:

---



### 🔎 What are we trying to do?

We’re trying to figure out **where the robot is**, given a noisy sensor. The robot sees “red” or “green,” but the sensor isn’t perfect:
- If it sees **red**, there’s a **60% chance it’s actually red**, but also a **40% chance it’s wrong**.
- If it sees **green**, there’s a **20% chance it’s actually green**, and an **80% chance it’s wrong**.

So every time the robot makes a measurement, we should trust it **a little**, but not completely.

---
### ⚙️ What happens step by step?
1. **Start with ignorance (prior):**  
    Initially, the robot has no idea where it is → probability is spread **uniformly** across all cells (each cell = 20%).
    
2. **Take a measurement (say “red”):**
    - If the robot sees “red,” we should lean towards cells that are red.
    - But we don’t fully trust it → so we only increase probability for red cells by 0.6 and for green cells by 0.2.
    
3. **Normalize (renormalize total = 1):**  
    After this weighting, the total probability may not equal 1. Normalizing just rescales things so probabilities sum to 100%.
    - Now, red cells have **higher probability** (because the sensor said “red”).
    - Green cells still have **some probability** (because the sensor might be wrong).
    
4. **Repeat with more measurements:**  
    Each new measurement keeps shifting probabilities.
    - If the sensor keeps saying “red,” confidence in red cells grows stronger.
    - If it flips to “green,” probabilities shift towards green cells.

---
### 🤯 The intuition
The robot is **updating its belief about the world**.
- **Before measurement:** “I could be anywhere equally.”
- **After measurement:** “Since my sensor said ‘red,’ I’m more likely in a red spot. But I’ll still keep some chance for green, because my sensor might be lying.”

It’s like a detective who gets **clues**: each clue doesn’t prove the answer, but together they narrow down the possibilities.

---
👉 So, when we normalize probabilities, we’re not saying the robot is definitely in green or red.  
We’re saying:
- “Given the evidence so far, how should I **weigh** the chances of being in each location?”


