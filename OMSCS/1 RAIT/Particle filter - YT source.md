The robot needs to determine its pose (position and orientation) inside an office building. It has the map/ layout of the bulding.

![[Pasted image 20250902192205.png]]

![[Pasted image 20250902192325.png]]

Deadreckoning - Estimating the future position of a robot based on the past position and relative measurements.
![[Pasted image 20250902192431.png]]

Typically we can use a Kalman filter, but for that the Noisy Lidar measurement, the noisy odometry measurement and the resulting state space needs to be Gaussian/ unimodal/ single bell curve distribution.

![[Pasted image 20250902192920.png]]

This is not the case in our current turtle bot problem, hence we cannot use Kalman filters.


Initial state-
![[Pasted image 20250902193032.png]]

![[Pasted image 20250902193113.png]]

The probability distribution of where we are might look something like this (yellow - higher probability ) -
![[Pasted image 20250902193152.png]]

Particle filter initially randomizing the particles

![[Pasted image 20250902193426.png]]

![[Pasted image 20250902193436.png]]

After sensor measurement
![[Pasted image 20250902193644.png]]

Give more weight to the particles which are more likely to represent the sensor reading-

After first measurement
![[Pasted image 20250902193726.png]]

![[Pasted image 20250902193741.png]]

We can resample now according to new distribution. More particles in the likely poses 
![[Pasted image 20250902193836.png]]

Apply same relative motion of the robot to all the particles

![[Pasted image 20250902193925.png]]

![[Pasted image 20250902193953.png]]

Again same
![[Pasted image 20250902194044.png]]

Resampling - we can remove some of the dead particles as we are getting to the real location of the robot, we could still use all the particles but it would slow down the filter.
![[Pasted image 20250902194114.png]]

Again
![[Pasted image 20250902194255.png]]


