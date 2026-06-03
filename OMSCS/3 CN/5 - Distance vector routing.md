
# Distance Vector Routing (DV)

> **Big Picture:**  
> Unlike Link-State Routing, where every router knows the entire network topology, Distance Vector Routing works by having routers talk only to their immediate neighbors. Each router gradually learns the best routes through repeated exchanges of routing information.

---

# Why Do We Need Distance Vector Routing?

Imagine you're trying to reach a destination city.

Instead of having a complete map, you ask your neighbors:

```
"How far is the destination from you?"
```

Each neighbor replies with its current best distance.

You then choose the neighbor that gives the cheapest total route.

This is exactly how Distance Vector Routing works.

---

# Main Characteristics

The Distance Vector algorithm is:

### 1. Iterative

Routers repeatedly exchange routing information until no router has new updates to send.

---

### 2. Asynchronous

Routers do not need to update at the same time.

Each router sends updates whenever its routing table changes.

---

### 3. Distributed

There is no central controller.

Each router performs its own calculations using information received from neighbors.

---

# Key Terminology

Assume we are router **X**.

```
Dx(y)
```

= X's current least-cost estimate to destination Y

---

```
c(x,v)
```

= Direct cost from X to neighbor V

---

```
Dv(y)
```

= Neighbor V's advertised cost to reach destination Y

---

# The Bellman-Ford Equation

![[Pasted image 20260603183123.png]]

---

# Understanding the Formula

Suppose:

```
X -----2----- Y -----1----- Z
X -----7----- Z
```

Current link costs:

```
X → Y = 2
Y → Z = 1
X → Z = 7
```

---

Goal:

```
Find shortest path from X to Z
```

Option 1:

```
Direct path
X → Z
Cost = 7
```

Option 2:

```
Through Y
X → Y → Z
Cost = 2 + 1 = 3
```

Take the minimum:

```
Dx(Z) = min(7,3) = 3
```

Therefore:

```
X reaches Z via Y
Cost = 3
```

This example appears in the module notes.

---

# What Is a Distance Vector?

Each router maintains a table.

Example for Router X:

|Destination|Cost|
|---|---|
|X|0|
|Y|2|
|Z|7|

Initially, X only knows costs to directly connected neighbors.

---

# Distance Vector Update Process

## Step 1: Exchange Distance Vectors

Each router sends its table to neighbors.

Example:

```
Y tells X:

Cost to X = 2
Cost to Y = 0
Cost to Z = 1
```

---

## Step 2: Recompute Costs

Router X receives Y's vector.

For destination Z:

```
Cost via Y
=
Cost(X→Y)
+
Cost(Y→Z)

=
2 + 1

=
3
```

Compare:

```
Current cost = 7
New cost = 3
```

Since 3 is better:

```
Update table
```

---

## Step 3: Advertise New Information

Because X found a better route:

```
X updates its table
```

and sends the new vector to neighbors.

Information spreads hop-by-hop through the network.

---

## Step 4: Convergence

Eventually no router discovers better routes.

At this point:

```
No updates are sent
```

The network is said to have **converged**.

---

# Example Walkthrough

Initial topology:

```
      2
   X-----Y
    \    |
   7 \   | 1
      \  |
        Z
```

Initial tables:

### Router X

|Dest|Cost|
|---|---|
|X|0|
|Y|2|
|Z|7|

---

### Router Y

|Dest|Cost|
|---|---|
|X|2|
|Y|0|
|Z|1|

---

### Router Z

|Dest|Cost|
|---|---|
|X|7|
|Y|1|
|Z|0|

---

After exchange:

X learns:

```
Route to Z through Y
2 + 1 = 3
```

Updated table:

|Dest|Cost|
|---|---|
|X|0|
|Y|2|
|Z|3|

Network converges to:

```
X → Z via Y
Cost = 3
```

instead of the direct cost of 7.

---

# Link-State vs Distance Vector

|Link-State|Distance Vector|
|---|---|
|Knows full topology|Knows neighbors only|
|Uses Dijkstra|Uses Bellman-Ford|
|Floods topology information|Exchanges distance vectors|
|Faster convergence|Slower convergence|
|OSPF|RIP|

---

# The Count-to-Infinity Problem

Distance Vector has a major weakness.

Suppose a link fails.

Bad news travels slowly.

Example:

```
Y thinks:"I can reach X through Z"
Z thinks:"I can reach X through Y"
```

Neither realizes the route is broken.

They keep increasing costs:

```
678910...∞
```

This is called the **Count-to-Infinity Problem**.

---

# Poison Reverse

A common fix is Poison Reverse.

Rule:

```
If I reach destination X through neighbor Y,I tell Y that my distance to X is ∞.
```

Essentially:

```
"Don't use me to reach X."
```

This prevents simple two-router loops and speeds up convergence.

---

# Real-World Protocol

The classic Distance Vector protocol is:

- RIP (Routing Information Protocol)

It periodically exchanges routing tables with neighbors and applies the Bellman-Ford equation to compute least-cost paths.

---

# Quick Revision (30 Seconds)

```
Distance Vector Routing:

1. Every router stores a distance vector.
2. Routers exchange vectors only with neighbors.
3. Uses Bellman-Ford:

   Dx(y) = min{c(x,v) + Dv(y)}

4. Update routing table if a cheaper path is found.
5. Advertise updated vector.
6. Repeat until no more updates.
7. Network converges.
8. Main problem:
   Count-to-Infinity.
9. Common fix:
   Poison Reverse.
```

### Memory Trick

```
Link-State:"I know the whole map.
"Distance Vector:"I only know what my neighbors tell me."
```

That's the fundamental difference between the two routing approaches.