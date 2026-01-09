21/8/2025

### 1. Tracking intro

In localization, a robot uses its sensors to determine where exactly it was in the environment and then moved accordingly
![[Pasted image 20250821111507.png]]

But in self driving cars it is important to detect other vehicles as well and make sure we do not run into them. Below is an image from the google self driving car sensor where other cars are shown in red and their movement is also captured
![[Pasted image 20250821111834.png]]

Different methods of tracking -
![[Pasted image 20250821111901.png]]

We will focus on Kalman filter based tracking in this section, where the distribution is continuous and unimodal

Question 1
![[Pasted image 20250821112125.png]]

### 2. Gaussian Intro

In monte-carlo localization, we created a histogram from our probability distribution, where sum of all the discrete data points or distributions summed up to 1, in Kalman filters we will have gaussian distribution, where area underneath the curve sums up to 1.

![[Pasted image 20250821112621.png]]

1-D gaussian
![[Pasted image 20250821112948.png]]

![[Pasted image 20250821113205.png]]

Think of it like this: A 1-D Gaussian describes how likely you are to observe a value around some mean μ\muμ, with uncertainty (spread) defined by σ\sigmaσ.

Question 2
![[Pasted image 20250821113426.png]]

Note:- Gaussian function are usually in the shape of a Bell curve.
The single peak means - uni modal.
option 3 is bimodal.

Question 3
![[Pasted image 20250821113714.png]]

Variance is measured as the spread, larger variance, more spread is the function, can be proved using the function as well. More the spread, more is the uncertainity of the actual state.
![[Pasted image 20250821113845.png]]

Which Gaussian to prefer in a self driving car ?
Question 4
![[Pasted image 20250821114032.png]]
![[Pasted image 20250821114050.png]]


Refer VSC code for coding questions.

3. Measurement and Motion

Similar to the localization approach, even Kalman filters follow a 2 step approach , that is measurement from the sensors, followed by motion.

Here the math changes but basic principle remains the same.

![[Pasted image 20250821120831.png]]

Question 5
![[Pasted image 20250821121133.png]]

Question6
![[Pasted image 20250821121443.png]]


Coming back to Kalman Filters using Gaussians for implementing these steps

![[Pasted image 20250821130140.png]]

Question 7 - Given initial mean in Black(prior) and new measurement(new sensor measure) mean in purple, where will the new mean be located ?
![[Pasted image 20250821130328.png]]

Question 8
![[Pasted image 20250821130659.png]]


This is because when we multiply 2 gaussians we gain information, information gain means more certainty. More certainty means lower variance, hence narrower graph
![[Pasted image 20250821130907.png]]

![[Pasted image 20250821131108.png]]
P(X) - prior
P(Z/X) - new measurement
P(X/Z) - resulting probability distribution.

Question 9 - Calculate new mean and variance
![[Pasted image 20250821131550.png]]

Question 10 - Same as above but different values
![[Pasted image 20250821131943.png]]

Question 11

![[Pasted image 20250821204346.png]]

Answer - B

Question 12-
![[Pasted image 20250821205013.png]]

When we look at the formula for a new variance, we see that it is independent of the mean. Refer the question 9 image. Hence multiplying the 2 distributions will result in information gain/ reduced variance which will result in a narrower distibution.

![[Pasted image 20250821204932.png]]
### 22/8/2025 - 

For calculating new mean and variance see gaussian.py in code notes.
Things we already know - Measurement update, that is how to calculate the new mean and new variance.
![[Pasted image 20250822120325.png]]

Gaussian motion - Once we have the new mean and new variance calculating the new position is very is as it is just addition -
![[Pasted image 20250822120554.png]]
![[Pasted image 20250822121035.png]]


We add position to old mean, as that is our updated position we want to be in.
We also lose information because when we move to a new position intuitively thinking, we lose information.

### 1. The big picture

In a Kalman filter:

- **Motion update (Prediction):** "Where do I think I’ll be next?"
- **Measurement update (Correction):** "Given new evidence, how should I adjust my belief?"

Both your belief and your measurement are modeled as **Gaussian probability distributions**.

---
### 2. Why Gaussians?

A Gaussian PDF is nice because it’s fully described by just two numbers:
- **Mean (μ):** Best guess (the peak of the bell curve).
- **Variance (σ²):** How uncertain I am (the spread).

So the Kalman filter boils down to:  
🔹 Update mean = adjust where the center of the Gaussian is.  
🔹 Update variance = adjust how wide the Gaussian is (how confident I am).

---
### 3. **Motion update (Prediction step)**
Think: _“I moved, but I’m not perfect. My belief spreads out.”_
- Before motion, I have `N(μ_prior, σ_prior²)`.
- Motion model says: “You should move by Δ, but with some noise (σ_motion²).”
- So new belief becomes:
    - Mean shifts: `μ_pred = μ_prior + Δ`
    - Variance grows: `σ_pred² = σ_prior² + σ_motion²`

**Intuition:**  
If you thought you were at 5 with ±2 error, and you move forward 3 but your motion is noisy with ±1, now you believe you’re around 8 but with larger uncertainty (√(2²+1²) ≈ 2.24 spread).

👉 Motion update always makes you **less certain** because you’re relying on a noisy model.

### 4. **Measurement update (Correction step)**

Think: _“I looked around, and the sensor gives me a hint. Trust it based on its reliability.”_
- Predicted belief: `N(μ_pred, σ_pred²)`
- Sensor reading: `N(μ_meas, σ_meas²)`

The new belief is the **product of two Gaussians** → another Gaussian:
- New mean:
    `μ_new = (σ_meas² * μ_pred + σ_pred² * μ_meas) / (σ_pred² + σ_meas²)`
    
- New variance:
    `σ_new² = (σ_pred² * σ_meas²) / (σ_pred² + σ_meas²)`

**Intuition:**  
This is just a **weighted average** of the prediction and measurement:
- If the sensor is very accurate (σ_meas small), trust it more.
- If the prediction is very accurate (σ_pred small), trust it more.
- The variance always shrinks compared to either input → you’re more confident after combining. 
---
### 5. Putting them together
Every cycle:
1. **Prediction:** Push mean forward, inflate variance.
2. **Correction:** Blend with measurement, shrink variance.

So the filter oscillates between:

- “I think I know where I am, but I’m drifting (motion).”
- “Oh! A measurement! Let’s tighten the guess (correction).”
---
### 6. A metaphor 🌍

Imagine you’re walking in fog:
- You think you walked 3m forward → but you’re not sure (motion update spreads your belief).
- You then glimpse a blurry landmark → it pulls your belief closer, with less uncertainty (measurement update shrinks it).
- Repeat: walk (spread), see (shrink).

That’s the Kalman dance.

Until now we have seen 1-D Kalman Filters
![[Pasted image 20250822130313.png]]

Multivariate gaussians
![[Pasted image 20250822134218.png]]
When there are more than 1 Dimensions we can use this. Don't have to remember the formula though.

In 1-D we saw a bell curve, but in 2-D the graph looks something like this-
![[Pasted image 20250822134600.png]]

Kalman Filter Land
In the below image, graph one gives the position w r t time
The second graph tells us the velocity (X dot - y-axis) w .r .t position X (x-axiz).
Initially we do not know velocity so our correlation is somewhat vertically aligned.
![[Pasted image 20250822134808.png]]

Question 13.

![[Pasted image 20250822135115.png]]

Question 14
![[Pasted image 20250822135440.png]]


![[Pasted image 20250822141847.png]]
### 1. **Observables vs Hidden states**

- **Observables** = what you can directly measure (e.g., GPS position, noisy sensor readings, radar returns).
- **Hidden states** = what you _actually care about_ but cannot measure directly (e.g., true position, true velocity, acceleration).
Sensors don’t give you the truth — they give you **noisy signals**.
---
### 2. **What the drawing shows**
- The oval labeled **“Observables”** = sensor data you have access to.
- The arrows pointing down to **“Hidden”** = Kalman filter using those observations to infer the true (hidden) state.
- The “Big Lesson” here is: _Kalman filters are all about using noisy, partial observations to recover the underlying hidden state._
---
### 3. **How Kalman does it**
- **Prediction step**: use your motion/dynamics model to project the hidden state forward in time.
- **Update step**: use new observables (measurements) to correct that prediction.
- Over time, the filter balances model predictions with actual observations to estimate the hidden variables more accurately than either alone.
---
### 4. **Example**
Suppose you want to know a car’s _true velocity_ (hidden):
- Your GPS gives you position readings (observable), but noisy.
- You can’t directly measure the true velocity all the time.
- Kalman filter takes those GPS positions, combines them with a motion model (e.g., physics equations of motion), and produces a much better estimate of both position _and_ velocity.
---
👉 So this diagram is emphasizing: **Kalman filters let you reconstruct hidden states from noisy observable data by combining models and measurements.**

Kalman Filter Design
Requirements- 
1. State variables(usually  a matrix)
2. Measurements measurement function

![[Pasted image 20250822142728.png]]

This may not be asked to write from scratch but just see for exam

![[Pasted image 20250823151245.png]]

![[Pasted image 20250823151304.png]]
![[Pasted image 20250823151323.png]]



Kalman Filter special notes
![[Pasted image 20250824182248.png]]

![[Pasted image 20250824183303.png]]

The Kalman Gain
![[Pasted image 20250824184555.png]]


The three Kalman equations-

![[Pasted image 20250824190246.png]]

Example 1
![[Pasted image 20250824190718.png]]

Example 1 iterated 
![[Pasted image 20250824191546.png]]
We can see how the estimated value is tapering down to the true value.

Now doing the same for multimodal inputs with more parameters
![[Pasted image 20250824193457.png]]

Step 1 - The State Matrix
![[Pasted image 20250824194816.png]]

2-Dimensions
![[Pasted image 20250824211107.png]]



Another Example-
![[Pasted image 20250824201125.png]]

Finding New F matrix Example - 
![[Pasted image 20250824210204.png]]

