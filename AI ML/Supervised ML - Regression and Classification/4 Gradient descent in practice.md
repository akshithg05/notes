## 1. Feature scaling 

If feature values are large, parameter values can be small. If features are large, the parameters can be relatively large.

![[Pasted image 20260326120718.png]]

If we follow the first case, then a small change in w1, causes a large change in the Cost J

![[Pasted image 20260326120930.png]]

![[Pasted image 20260326154550.png]]

WHen we have diff features with diff ranges of values , we need to rescale to speed up gradient descent.

## 2. Feature scaling methods

### 2.1 Basic scaling

![[Pasted image 20260326161016.png]]

Above shows dividing by the largest value

### 2.2 Mean normalization

![[Pasted image 20260326161419.png]]

### 2.3 Z score normalization
![[Pasted image 20260326161628.png]]

### General rule of thumb for scaling

![[Pasted image 20260326161845.png]]

## 3. Checking gradient descent convergence

PLot cost function against the total number of iterations of gradient descent. That is everytime we do a simultaneous update.

![[Pasted image 20260326162546.png]]

It is often difficult to choose a proper value of epsilon. It is better to look for a curve like the curve on LHS.