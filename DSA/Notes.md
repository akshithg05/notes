![[Pasted image 20250804192259.png]]![[Pasted image 20250804192334.png]]

Priority Queue
![[Pasted image 20250805195123.png]]



## Dynamic Programming
![[Pasted image 20250925141903.png]]

![[Pasted image 20250925144418.png]]
![[Pasted image 20250925150628.png]]


Fibonacci Numbers problem using recursion
![[Pasted image 20250925151605.png]]
Above program time complexity - O(2^n)

We are computing the same problem again and again. When we compute the same problem again and again, we call these problems as overlapping subproblems.

When we solve all the smaller subproblems, finally all the subproblems will lead to the final problem. This is known as optimal substructure.

When we have these 2 conditions met, it is a very goof candidate for Dynamic Programming.
Now we need to see how do we apply DP to this ?
![[Pasted image 20250925152034.png]]

![[Pasted image 20250925153443.png]]
By introducing memoization we reduced the time complexity of the solution from O(2^n) to O(n).
There is a small addition in space complexity, but that will not matter because recursion also occupies O(n) space in the call stack depth.

Fun facts -
![[Pasted image 20250925153850.png]]

IN DP the solution of one problem will be required by another subproblem and this pattern will help us identify that this is DP
And most DP qs are variations of similar problems.

## 26/09/2025

![[Pasted image 20250926112512.png]]

Recursion vs Iteration
![[Pasted image 20250926123045.png]]


