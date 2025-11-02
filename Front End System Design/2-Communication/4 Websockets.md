![[Pasted image 20251031192037.png]]

# 🧠 WebSockets — Notes

## 🔹 Overview
- **WebSockets** provide a **full-duplex communication mechanism**, meaning **both client and server can send and receive data simultaneously**.  
- It uses a **single, long-lived TCP connection** instead of opening a new connection for each request (as in HTTP).  
- Enables **continuous, real-time, bidirectional communication** — there’s **no need to wait** for a request-response cycle.  

## ⚙️ How WebSockets Work
1. **Handshake Phase**  
   - The communication starts as a **regular HTTP request**.  
   - The **client sends an HTTP Upgrade request** asking the server to switch from HTTP to the WebSocket protocol.  
     ```
     GET /chat HTTP/1.1
     Host: example.com
     Upgrade: websocket
     Connection: Upgrade
     Sec-WebSocket-Key: x3JJHMbDL1EzLkh9GBhXDw==
     Sec-WebSocket-Version: 13
     ```
2. **Server Response**  
   - The **server acknowledges the request** and agrees to upgrade the protocol by sending a `101 Switching Protocols` response:  
     ```
     HTTP/1.1 101 Switching Protocols
     Upgrade: websocket
     Connection: Upgrade
     Sec-WebSocket-Accept: HSmrc0sMlYUkAGmm5OPpG2HaGWk=
     ```
3. **Full-Duplex Communication**  
   - After the handshake, the **TCP connection remains open**.  
   - Both client and server can now **send and receive messages** anytime — no request required.  
   - The data exchanged is in the form of **frames** (binary or text).  
4. **Connection Closure**  
   - Either the client or the server can **terminate the connection**.  
   - The other party acknowledges the close frame, and the TCP connection ends gracefully.  

## 🧩 Key Features
- Persistent, low-latency communication channel.  
- Ideal for **real-time applications** (e.g., chat apps, live dashboards, online gaming).  
- Uses **ws://** or **wss://** (for secure WebSockets over TLS).


Example - Go through the code

Below is an image of the WS connection being created - type (status code - 101)
![[Pasted image 20251102150926.png]]

Web socket connection message section under network tab
![[Pasted image 20251102151033.png]]

## 🧩 Uses of WebSocket Connections
- **Online analytics and trading dashboards** – enable real-time updates and live data feeds.  
- **Collaborative documents** – allow multiple users to edit and view changes simultaneously.  
- **Online games** – support fast, bidirectional communication for real-time gameplay.  

## 🌐 Protocols
- Similar to **HTTP and HTTPS**, WebSockets use **WS** and **WSS** protocols.  
  - `ws://` → standard WebSocket connection (non-secure).  
  - `wss://` → secure WebSocket connection (over TLS/SSL).  

## ⚙️ Data Framing Principle
- WebSockets work on a **data framing mechanism**.  
  - **Small messages** are sent directly as a single frame.  
  - **Large messages** are **split into smaller chunks (frames)** and sent sequentially.  

## 🔁 101 Switching Protocols
- During the handshake, the server responds with  
  `HTTP/1.1 101 Switching Protocols`  
  to indicate a successful **protocol upgrade** from **HTTP → WS** or **HTTPS → WSS**.



## ⚠️ Challenges of Using WebSockets

1. **Resource Usage**  
   - Each WebSocket connection consumes **server resources** (memory, CPU, file descriptors).  
   - As the number of concurrent connections increases, resource usage scales significantly.  
   - Requires careful **scaling and capacity planning** to maintain performance.

2. **Connection Limits**  
   - Servers and browsers may impose **limits on the maximum number of concurrent WebSocket connections**.  
   - Exceeding these limits can cause new connections to fail or drop existing ones.  
   - Proper connection management and monitoring are essential.

3. **Sticky Sessions (Load Balancing)**  
   - Since WebSockets are **stateful, long-lived connections**, traditional load balancers cannot freely route each request.  
   - **Sticky sessions** ensure that a client’s connection is always routed to the same server.  
   - Proper load balancing and horizontal scaling strategies are needed to **distribute load evenly** without breaking persistent connections.

4. **Authentication**  
   - Unlike HTTP, WebSockets don’t include headers for authentication in every message.  
   - Must handle **token-based authentication** (e.g., JWT) during the initial handshake or through custom message handling.  
   - Security tokens must be validated and refreshed securely during long-lived sessions.

5. **Firewall and Proxy Bypassing**  
   - Some **corporate firewalls or proxies** may block or interfere with WebSocket traffic.  
   - WebSockets use ports 80 (ws) and 443 (wss), but intermediaries may still terminate or timeout long-lived connections.  
   - Requires configuration to ensure **firewall and proxy compatibility**.

6. **Caching**  
   - WebSockets are designed for real-time communication, not static content delivery.  
   - **Caching mechanisms (CDNs, proxies)** are generally ineffective with WebSockets.  
   - This makes bandwidth optimization and scalability more challenging.

7. **Scaling**  
   - Maintaining millions of persistent connections can be difficult.  
   - Requires **distributed infrastructure** with shared state management (e.g., Redis pub/sub, message brokers).  
   - Vertical scaling is limited — horizontal scaling with clustering and proper session handling is crucial.

8. **Testing and Debugging**  
   - WebSockets lack mature testing frameworks compared to HTTP.  
   - **Monitoring and debugging** real-time message flows can be complex.  
   - Tools like `wscat` or browser dev tools help, but end-to-end testing remains a challenge.

9. **Backward Compatibility / Fallback Mechanisms**  
   - Older browsers or restricted networks may not support WebSockets.  
   - Applications need fallback strategies like **long polling** or **short polling** when a connection drops or fails to establish.  
   - Ensures continuity in message delivery.

10. **Resource Cleanup Post-Connection**  
    - When connections close unexpectedly, **resources must be freed properly** (memory, sockets, threads).  
    - Failure to clean up can lead to **memory leaks** or **dangling connections**.  
    - Implementing cleanup logic and heartbeat mechanisms helps maintain stability.

