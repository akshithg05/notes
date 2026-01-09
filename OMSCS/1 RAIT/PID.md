Question 1
![[Pasted image 20250916195607.png]]

## 1. Smoothing Algorithm

![[Pasted image 20250916195948.png]]

Question 2
![[Pasted image 20250916200312.png]]

Question 3
![[Pasted image 20250916200509.png]]

Question 4
![[Pasted image 20250916201151.png]]

Smoothing Algorithm
![[Pasted image 20250916202143.png]]

## 🚙 The Problem

When you plan a path with search algorithms (like **A***), the path is:

- Optimal in terms of cost (fewest steps, shortest distance, etc.),
    
- But it often looks **jagged** — sharp turns, zig-zags.
    

Robots (and cars) can’t follow jagged paths well:

- A car has turning constraints (you can’t instantly turn 90°).
    
- Noise in actuators and sensors makes sharp paths impractical.
    
- Smoother paths are more efficient and safer.
    

---

## 🧠 The Intuition Behind Smoothing

We want to take the “blocky” path from A* and make it smooth while **still staying close to the original path**.

There are **two competing desires**:

1. **Stay true to the original path** → Don’t wander too far away, otherwise you might collide with obstacles.
    
    - This is controlled by `weight_data`.
        
    - Higher `weight_data` = cling more tightly to original path.
        
2. **Make the path smooth** → Adjust each point so it’s more in line with its neighbors (like pulling a rubber band tight).
    
    - This is controlled by `weight_smooth`.
        
    - Higher `weight_smooth` = straighter, smoother line.
        

---

## ⚖️ The Gradient Descent Rule

At each step we update:

![[Pasted image 20250916205928.png]]


So:

- The **first term** is like a spring attaching the smoothed path back to the original (so we don’t drift too far).
    
- The **second term** is like a spring pulling each point toward the midpoint of its neighbors (so it becomes straighter).
    

---

## 🔧 Why Iteration?

If you only apply this update once → you just “nudge” points a little.  
If you apply it **many times** → the path gradually settles into a balance between:

- Following the original points,
    
- And becoming smooth.
    

That’s why we iterate until the updates become tiny (`tolerance`).

---

## 🌉 Analogy

Think of the original path as **wooden pegs nailed into a board**.

- The start and end pegs are nailed down (they can’t move).
    
- The other pegs are attached to both:
    
    - A spring pulling them toward where they were originally placed,
        
    - Springs connecting them to their neighbors.
        

When you let go, the system of springs relaxes into a **smooth curve** — still close to the pegs, but much nicer to follow.

---

## 🚀 End Goal

The result is:

- A path that is **smooth, drivable, and feasible**,
    
- But also **respects obstacles** (since it stays close to the original safe path).
![[Pasted image 20250916211159.png]]

Question 5
![[Pasted image 20250916211309.png]]

Question 6
![[Pasted image 20250916211811.png]]


## 17/9/2025

![[Pasted image 20250917192040.png]]


PID controller
![[Pasted image 20250917201439.png]]

![[Pasted image 20250917201523.png]]

Twiddle
![[Pasted image 20250917203423.png]]


