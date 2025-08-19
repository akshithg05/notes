
# 18/8/2025

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

# 19/8/2025

Move function (Exact motion, in a cyclic world)
![[Pasted image 20250819195321.png]]

Inaccurate Robot motion
![[Pasted image 20250819195551.png]]


Here what we are trying to say is a robot wants to move U steps, the probability that it moves U steps is 0.8, the probability it overshoots by 1 step is 0.1 and the probability it undershoots by 1 is also 0.1
![[Pasted image 20250819200257.png]]
If the first cells diagram is the initial diagram, after the robots motion, the second diagram is the updated motion.

example 2
![[Pasted image 20250819201247.png]]

Example 3
![[Pasted image 20250819201643.png]]
In this case it is a special case where, it will still give the same 0.2 for each cell. If we consider movement U=2 for every cells' value, we will get (0.02 + 0.16 + 0.02 = 0.2) in every cell.

Intution
Let’s think of this as a story of a little robot moving around a circular world 🌍:

---
### 🔹 Deterministic Move (the simple case)

If the robot starts at position 1 with 100% certainty (`[0,1,0,0,0]`) and you tell it _“move 2 steps forward”_, then it **always ends up at exactly position 3**.  
So after the move, the probability distribution is:

`[0,0,0,1,0]`

Super neat, super clean. But real robots aren’t that perfect.
---
### 🔹 Why Inexact Moves?

Imagine your robot has:
- **Slippery wheels**
- **Uneven floor**
- **Sensors with delay**

So when you say _“move 2 steps forward”_:
- **Most of the time (0.8)** → it lands where you expect (exact move).
- **Sometimes (0.1)** → it overshoots, rolling one extra step.
- **Sometimes (0.1)** → it undershoots, stopping short by one step.

The robot is **unreliable**, so you hedge your bets with probabilities.

---
### 🔹 Intuition Behind the Distribution
Think of the distribution as **our belief about where the robot might be**.
- When we start: `[0,1,0,0,0]` → _“I’m 100% sure the robot is at position 1.”_
- After the move: `[0,0,0.1,0.8,0.1]` →  
    _“I strongly believe the robot is at position 3, but there’s a small chance it slipped and is at 2 or 4.”_
    
This mirrors how **humans think about uncertainty**: we don’t say “it’s exactly here,” we say “it’s most likely here, but maybe there too.”

---
### 🔹 Uniform Distribution Case (p3)
If the robot starts with a **completely uncertain position**: `[0.2,0.2,0.2,0.2,0.2]`,  
then moving doesn’t really help — because every position spreads its uncertainty equally.  
So the distribution stays uniform.
This matches intuition:
- If you had _no clue_ where the robot was, moving it doesn’t magically give you more information.
---
### 🔹 Big Picture Intuition
- **Move function** spreads the probability cloud, because motion is unreliable.
- **Sense function** squeezes the cloud, because sensing gives us sharper clues.
- Alternating move + sense = the robot gradually **homes in on where it must be**, despite noise.
---
👉 So the intuition:
- **Move = uncertainty grows** (the cloud gets blurrier).
- **Sense = uncertainty shrinks** (the cloud gets sharper).
- Together, they balance into **robust localization**.


## Limit Distribution
![[Pasted image 20250819204740.png]]

**Limit Distribution in a Cyclic World**  
When a robot moves in a cyclic world with inexact motion (overshoot/undershoot probabilities), each movement redistributes probability across neighboring positions. If the robot keeps moving indefinitely, the uncertainty spreads out until every position is equally likely. At this point, the distribution reaches **balance**, where no position is favored over another. This balanced state is called the **limit distribution**, and it is always **uniform** (e.g., `[0.2, 0.2, 0.2, 0.2, 0.2]` for 5 cells).

Mathematical intution

**Limit Distribution in a Cyclic World**  
When a robot moves in a cyclic world with inexact motion (with probabilities of exact, overshoot, and undershoot), its belief distribution spreads out over time. After many moves, the distribution reaches a **balanced state** where each cell receives the same probability mass from its neighbors.

Mathematically, for any cell XiX_iXi​:

p(Xi)=0.8⋅p(Xi−1)+0.1⋅p(Xi−2)+0.1⋅p(Xi)p(X_i) = 0.8 \cdot p(X_{i-1}) + 0.1 \cdot p(X_{i-2}) + 0.1 \cdot p(X_{i})p(Xi​)=0.8⋅p(Xi−1​)+0.1⋅p(Xi−2​)+0.1⋅p(Xi​)

In this balanced state, all p(Xi)p(X_i)p(Xi​) are equal, so the only possible solution is a **uniform distribution** (e.g., `[0.2, 0.2, 0.2, 0.2, 0.2]` for 5 cells).

Thus, if the robot keeps moving forever in a cyclic world, the distribution always converges to **uniform**.

## IMP: Move- Sense Cycle
![[Pasted image 20250819212936.png]]

### **1. Move (Prediction step)**

- When the robot **moves**, it becomes _less certain_ about its exact position.
- Example: If the robot thinks it’s at cell 3 and tries to move 1 step, because of noise (overshoot/undershoot), it might actually end up in cell 2, 3, or 4.
- This spreads out the probability distribution → the belief becomes _blurred_.
- **Effect:** The robot **loses information** (entropy increases).
---
### **2. Sense (Update step)**
- When the robot **senses**, it compares the sensor measurement with the actual world.
- If the sensor says “red,” then all red cells get higher probability, and all non-red cells get lower probability.
- This sharpens the distribution → the belief becomes more concentrated.
- **Effect:** The robot **gains information** (entropy decreases).
---
### **3. The Cycle**
- The robot alternates between **move (loses certainty)** and **sense (gains certainty)**.
- Over time, this balance lets the robot track its position, even in noisy worlds.
---
👉 Intuition:
- **Move = spreading out belief (uncertainty grows).**
- **Sense = correcting belief (uncertainty shrinks).**

In **probabilistic robotics** (or more generally, Bayesian filtering):

- **Motion step (prediction/update using control):**
    - When the robot moves, we add _uncertainty_ because motion is never perfect.
    - The probability distribution “spreads out.”
    - That means the **entropy (uncertainty)** of the belief increases.

- **Measurement step (correction/update using sensors):**
    - When the robot senses the environment, the measurement gives information that “sharpens” the distribution.
    - The belief becomes more _peaked_ (less spread out).
    - That means the **entropy decreases** — uncertainty goes down.
![[Pasted image 20250819220324.png]]

So, the process is like:

🔄 **Motion → entropy ↑ (less certain)**  
🔍 **Measurement → entropy ↓ (more certain)**

Example 1 (Refer coding example 11)
![[Pasted image 20250819214202.png]]
Looking at this example, the robot sensed red, moved right, sensed green and moved right, by looking at the world and comparing, the robot must most likely be in cell number 5 (last cell, green). And by seeing the results, we see probability of the last cell green in 0.38 which is the highest, so robot is most likely there!. 

Example 2 (refer coding example 2 in localization.py)

Localization summary
![[Pasted image 20250819220016.png]]



# Formal Definition of Probability 1

Baye's rule 
p (Xi/Z) is posterior probability distribution
p(Xi) - prior belief
p(Z/Xi) - measurement probability (the weight attached - pHit/pMiss)
p(Z) - normalized sum

![[Pasted image 20250819222025.png]]

To make it more formalized
![[Pasted image 20250819222406.png]]

p bar is non normalized probability, alpha is sum of all non normalized probability vector.