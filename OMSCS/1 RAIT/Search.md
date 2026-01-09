Motion planning - 
A robot wants to get from a particular starting position to a particular end goal-
![[Pasted image 20250908175853.png]]

The same problem occurs in a self driving car as well.
![[Pasted image 20250908175936.png]]

In a complicated city environment as shown below, the car can have two ways to reach its target-
![[Pasted image 20250908180056.png]]
One being the red arrows, other being the black arrows.
The goal of the problem is -
![[Pasted image 20250908180223.png]]

## Computing Cost - Breadth First Search

Question 1 -
![[Pasted image 20250908180500.png]]

Answer is 7 because -
![[Pasted image 20250908180600.png]]

Question 2
![[Pasted image 20250908180737.png]]

Question 3
![[Pasted image 20250908181015.png]]

Even if we go around the blocks and come to the correct location it will take a higher cost to reach the final goal location.

Question 4
![[Pasted image 20250908181408.png]]

Question 5
![[Pasted image 20250908181622.png]]

Question 6
![[Pasted image 20250908181925.png]]

A* Algorithm - Heuristic function 

![[Pasted image 20250910164102.png]]

Here we have additional information called a heuristic function. The main difference here is we will chose the node expanding with the minimum heuristic values.
This will make sure we do not have to explore other paths, directly we can explore the shortest path.
![[Pasted image 20250910164919.png]]

## Dynamic Programming -

You dont need a plan just for the most optimal solution but need to have a plan for other paths and solutions as well, This is because the real world is not always ideal, there are lot of obstacles, people and barriers.
![[Pasted image 20250910202410.png]]

this will not involve A* algorithm, but another approach - 
![[Pasted image 20250910202552.png]]

Value function -
![[Pasted image 20250910202914.png]]


Question 7
![[Pasted image 20250910211341.png]]

Question 8
![[Pasted image 20250910211511.png]]

