
![[Pasted image 20251121144045.png]]
# Server-Sent Events (SSE)

## 1. What Are SSE?
Server-Sent Events (SSE) provide a **one-way real-time communication channel** from **server → client** using a standard long-lived HTTP connection.  
They are supported in most modern browsers and are ideal when the server needs to continuously push updates to the client. Exaampe - news feeds, notifications like instgram, facebook, linkedin and monitoring dashboards.


---
## 2. How SSE Works

### Single Long-Lived HTTP Connection
- The client sends **one HTTP request** to the server.
- The server **keeps the connection open** instead of closing it after a response.
- New data is **streamed to the client** whenever available.
- No repeated requests are needed from the client.

---
## 3. Difference Between SSE and Long Polling

| Feature | Long Polling | Server-Sent Events |
|--------|--------------|-------------------|
| Connection | Multiple request–response cycles | Single persistent connection |
| Data Flow | One response per request | Continuous stream of updates |
| Overhead | Higher | Lower |
| Direction | Client → Server triggered | Server → Client only |

**Summary:** Long polling continuously reopens connections.  
SSE **keeps a single connection alive** and pushes events over it.

---
## 4. How Data Is Sent in SSE
- Data is sent in **text/event-stream** format.
- Server pushes new messages whenever new data exists.
- Connection stays open until:
  - closed by client,
  - closed by server,
  - or network drops.
- Browsers automatically **reconnect** if the connection breaks.

---
## 5. Why Use SSE?
SSE is ideal for:
- Real-time notifications  
- Live dashboards  
- Event streams  
- Monitoring/logging pipelines  
- Price / stock updates  
- Any one-way server → client update system

---
## 6. High-Level Flow

```
Client                Server
  | ---- Request ----> |
  | <--- Stream Data --|
  | <--- Stream Data --|
  | <--- Stream Data --|
  |   (connection open)
```

## 7. SSE Event Format

Data in SSE comes through an **event stream**, where each message is sent in a simple text format.  
Each event can contain fields such as:

- **event:** the event name/type  
- **data:** the actual payload  
- **id:** a unique identifier used for reconnection and resuming the stream  

### Example Event Structure
```
id: 42
event: message
data: {"text": "Hello from the server!"}
```

### Role of the `id` Field
- The browser automatically stores the last received `id`.
- If the connection drops, the client retries the stream.
- During reconnection, the last `id` is sent to the server (`Last-Event-ID` header).
- This allows the server to resume from the **next event**, preventing data loss.

### Summary
SSE events are lightweight text messages where:
- `event` defines the type of update  
- `data` contains the content  
- `id` ensures reliable delivery during reconnects


## 8. Caution: Long-Lived Connections in SSE

SSE uses a **single long-lived HTTP connection**, which means the connection stays open for an extended period instead of closing after the response.

Because of this, there are important considerations:

### Why You Need to Be Careful
- **Each client consumes one server connection**  
  Since SSE connections stay open, every connected client occupies:
  - a file descriptor  
  - memory buffers  
  - a worker/thread/event-loop slot (depending on server architecture)

- **Large numbers of clients → high resource usage**  
  For example, if 10,000 clients are connected simultaneously:
  - the server must maintain **10,000 open sockets**  
  - this can exhaust OS limits (max open files)  
  - and increase CPU load for managing idle but open connections  

- **Server must support concurrency well**  
  SSE works best in:
  - event-driven servers (Node.js, Deno, Go, Nginx)  
  - environments optimized for many open connections  

  It is not ideal for:
  - traditional thread-per-request servers  
  - low-resource systems  

### Scaling Considerations
- Increase system file descriptor limits (`ulimit -n`)
- Use load balancing to distribute connections
- Prefer event-driven frameworks that handle idle connections efficiently
- Use heartbeats (periodic `data: ping`) to keep connections alive
- Plan for automatic browser reconnection behavior

### Summary
SSE is lightweight and simple, but you must plan for **connection persistence**, since each client ties up one open connection for a long time. This makes capacity planning and server design crucial for production use.


Some challenges to think about while using SSE
![[Pasted image 20251121155614.png]]

