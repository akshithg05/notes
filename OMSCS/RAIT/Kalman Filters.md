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

