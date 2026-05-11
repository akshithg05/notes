![[namastedev.com_learn_namaste-dsa_introduction-to-graphs.png]]

![[namastedev.com_learn_namaste-dsa_introduction-to-graphs 1.png]]


Example of graph
1. Graph is a broad data structure.
2. Tree is a special kind of graph.
3. Degree - Number of edges connecting from a node is degree. Degree of 3 - 4

4. Path - Way of going from one node to another node in a graph is called path. There can be multiple paths for going from one node to another node. There can be no path as well.

Node without edges also is a graph.

5. Cycle - Start from a node and reach back the same node.
![[namastedev.com_learn_namaste-dsa_introduction-to-graphs 2.png]]

### Real world analogy

![[namastedev.com_learn_namaste-dsa_introduction-to-graphs 3.png]]

Degree of B - 3, 3 friends;
1st Degree connections of A - B
2nd Degree connections of A  - C and D
3rd Degree connections of A - G and E

Another example - 
![[namastedev.com_learn_namaste-dsa_introduction-to-graphs 4.png]]

#### Nodes are represented by - Value and Edges.

Value of node can be anything - strings, numbers , etc.

## Types of Graphs classification
## 1. Undirected and Directed Graph (Digraph)

Directed graph - Edges have a direction
Shows relationship between entities in one direction.

![[namastedev.com_learn_namaste-dsa_introduction-to-graphs 6.png]]

Directed graphs have one way relationship between nodes/ vertices.
Example - A follows B . but B does not follow A - one way rel.
1. Indegree - Inward edges in a node of a graph.
2. Outdegree - outward edges in a node of a graph.


## 2. Weighted and Unweighted graphs

Weight can be - Cost, time, distance price, weight

![[namastedev.com_learn_namaste-dsa_introduction-to-graphs 7.png]]


## 3. Cyclic and Acyclic graphs

Cyclic graphs have a cycle in them as shown in the image below. 

We can have a combination of direction as well as Acyclic graphs as shown in the bottom of the image.

![[namastedev.com_learn_namaste-dsa_introduction-to-graphs 8.png]]

Example of Acyclic graphs - NPM packages, version control in 

**Trees are special type of acyclic graphs** representing hierarchical data.
## 4. Connected / Disconnected Graph (Less used in problem solving)
![[Pasted image 20251030201045.png]]


## Summary
![[Pasted image 20260422203459.png]]

[[2026-04-23]]

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


[[2026-05-11]]

## Topological sort

![[namastedev.com_learn_namaste-dsa_topological-sort-dfs.png]]

Here in the above example both the lists in the bottom are valid answers, and satisfy the definition of a linear order of nodes where u comes before v.

### Why do we do topological sort -

1. If the above graph represents npm packages, every node represents a dependency and what order they must be installed. In cases where we need to linearly install packages, this sort is useful.

2. Perquisites representation

There are 2 approaches to do this , DFS and BFS approach.
BFS Algorithm - Kahn's Algorithm

#### DFS method 

![[namastedev.com_learn_namaste-dsa_topological-sort-dfs 2.png]]

Doing this intuitively - Build solution bottom up in reverse order

