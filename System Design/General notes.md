**Scaling** refers to the ability of a system (app, backend, database, frontend) to **handle increasing load** — such as more users, requests, or data — **without degrading performance**.
### ✅ **Types of Scaling**

#### 1. **Vertical Scaling (Scaling Up)**:

- Add **more resources to a single machine** (e.g., CPU, RAM).
- Simpler but has a limit (there’s only so much you can add to one server).
✅ Use Case: Quick performance boost for smaller apps.
#### 2. **Horizontal Scaling (Scaling Out)**:

- Add **more machines/instances** to distribute load.
- Enables handling massive traffic.
✅ Use Case: Distributed systems, microservices, cloud-native apps.

## Availability vs Reliability vs Durability

| Concept          | Definition                                                                         | Focuses On                     | Real-World Analogy                                                    |
| ---------------- | ---------------------------------------------------------------------------------- | ------------------------------ | --------------------------------------------------------------------- |
| **Availability** | The percentage of time a system is up and accessible to users during a time window | **Uptime** / being accessible  | "Is the store open when I try to visit?"                              |
| **Reliability**  | The system's ability to function **correctly and consistently** over time          | **Correct behavior** over time | "Does the store deliver the right product every time?"                |
| **Durability**   | The assurance that once data is written, it won't be lost or corrupted             | **Data persistence**           | "If I store something in a vault, will it still be there in 5 years?" |

- **Redundancy reduces the chance of total failure**  
    → because if one component fails, another takes over (failover).

- This improves **Reliability**  
    → system continues to operate **without interruption or failure**.

- Higher Reliability leads to better **Availability**  
    → because the system is less likely to be down or unresponsive.

### 🧠 Interview-Ready Line:

 _"Redundancy improves reliability by minimizing single points of failure. A more reliable system is less likely to experience downtime, which directly contributes to higher availability."_