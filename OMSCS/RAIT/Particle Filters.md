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

