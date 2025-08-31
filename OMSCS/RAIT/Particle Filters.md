Question 1
![[Pasted image 20250829144250.png]]


Question 2
![[Pasted image 20250829144638.png]]

![[Pasted image 20250829144916.png]]

Question 3
![[Pasted image 20250829145111.png]]

![[Pasted image 20250829145222.png]]
The Kalman filters are more efficient than the histogram filters as Kalman filter has quadratic efficiency, whereas Histogram filters have exponential efficeincy.

Question set 4
![[Pasted image 20250829160715.png]]

Kalman filters are exact only for linear systems, if the world goes into a non linear system Kalman filters are also just an approximation.

## Particle filters

![[Pasted image 20250829161126.png]]

A particle filter is represented using particles. In the below diagram, each of the red particles , of which there a several thousand, is a discrete guess, where the world might be. X coord, Ycoord and heading direction comprise a single guess. It is a collection of several thousands of these guesses., that together comprise an approximate representation for the posterior of the robot.
![[Pasted image 20250829165501.png]]

As the robot moves, some particles will survive and some will be removed, and correct set of particles survive. The esscence is to make particles guess where the robot is moving and then make the particles survive.

The robot class in the Particle filters assignment and classes.
![[Pasted image 20250829180256.png]]

Creating particles for particle filter
![[Pasted image 20250829180451.png]]


Importance weight
![[Pasted image 20250830123239.png]]

Larger the weight, more is the importance.  Importance weight is difference between actual measurement and predicted measurement.

Resampling in particle filters
![[Pasted image 20250830125359.png]]

Question 5 - Answer to this question is the next question.
![[Pasted image 20250830125956.png]]

Question 6
![[Pasted image 20250830130116.png]]

Explanation - Due to the small alpha value and low weight, it is possible that this particle might be dropped and never picked during resampling.

Question 7
![[Pasted image 20250830130342.png]]
Explanation - Even though it has a large weight, it is possible that in each of the resampling steps, this particle might never be picked!.

Question 8
![[Pasted image 20250830131106.png]]

Explanation - 0.6 (probability of not sampling P3), and 5 picks so 0.6 x 0.6 x 0.6 x 0.6 x 0.6.

Question 9
![[Pasted image 20250831165724.png]]

Explanation - Orientation does matter, especially for the 2nd part of particle filters.
![[Pasted image 20250831165847.png]]

