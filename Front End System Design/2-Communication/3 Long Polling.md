
![[Pasted image 20251029194804.png]]
# 🧩 Long Polling

Unlike **short polling**, where the client sends requests at fixed intervals and the server responds immediately (even if no new data is available), **long polling** keeps the connection open until the server has new information to send.

## 🔁 How It Works
- The client sends a request to the server.  
- The server **keeps the connection alive** until there’s a new update or a timeout occurs.  
- Once the server responds (either with data or a timeout), the client **immediately sends another request**, repeating the process.  
- This creates a continuous loop of waiting → receiving → re-requesting.

## ⚙️ Key Characteristics
- Single long-lived connection per request cycle.  
- Connection stays open until:
  - The server has new data, **or**
  - The request times out.  
- Fewer round trips compared to short polling.  
- Simulates near real-time communication using standard HTTP.

## ⚠️ Drawbacks
- Each client maintains a persistent connection → increases load on the server.  
- Scalability can be a challenge for applications with many concurrent users.  
- Less efficient than WebSockets for true bidirectional communication.

## 💡 Real-World Use Cases
- Chat applications (e.g., Facebook Chat before WebSockets).  
- Comment or notification systems (e.g., Stack Overflow new answer alerts).  
- Collaborative tools (e.g., Google Docs before WebSocket adoption).  
- Newsfeed or social updates where moderate real-time updates are required.

