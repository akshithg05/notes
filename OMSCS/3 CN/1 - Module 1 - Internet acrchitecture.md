
# OMSCS 6250 — Module 1 — Internet Architecture & Design Principles

Based on:
- Lecture slides
- Video transcript

---

# 1. Big Picture — Why This Module Matters

The Internet grew from:
- a small research network
→ into
- a massive global infrastructure.

The challenge:
- billions of users
- billions of devices
- heterogeneous technologies
- real-time applications
- scalability
- low latency
- security

The Internet works because of architectural design choices.

Core themes:
- Layering
- Encapsulation
- End-to-End Principle
- Hourglass Architecture
- Network Devices
- Learning Bridges
- Spanning Tree Protocol

---

# 2. Why Layering Exists

## Problem
Applications must work across:
- WiFi
- Ethernet
- 5G
- Optical Fiber
- Satellite
- etc.

without caring about underlying hardware.

---

## Solution → Layered Architecture

Each layer:
- uses services from layer below
- provides services to layer above

Benefits:
- modularity
- scalability
- interoperability
- evolvability

---

# Mental Model

Think of networking layers like software abstraction layers.

Example:

```text
React App
↓
HTTP API
↓
TCP
↓
IP
↓
Ethernet/WiFi
↓
Physical cable/radio
```

Your browser doesn’t care whether packets travel via:
- WiFi
- Ethernet
- Fiber

because abstraction hides complexity.

---

# 3. Internet Protocol Stack

## 5 Layers

| Layer | Responsibility | Example |
|---|---|---|
| Application | User-facing protocols | HTTP, DNS |
| Transport | End-to-end communication | TCP, UDP |
| Network | Addressing + routing | IP |
| Link | Local delivery | Ethernet |
| Physical | Transmitting bits | Fiber, radio |

---

# Important Understanding

## TCP vs IP

### TCP
Handles:
- reliability
- ordering
- retransmissions

### IP
Handles:
- addressing
- forwarding packets between networks

---

# 4. Encapsulation

Data moves DOWN layers at sender:

```text
HTTP Message
↓
TCP Segment
↓
IP Datagram
↓
Ethernet Frame
↓
Bits
```

At receiver:
- reverse process happens
- called de-encapsulation

---

# Mental Model

Like shipping a package:

| Layer | Analogy |
|---|---|
| Application | Letter |
| TCP | Adds tracking |
| IP | Adds destination address |
| Link | Local delivery truck |
| Physical | Actual road/wires |

---

# 5. End-to-End Principle (VERY IMPORTANT)

Core Internet philosophy:

> Keep the network core simple.
> Put intelligence at endpoints.

---

# Meaning

The network itself should NOT:
- understand applications deeply
- guarantee application semantics

Instead:
- endpoints handle reliability/security/etc.

---

# Why?

Different apps need different behavior.

| Application | Priority |
|---|---|
| Video call | Low latency |
| File transfer | Reliability |
| Gaming | Fast response |
| Streaming | Continuous flow |

A “smart network core” would limit flexibility.

---

# Real Engineering Insight

This idea is VERY important in:
- cloud systems
- distributed systems
- microservices
- API design
- Kubernetes networking

The Internet succeeded because:
- the middle stayed generic
- innovation happened at edges

---

# 6. Violations of End-to-End Principle

Real networks violate it using:
- NAT
- Firewalls
- Proxies
- Middleboxes

---

# NAT (Network address translation) (Important)

## Why NAT Exists
IPv4 addresses are limited.

NAT allows:

```text
Many private devices
↓
share one public IP
```

---

# What NAT Does

It rewrites:
- source IP
- source port

and maintains:

```text
(public IP, port) ↔ (private IP, port)
```

mapping table.

Out of the roughly 4.3 billion total IPv4 addresses that exist, the vast majority are designated as **public** addresses, but a specific subset is legally reserved for **private** use only.

Because billions of people use multiple internet-connected devices today, we would have run out of public IPv4 addresses decades ago without NAT.

The Core Solution: Public vs. Private IPs

- **The Private Pool:** IP addresses starting with `192.168.x.x`, `10.x.x.x`, or `172.16.x.x` through `172.31.x.x` are private. They are completely invisible to the internet.
- **The Recycling Trick:** Because private IPs are invisible globally, **every single home and business in the world can reuse the exact same private numbers** inside their own walls. Your router uses `192.168.1.1`, and your neighbor's router uses `192.168.1.1` at the exact same time.
- **The NAT Funnel:** NAT acts as a bottleneck translator. It takes thousands of these "recycled" private devices and funnels all their traffic through just **one** unique, paid public IPv4 address assigned by your Internet Service Provider (ISP).

An Easy Analogy: An Apartment Building

Think of a massive corporate building or apartment complex:

- **Without NAT:** Every single desk phone in the entire building needs its own unique, 10-digit public phone number. The telephone company would run out of numbers instantly.
- **With NAT:** The entire building has just **one main public phone number** (the Public IP). Inside the building, every desk has a 3-digit extension like x101, x102, or x103 (the Private IPs). When you call out, the main system handles the routing. Another building down the street can reuse those exact same extensions (x101, x102) without any conflict.
---

# Important Tradeoff

## Benefit
- solves IPv4 scarcity

## Downside
- breaks original end-to-end connectivity

---

# 7. Hourglass Architecture

One of the MOST IMPORTANT concepts in networking.

---

# Structure

```text
Many Applications
        ↑
Few Core Protocols
(TCP/IP/UDP)
        ↓
Many Link Technologies
```

---

# Why It Happens

Protocols survive when:
- many systems depend on them

This creates:
- network effects
- ecosystem lock-in
- ossification

---

# Ossification

Meaning:

> Core protocols become extremely hard to replace.

Even if better protocols exist.

---

# Why TCP/IP Won

Not necessarily because:
- technically perfect

But because:
- adoption snowballed early

Once many apps depend on it:
- replacing it becomes nearly impossible.

---

# VERY Important Systems Insight

This exact pattern appears in:
- Linux
- Kubernetes
- React
- Docker
- Cloud APIs
- Databases

Winner ecosystems become:
- entrenched
- difficult to replace

---

# 8. Interconnecting Devices

## Layer 1 → Hubs/Repeaters

- forwards bits blindly
- no intelligence
- floods everywhere

---

## Layer 2 → Bridges/Switches

Uses:
- MAC addresses

Forwards:
- frames intelligently

---

## Layer 3 → Routers

Uses:
- IP addresses

Forwards:
- packets between networks

---

# Key Difference

| Device | Uses |
|---|---|
| Hub | Bits |
| Switch | MAC addresses |
| Router | IP addresses |

---

# 9. Learning Bridges

Switches “learn” MAC locations dynamically.

They build:

```text
MAC Address → Port
```

table.

---

# Learning Process

When switch receives frame:
1. Observe source MAC
2. Record incoming port
3. Use table later for forwarding

---

# If Destination Unknown

Switch:
- floods frame everywhere except incoming port

Once reply comes:
- switch learns correct location

---

# 10. Spanning Tree Protocol (STP)

## Problem

Redundant links create loops.

Layer 2 frames:
- DO NOT have TTL/hop limit

Result:
- infinite circulation
- broadcast storms
- network collapse

---

# Solution → Spanning Tree

STP:
- disables selected links
- creates loop-free topology

---

# How It Works

Switches:
- exchange messages
- elect root bridge
- compute best paths
- disable unnecessary ports

Result:

```text
Connected network
WITHOUT loops
```

---
# Spanning Tree Protocol (STP)

## Problem
Redundant links between switches create loops.

Example:
```text
A --- B
|     |
|     |
C --- D
```

At Layer 2, Ethernet frames:
- do NOT have TTL/hop limit
- can circulate forever

This causes:
- broadcast storms
- duplicate frames
- MAC table instability
- network congestion/collapse

---

# Goal of STP

Convert a network graph with cycles into a:

```text
loop-free spanning tree
```

while still:
- keeping all switches connected
- preserving redundancy for failover

---

# High-Level Working

## 1. Root Election
Initially every switch assumes:
```text
"I am the root."
```

Switches exchange messages.

Eventually:
- switch with lowest bridge ID becomes root

---

## 2. Best Path Selection
Each switch determines:
```text
shortest path to root
```

---

## 3. Loop Prevention
Ports/links that create cycles are:
```text
logically disabled
```

Result:
- only one active loop-free path remains

---

# Important Notes

- STP is a distributed algorithm
- No central controller exists
- Switches converge using local message exchange
- Physical links still exist; some are just blocked logically

---

# Mental Model

STP keeps enough roads open so every city is reachable, but closes extra roads that would cause traffic to loop forever.

---

# Key Exam Points

- Why loops are dangerous
- Why redundancy exists
- What is a spanning tree
- Root election concept
- Distributed convergence idea
- Why some ports are disabled
# Most Important Exam Concepts

Focus heavily on:
- layering
- encapsulation
- end-to-end principle
- NAT
- hourglass architecture
- ossification
- switches vs routers
- learning bridges
- spanning tree loops

---

# High-Level Mental Model of Entire Module

## Internet succeeds because:

### 1. Abstraction
(layering)

### 2. Simplicity in core
(end-to-end principle)

### 3. Stable middle
(hourglass architecture)

### 4. Smart forwarding
(switches/routers)

### 5. Loop prevention
(STP)

---

# Things Worth Memorizing

## Encapsulation order

```text
Application
→ Transport
→ Network
→ Link
→ Physical
```

---

## Device layers

```text
Hub → Layer 1
Switch → Layer 2
Router → Layer 3
```

---

## End-to-End Principle

> Intelligence at edges, simple network core.

---

# Practical Engineering Connection

Modern cloud/datacenter networking still uses:
- layering
- encapsulation
- switching
- routing
- NAT
- STP concepts

These are foundational to:
- Kubernetes networking
- service meshes
- SDN
- cloud infrastructure
- load balancers
- observability systems

---

# Revision Strategy

Before assignments/exams:
1. Understand packet journey
2. Understand which layer handles what
3. Understand why abstraction matters
4. Understand why loops are dangerous
5. Understand why protocols become entrenched

---

# One-Sentence Summary of Module 1

The Internet scales because it uses layered abstractions, keeps the core simple, and relies on a small stable set of protocols while intelligent devices efficiently forward traffic and prevent loops.

