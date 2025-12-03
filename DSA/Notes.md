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



# Graphs - 30/10/25

![[Pasted image 20251030193225.png]]

Tree is a special kind of a graph

![[Pasted image 20251030193917.png]]

Real world analogy
![[Pasted image 20251030194152.png]]

Cities
![[Pasted image 20251030194312.png]]


Directed and Undirected graphs - 
![[Pasted image 20251030194902.png]]

Weighted and unweighted graphs
![[Pasted image 20251030195055.png]]

Cyclic and Acyclic graphs
![[Pasted image 20251030195414.png]]

Connected / Disconnected Graph (Less used in problem solving)
![[Pasted image 20251030201045.png]]

![[Pasted image 20251030202304.png]]


## BFS Traversal - (21/11/2025)

BFS Traversal
![[Pasted image 20251121160159.png]]


BFS Traversal example 2
![[Pasted image 20251122102921.png]]

BFS Example 3
![[Pasted image 20251122103132.png]]

One thing to remember is that BFS traversal can start from anywhere and have multiple solutions, there is no one single correct answer, we can also interchange Agra and Jaipur in the above example.


Depth First Search
![[Pasted image 20251202180156.png]]

Another example
![[Pasted image 20251202180251.png]]


In BFS we use Queue, in DFS we use Stack