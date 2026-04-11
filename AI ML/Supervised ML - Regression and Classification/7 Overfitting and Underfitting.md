Lets go back to the housing problem example. Linear regression example.

![[Pasted image 20260411162453.png]]

## 2. Underfitting , overfitting for classification

![[Pasted image 20260411162739.png]]


## 3. Addressing overfitting

1. Collect more training data - 
But this is not always an option. Maybe there is no more data at all.
![[Pasted image 20260411162939.png]]

2. Maybe cut some features - Reduce features

Use intuition maybe to select features. But sometimes all features might be useful, we cannot discard features.

![[Pasted image 20260411163200.png]]

3. Regularization

Gently reduce the weight of the feature, shrink the value of the parameter instead of fully setting it to 0. Use smaller parameter values to smoothen the curve instead of strict curve.

We generally regularize w1.... wn. Might not make a big difference to reduce the value of b.![[Pasted image 20260411163356.png]]

### Summary

