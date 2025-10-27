![[Pasted image 20251025110950.png]]
![[Pasted image 20251025112409.png]]
Chat application - we need messages in real time. It should instantly reach me. Order of messages matters. We need to take care of comm technique to keep communication sane. Some systems like these are real time critical like chat applications.

Eg of not real time criticial - Driver location in Uber/ ola - Its okay to have a delay of 5-10 seconds.
But in chat applications we cant have that delay at all, it should be instant.

But this comes with a cost. we will discuss these in the module.

Another example of critical and not critical systems - In a chat app which automatically sends messages to customers on whatsapp, messages related to transaction or booking need to be immediately sent to the customer.
But some other messages like marketing messages/ offers can be sent slowly, not very critical.

Another critical place - 2 people editing the same file simultaneously. We need time critical operation.

So 2 -3 major things we will cover - 
1. Polling - Eg in cricbuzz, website needs to be updated near real time, on every ball. This uses Websockets. A socket is open between client and server, socket is open always. Even for chat the same principle

But for delivery driver location, we dont need that time criticial, we can fetch the data every 10-15-5 seconds, not thatt critical.

Youtube live chat uses - ? open ended question, I think it uses websocket.

We will cover long polling , short polling , webhooks, server side events and websockets in this section.


## 27 - 10 - 2025

![[Pasted image 20251027065730.png]]

# 🧩 Communication Techniques — System Design

When building a **complex application**, choosing the **right communication technique** is crucial for performance, scalability, and user experience.  

> These are high-level overviews — each topic will be explored in more depth later.

---

## 🗂️ Topics Covered
- Short Polling  
- Long Polling  
- WebSockets  
- Server-Sent Events (SSE)  
- Webhooks  

---

## 🔁 Short Polling
**Concept:**  
The client **repeatedly polls** the backend server at **regular short intervals** to check if new data is available.

**How it works:**
1. Client sends a request every few seconds (e.g., `GET /updates`).
2. Server checks if data is ready.
3. If ready → returns data.  
   If not → returns an empty or “not ready” response.
4. Client repeats the process.

**Use Case:**  
- Simple or low-frequency update systems.  
- When real-time connection isn’t essential.

**Drawback:**  
- Inefficient — generates unnecessary network traffic if updates are infrequent.

---

## ⏳ Long Polling
**Concept:**  
The client sends **one request** and the server **holds it open** until data becomes available.

**How it works:**
1. Client sends a request.
2. Server doesn’t immediately respond — it waits until new data is available.
3. Once ready → server responds with the data.
4. Client immediately sends another request to continue listening.

**Use Case:**  
- Chat applications, notifications, or live data feeds where events are irregular.

**Benefit:**  
- Reduces unnecessary requests compared to short polling.  
- Feels closer to “real-time” without needing persistent connections.

---

## 🔄 WebSockets
**Concept:**  
A **persistent, bi-directional communication channel** between client and server.

**How it works:**
1. Connection starts as HTTP → then upgraded to a WebSocket protocol.  
2. Both client and server can send messages **independently**.  
3. The connection stays open for multiple requests/responses.

**Use Case:**  
- Real-time apps like chats, multiplayer games, live dashboards, or trading platforms.

**Benefit:**  
- Full-duplex communication (both sides can talk simultaneously).  
- Lower latency and overhead compared to repeated HTTP calls.

---

## 📡 Server-Sent Events (SSE)
**Concept:**  
The server can **push updates to the client automatically** — without the client requesting each time.

**How it works:**
1. Client opens a one-way connection (HTTP stream).  
2. Server keeps sending updates as events occur.  
3. Client listens for these “events” and updates the UI.

**Use Case:**  
- Real-time dashboards, notifications, live feeds (e.g., stock prices).

**Benefit:**  
- Lightweight and simple compared to WebSockets for server → client updates.  
- Automatically reconnects if the connection drops.

**Note:**  
- One-way: only **server → client**, not the other way around.

---

## ⚙️ Webhooks
**Concept:**  
An **event-driven callback mechanism** where one server notifies another server when a specific event occurs.

**How it works:**
1. A system (e.g., payment gateway) is configured with a webhook URL.  
2. When an event happens (e.g., “payment successful”), it **POSTs** data to that URL.  
3. The receiving server processes that event.

**Use Case:**  
- Payment confirmations, CI/CD pipeline triggers, notifications between services.

**Difference from APIs:**  
- APIs: client *pulls* data when needed.  
- Webhooks: server *pushes* data when an event happens.

---

## 🧠 Summary Table

| Technique | Communication Type | Connection | Direction | Ideal For |
|------------|--------------------|-------------|-------------|-------------|
| **Short Polling** | Request/Response | Repeated requests | Client → Server | Periodic updates |
| **Long Polling** | Request/Response | Semi-persistent | Server → Client | Chat, notifications |
| **WebSockets** | Persistent | Full-duplex | Both ways | Real-time apps |
| **SSE** | Persistent (one-way) | Server → Client | One-way | Live updates |
| **Webhooks** | Event-driven | On event trigger | Server → Server | Integrations, callbacks |
