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

