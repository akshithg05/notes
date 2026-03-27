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

Plot cost function against the total number of iterations of gradient descent. That is everytime we do a simultaneous update.

![[Pasted image 20260326162546.png]]

It is often difficult to choose a proper value of epsilon. It is better to look for a curve like the curve on LHS.

## Choosing proper learning rate alpha

1. Below image shows when learning rate is too big or there is a possible bug in the code such as updating the parameter (w1) in a wrong way.

![[Pasted image 20260327214158.png]]

But alpha should not be very small as well, it will cause slower convergence

![[Pasted image 20260327215243.png]]

(Next optional lab)