
# Module 3 — Link-State Routing & Dijkstra's Algorithm

> **Big Picture:**  
> Routers need to figure out the best path to every destination in a network. Link-State Routing solves this by giving every router a complete map of the network and letting each router independently compute shortest paths using Dijkstra's Algorithm.

---

# Why Link-State Routing?

Imagine Google Maps.

Instead of asking neighbors for directions, every router gets the entire road map:

- Which routers exist
- Which routers are connected
- Cost of each link (delay, bandwidth, admin-defined metric)

Then each router computes the shortest path from itself to all other routers.

---

# Key Terminology

Assume we're computing paths from router **u**.

```
u ----- source router

v ----- any destination router

D(v) -- current best-known cost from u to v

p(v) -- predecessor of v on shortest path

c(u,v) -- direct link cost between u and v

N' ---- nodes whose shortest paths are finalized
```

---

# Mental Model

Think of Dijkstra like this:

```
Known Safe Area (N')

[ u ] ---> confirmed

Unknown Area

[ v ] [ w ] [ x ] [ y ]
```

At every step:

1. Find the closest unknown node.
2. Mark it as confirmed.
3. See if going through it improves paths to others.

Repeat until all nodes are confirmed.

---

# Dijkstra Algorithm Steps

## Step 1: Initialization

Start from source router `u`.

```
N' = {u}
```

For every direct neighbor:

```
D(v) = direct link cost
```

For non-neighbors:

```
D(v) = ∞
```

Example:

```
u --1--> x
u --2--> v
u --5--> w
```

Initial table:

|Node|Cost|
|---|---|
|x|1|
|v|2|
|w|5|
|y|∞|
|z|∞|

---

## Step 2: Pick Closest Unvisited Node

Choose node with smallest cost.

```
x = cost 1
```

Add to N':

```
N' = {u,x}
```

Now check whether going through x gives shorter paths.

Example:

```
u → x → y
1 + 1 = 2
```

If:

```
2 < current D(y)
```

Update:

```
D(y)=2
p(y)=x
```

---

## Step 3: Repeat

Next smallest:

```
y = cost 2
```

Add:

```
N' = {u,x,y}
```

Relax neighbors again.

Maybe:

```
u → x → y → w
1 + 1 + 1 = 3
```

Current:

```
D(w)=5
```

New:

```
D(w)=3
p(w)=y
```

Update it.

---

## Step 4: Continue Until Done

Eventually:

```
N' = {u,x,y,v,w,z}
```

All nodes are finalized.

Now every shortest path is known.

---

# What Does "Relaxing" Mean?

This is the most important concept.

When we discover a new node `w`, we ask:

```
Is it cheaper to reach v through w?
```

Formula:

```
New Cost =Cost(u→w) + Cost(w→v)
```

Then:

```
D(v) =
min(
    current D(v),
    new cost
)
```

This is called **relaxation**.

---

# Example

```
A ---1--- B
|         |
5         2
|         |
C ---1--- D
```

Goal:

```
Shortest path from A
```

Initialization:

```
B = 1
C = 5
D = ∞
```

Choose B:

```
A → B → D = 3
```

Update:

```
D = 3
```

Choose D:

```
A → B → D → C = 4
```

Current:

```
C = 5
```

Update:

```
C = 4
```

Final shortest paths:

```
A→B = 1
A→D = 3
A→C = 4
```

---

# Output of Dijkstra

Dijkstra produces a **Shortest Path Tree (SPT)**.

Example:

```
      A
     / \
    B   C
     \
      D
```

Not every network link appears.

Only links that belong to shortest paths from source A.

---

# How Router Uses This

The router doesn't store entire paths.

It builds a forwarding table:

|Destination|Next Hop|
|---|---|
|B|B|
|C|B|
|D|B|

Meaning:

```
To reach C:send packet to B first
```

The forwarding table stores only the **first hop**.

---

# Complexity

Simple implementation:

```
O(N²)
```

Why?

For every node:

```
Find minimum cost node
```

which requires scanning remaining nodes repeatedly.

```
N + (N-1) + (N-2) + ...≈ N²
```

---

# Real-World Protocol: OSPF

Open Shortest Path First (**OSPF**) is the most common Link-State protocol.

Process:

```
1. Routers flood LSAs
   (Link State Advertisements)

2. Every router learns
   the same topology

3. Every router runs
   Dijkstra locally

4. Builds forwarding table
```

```
LSA Flooding      ↓Common Network Map      ↓Dijkstra      ↓Forwarding Table
```

---

# Link-State vs Distance Vector

|Link-State|Distance Vector|
|---|---|
|Knows full topology|Knows neighbors only|
|Uses Dijkstra|Uses Bellman-Ford|
|Faster convergence|Slower convergence|
|More memory|Less memory|
|OSPF|RIP|

---

# Common Exam Questions

### What does N' contain?

Nodes whose shortest path from source is finalized.

---

### What is D(v)?

Current best-known cost from source to v.

---

### What is p(v)?

Previous node on shortest path.

---

### What is relaxation?

Checking whether a path through a newly discovered node is cheaper.

---

### What does Dijkstra produce?

A shortest-path tree rooted at the source.

---

# Quick Revision (30 Seconds)

```
Link-State Routing:

1. Every router learns entire topology.
2. Represent network as graph.
3. Run Dijkstra from source.
4. Keep:
   D(v) = cost
   p(v) = predecessor
   N' = confirmed nodes
5. Repeatedly:
   - choose closest node
   - add to N'
   - relax neighbors
6. Build forwarding table.
7. OSPF is the real-world example.
```

**Memory Trick:**

```
Dijkstra ="Grow the shortest-path treeone cheapest node at a time."
```