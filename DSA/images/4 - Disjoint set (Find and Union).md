
![[namastedev.com_learn_namaste-dsa_disjoint-set-union-find (1).png]]

Suppose we want to create a new edge B to D. We need to find which set B and D exists first.
Find operation is done to find which set these exist in.

After find we do union and B and D is joined

![[namastedev.com_learn_namaste-dsa_disjoint-set-union-find (1) 1.png]]

If 2 nodes are on the same set then we do not need a union in that case

If I want to create an edge from D to F. D -> S4, F -> s3

These 2 will be unioned

![[namastedev.com_learn_namaste-dsa_disjoint-set-union-find (2).png]]

If we want to find cycles in a graph, find and union are very very very helpful for these operations

## How to detect cycle using find and union operations

Take edges one by one and explore the graph.
Initially assume every node is a different set (disjoint sets, initially)

Rank - number of nodes in set.

Set which has greater rank gets the node. Lower rank set gets attached to greater rank set.

![[namastedev.com_learn_namaste-dsa_disjoint-set-union-find (2) 1.png]]

All this can be achieved using linked likst as shown above
We can do the same thing using arrays as well.

![[namastedev.com_learn_namaste-dsa_disjoint-set-union-find (2) 2.png]]


