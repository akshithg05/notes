## 2.1 Introduction to gradient descent

Used for reducing the cost function to make it minimum cost function.

![[Pasted image 20260312155758.png]]

Not every cost function will have a bowl shaped output, there can be complex functions with more than one minimum value.

Non-squared error cost functions like the one below does not conform to this pattern.

For gradient descent we can choose any starting point, it will take is to some or the other local minima in the function.
![[Pasted image 20260312160715.png]]

## 2.2 Implementing gradient descent

Learning rate controls how much we are descending. Larger alpha more steep step.

![[Pasted image 20260312163948.png]]

Remember to always simultaneously update w and b.

## 2.3 Gradient descent intuition

![[Pasted image 20260312164816.png]]

![[Pasted image 20260312165154.png]]

The derivative is the slope of the graph. In the above example whatever w we choose, the derivative will adjust itself so that we are moving towards minimum cost.

## 2.4 Learning rate (alpha)

1. If alpha is too small, we will take too many steps to reach minimum. Algorithm will be slow and take a lot of time and resources

2. If alpha is too large, then we will overshoot from the minimum, the cost might increase. It will cause a wayward function.
![[Pasted image 20260314171853.png]]


3. When gradient descent is already is at a local minimum and we apply the gradient descent, tangent to the curve at that point is 0. The derivative term is 0 and ***w*** will stay the same value.

Gradient descent leaves a value unchanged if w is already at a local minimum.

![[Pasted image 20260314172138.png]]

Important below
![[Pasted image 20260314172334.png]]


## Putting it all together for the linear regression model with gradient descent.

Full picture
![[Pasted image 20260314173532.png]]

Derivation (basic differentiation)
![[Pasted image 20260314173742.png]]

For a squared error cost function in linear regression, there will be only one global minimum and not multiple local minima. This is an important feature of the squared error cost function. It is a convex function.

![[Pasted image 20260314174419.png]]

### Running gradient descent

1. Initial considerations
![[Pasted image 20260314174557.png]]

2. Gradient descent in action
![[Pasted image 20260314174700.png]]

Batch linear regression
![[Pasted image 20260314174840.png]]




