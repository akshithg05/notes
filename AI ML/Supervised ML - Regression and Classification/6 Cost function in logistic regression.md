![[Pasted image 20260407212555.png]]

Squared error cost function for linear regression
For logistic regression, we cannot use the same squared error cost function because it will give a non-linear graph. This ,means we will get multiple local minima and we will not always get the best value of minimum cost as shown below.

![[Pasted image 20260407212818.png]]

## Loss function when output label (y) = 1

![[Pasted image 20260407213515.png]]

## Loss function when output label (y) = 0
![[Pasted image 20260407213851.png]]

To put into perspective - For a given array of x, if our model predicts that malignancy is 99.99%, but the true output value (y) for that given x is 0 (benign), then the loss is very high. That is we penalize the model for predicting wrong results.

## Summary 
![[Pasted image 20260407214153.png]]



[[2026-04-08]]

## Simplified loss function

![[Pasted image 20260408222429.png]]

Simplified cost function 
![[Pasted image 20260408222602.png]]

[[2026-04-09]]

## Summary -

![[Pasted image 20260409125746.png]]

## Minimizing cost function using Gradient Descent

![[Pasted image 20260409140741.png]]

Summary of gradient descent

![[Pasted image 20260409141025.png]]

