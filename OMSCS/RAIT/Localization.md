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




**Multiple sensor measurements** in sequence (refer code 7. in localization.py)
### 1. Initial belief

`p = [0.2, 0.2, 0.2, 0.2, 0.2]`
Uniform prior → equally likely to be in any of the 5 cells.

---
### 2. World (map)
`world = ['green', 'red', 'red', 'green', 'green']`
So:
- Cell 0 = green
- Cell 1 = red
- Cell 2 = red
- Cell 3 = green
- Cell 4 = green

---

### 3. Measurements

`measurement = ['red','green']`
This means your robot’s sensor first saw **red**, then **green**.

---
### 4. The `sense` function
Same as before — it takes a prior distribution `p` and updates it based on one measurement (`Z`).
- If the cell matches the measurement → multiply by `pHit`.
- Otherwise → multiply by `pMiss`.
- Then normalize so the distribution sums to 1.
---

### 5. The loop

`for k in range(len(measurement)):     p = sense(p, measurement[k])`
- Step 1: Apply `sense(p, 'red')` → posterior after first measurement.
- Step 2: Apply `sense(p, 'green')` → posterior after second measurement.

So now `p` is the belief **after incorporating both measurements in sequence**.

---
### 6. The extra line
`result = sense(p,Z)`

⚠️ Here `Z` is **not defined** in this code snippet (you probably copied it from the previous version).  
That line will throw a `NameError` unless you still have `Z` defined elsewhere.

If your goal was just to apply the sequence of measurements, the code should simply be:

`for Z in measurement:     p = sense(p, Z)  print("Normalized Result:", p)`

---

### 🚩 What you’re really calculating

You’re performing **sequential Bayesian updates**:

p(X∣Z1,Z2)    ∝    p(Z2∣X) p(Z1∣X) p(X)p(X \mid Z_1, Z_2) \;\;\propto\;\; p(Z_2 \mid X)\,p(Z_1 \mid X)\,p(X)p(X∣Z1​,Z2​)∝p(Z2​∣X)p(Z1​∣X)p(X)

- Start with prior p(X)p(X)p(X).
- Update with first measurement Z1=redZ_1 = \text{red}Z1​=red.
- Update again with second measurement Z2=greenZ_2 = \text{green}Z2​=green.
- End up with the posterior p(X∣Z1,Z2)p(X \mid Z_1, Z_2)p(X∣Z1​,Z2​).
---

👉 In words: You are calculating the robot’s updated belief about its position after sensing `"red"` and then `"green"`.