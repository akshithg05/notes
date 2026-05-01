
## 1. Multiple linear regression

![[Pasted image 20260316232354.png]]

Arrow is to show vector and not number

Example - 
![[Pasted image 20260316232650.png]]

If we consider 80K as house price, then for every 1000 sqF we multiply by 0.1 times , for every bedroom we add multiply by 4 times, for every floor price increases 10 times and every year decreases by twice the value.

This is called **MULTIPLE Linear Regression**
![[Pasted image 20260316233315.png]]

We use vectorization to implement this.

[[2026-03-17]]

## 2. Vectorization part 1

![[Pasted image 20260317230613.png]]

Vectorization is better - 
1. code is cleaner
2. numpy uses parallel hardware so it is faster to run than using a loop to run in O(n). It is more efficient to use dot product.

[[2026-03-18]]
##### Why vectorization is faster ?

![[Pasted image 20260318205011.png]]

Gradient descent 
![[Pasted image 20260318205451.png]]


[[2026-03-19]]

## Gradient descent for multiple linear regression

![[Pasted image 20260319210538.png]]

An alternative to gradient descent
![[Pasted image 20260319210722.png]]
 We will use gradient descent mostly 

