![[Pasted image 20251028064245.png]]
# 🔁 Short Polling — In Detail

## 🧩 Overview

**Short polling** is a communication technique where the **client repeatedly sends requests** to the server at **regular intervals** (e.g., every 5 or 10 seconds) to check for new data or updates.

It’s often used when a client wants to stay somewhat updated in near-real-time, but a **persistent connection** (like WebSocket) is unnecessary or too resource-intensive.

---
## ⚙️ How It Works

1. The **client** sends a request to the **server** asking if any new data or events are available.
2. The **server** immediately responds — either with the latest data or with a message indicating no new updates.
3. The **client** waits for a short period (e.g., 5 seconds) and sends another request.
4. This cycle repeats continuously.

---
## 🧠 Key Characteristics

- **Short-lived connections:**  
    Each request–response cycle is independent; the connection closes after each response.
- **No persistence:**  
    There is **no long-standing or streaming connection** between client and server.
- **Polling interval-based:**  
    The frequency of requests (e.g., every 5s, 10s) determines how "real-time" the data appears.
- **Immediate server response:**  
    The server **does not wait** for new data to arrive — it responds right away with whatever it has (possibly stale data).
---
## 📊 Example

Example use case:  
A notification system that checks the server every few seconds to see if new notifications are available.

Client → Server: "Do you have new notifications?"  
Server → Client: "No new updates."  
(wait 5 seconds)  
Client → Server: "Do you have new notifications?"  
Server → Client: "Yes, 2 new messages."

---

## ⚡ Advantages

- ✅ **Simple to implement:** Works with standard HTTP protocols.
- ✅ **No persistent connections:** Reduces connection management complexity.
- ✅ **Lower server memory usage:** Connections are short-lived.

---
## ⚠️ Limitations

- ❌ **High server load under scale:**  
    With many clients polling frequently, the number of requests per second can overwhelm the server.
- ❌ **Inefficient network usage:**  
    Many requests may return “no new data,” wasting bandwidth.
- ❌ **Not truly real-time:**  
    Data freshness depends on the polling interval — shorter intervals improve responsiveness but increase server strain.

---

## 🧮 Example Scenario

If **10,000 users** poll the server every **5 seconds**, the server must handle:  
10,000 users × (1 request / 5s) = **2,000 requests per second**

Even if only a few have updates, all 10,000 requests still reach the server.

---

## 🧭 Summary

|Property|Description|
|---|---|
|**Connection Type**|Short-lived HTTP requests|
|**Direction**|Client → Server|
|**Response Behavior**|Immediate (may contain stale data)|
|**Use Case**|Lightweight, periodic updates|
|**Limitation**|Scalability issues with large user bases|

---

## 🧩 When to Use

Use **short polling** when:
- You need _semi-real-time_ updates but not true streaming.
- Your user base is small or polling frequency is low.
- You want a simple setup without persistent connections.

# 📊 Example — Cricbuzz

A platform like **Cricbuzz** uses **short polling** for score updates:

- The client polls the server every few seconds to check if a new score or event (e.g., wicket, boundary) is available.  
- The server may respond with the **cached version** of data if there is no change.  
- **Cache validation** can be performed based on **version numbers** or **timestamps** to ensure only updated scores are sent.

## Example Flow

**Client → Server:** “Do you have an updated score?”  
**Server → Client:** “Version 14, no change.”  

*(wait 5 seconds)*  

**Client → Server:** “Do you have an updated score?”  
**Server → Client:** “Version 15, score updated to 145/3.”  

# ⚙️ Clearing Intervals in Short Polling

When implementing **short polling**, developers often use `setInterval()` to repeatedly call the server at fixed intervals.

However, it’s **crucial** to clear this interval once the target condition is met or the user navigates away from the page.

Example:
```javascript
// Start polling every 5 seconds
const intervalId = setInterval(fetchData, 5000);

// On navigation, user action, or target condition
clearInterval(intervalId);

```

## ❗ Why It’s Important

- **Prevents memory leaks:**  
    If the interval is never cleared, it continues running even when the component or page is no longer active.
- **Avoids redundant API calls:**  
    Without clearing, the server continues receiving requests unnecessarily, wasting bandwidth and backend resources.
- **Improves performance:**  
    Reduces CPU/network usage on the client and request load on the server.
- **Ensures proper cleanup in React:**  
    In frameworks like React, you should clear the interval in the `useEffect` cleanup function:

If you don’t clear the `setInterval` when leaving or re-entering a page/component, **a new interval is created each time** the code runs again. The old one keeps running in the background, so over time:
- Multiple intervals pile up.
- Each keeps executing its callback at the defined interval.
- The browser ends up doing duplicate work, increasing CPU usage and memory consumption.
- Eventually, the page becomes **laggy or unresponsive** — especially if the callback involves DOM updates or network calls.

In React, for example, this commonly happens if you set up `setInterval` inside a component without cleaning it up in the `useEffect` return function:
![[Pasted image 20251029193527.png]]

So yes — always clear your intervals when you leave the page, unmount a component, or when the condition for running it is no longer valid. Otherwise, you’ll create a “leak” of intervals that keeps multiplying in the background.

