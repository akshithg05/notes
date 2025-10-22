# 🧩 gRPC — Introduction

![[Pasted image 20251022142330.png]]

## What is gRPC?

**gRPC** stands for **Google Remote Procedure Call** — an **open-source, high-performance RPC framework** developed by Google.  
It enables efficient communication between **distributed systems** and services.

Before diving into gRPC, let's understand its foundation — **RPC (Remote Procedure Call)**.

---

## 💡 RPC (Remote Procedure Call)

RPC is a communication paradigm that allows a **client to directly execute functions or procedures** that **reside on a remote server**, as if they were local calls.

In traditional setups like **REST** or **GraphQL**:
- The **server exposes APIs (endpoints)**.
- The **client makes HTTP requests** to those endpoints.
- The **server executes the corresponding logic** and sends a **response** back.

In **RPC**, instead of invoking endpoints, the client calls **remote methods** directly — the framework abstracts away the underlying network communication.

> 🧠 Think of it as calling a function from another file — except the function actually runs on a **different machine**!

---

## 🚀 What Makes gRPC Special?

- The **"g"** in **gRPC** stands for **Google** — it originated at Google and was later **open-sourced**.  
- It is designed for **high-performance** and **low-latency** communication across microservices or distributed systems.  
- Built on top of **HTTP/2**, it supports **streaming**, **multiplexing**, and **binary serialization** via **Protocol Buffers (Protobuf)**.

---

## ⚖️ gRPC vs REST

| Feature                  | REST                      | gRPC                                                               |
| ------------------------ | ------------------------- | ------------------------------------------------------------------ |
| **Protocol**             | HTTP/1.1 (usually JSON)   | HTTP/2 (binary via Protobuf)                                       |
| **Serialization Format** | JSON (text-based)         | Protocol Buffers (binary, smaller & faster)                        |
| **Communication Type**   | Request–Response          | Unary, Server-streaming, Client-streaming, Bidirectional streaming |
| **Performance**          | Higher latency            | Low latency, high throughput                                       |
| **Use Case**             | Public APIs, web services | Internal microservices, high-performance systems                   |

---

## ✅ Summary

- gRPC = *Google Remote Procedure Call*.  
- Enables direct execution of remote functions.  
- Built for **speed**, **efficiency**, and **scalability**.  
- Ideal for **inter-service communication** in **microservice architectures**.


## 🧠 gRPC — How Communication Happens Between Client and Server

![[Pasted image 20251022143101.png]]

Let’s consider two different machines:

- **Machine A** → acts as the **Client**
- **Machine B** → acts as the **Server**

Both are part of a **distributed system**.

---

### 🔁 Basic Idea

The **Client (A)** wants to execute a **function** that actually runs on the **Server (B)**.  
gRPC makes this possible through a series of well-defined components.

---

### ⚙️ Flow of Execution

1. **Client Stub (on A)**  
   - Acts as a *local representation* of the remote server function.  
   - Similar to a **schema** in GraphQL — it defines what functions can be called and what data types they expect.  
   - The client calls this stub as if it’s a local function.

2. **RPC Runtime (on A)**  
   - Handles the **network communication** part.  
   - It serializes the request (using **Protocol Buffers**) and sends it across the network to the server.

3. **RPC Runtime (on B)**  
   - Receives the serialized request and **forwards it** to the server-side components.

4. **Server Stub (on B)**  
   - Acts as a **bridge** between the RPC runtime and the actual server logic.  
   - It deserializes the incoming data and invokes the corresponding **server function**.

5. **Server Function (on B)**  
   - Executes the actual business logic and returns a response.

6. **Response Flow**  
   - The result moves from **Server Function → Server Stub → RPC Runtime (Server) → RPC Runtime (Client) → Client Stub**.  
   - The **Client Stub** then presents the result to the client application as if the function was executed locally.

---

### 🧩 Summary

- The **stubs** act as communication interfaces.
- The **RPC runtime** handles all serialization, deserialization, and transport.
- The client experiences this as a **simple function call**, even though it’s actually a **remote network operation**.


## 🧩 Key Concept — Client Stub in gRPC

In gRPC, the **client doesn’t directly call** the remote server function.  
Instead, it calls a **local function** — called the **Client Stub**.

- This **Client Stub** is the **local representation** (or proxy) of the actual function that exists on the **Server**.
- When you call this local stub:
  - It **serializes** your request.
  - Sends it over the network via the **RPC runtime**.
  - The **Server Stub** on the other side receives it, executes the **actual server function**, and returns the result.

> 🧠 So yes — you’re calling a *local function* that internally triggers a *remote execution* on another machine.


![[Pasted image 20251022143839.png]]

## 🌐 gRPC Data Transfer and Communication Model

### 🧩 Data Format — Protocol Buffers (Protobuf)

In REST:
- Data is **sent and received in JSON** format.

In gRPC:
- Data is defined using **IDL (Interface Definition Language)**.
- It is **serialized and transmitted** using **Protocol Buffers (Protobuf)** — a **compact, binary** data format.

> 🧠 Protobuf is much faster and smaller than JSON, making communication highly efficient.

---

### ⚙️ Underlying Protocol — HTTP/2

All gRPC communication happens over **HTTP/2**, offering several advantages over HTTP/1.1:

- **Compressed Headers** → reduces bandwidth usage.  
- **Multiplexing** → multiple requests/responses over a single connection (no need to open multiple TCP connections).  
- **Streaming Support** → allows continuous data exchange between client and server.

---

### 🔄 Data Serialization

Just like REST converts data to JSON strings, gRPC **serializes** data into binary format using **Protobuf** before sending it over the network.

Both:
- **Client → Server**
- **Server → Client**

use the **same serialization technique** for communication.

> Serialization = converting structured data into a format suitable for network transmission.  
> Deserialization = converting it back to usable objects.

---

### 🔁 Persistent Connection and Streaming

- gRPC uses a **single long-lived HTTP/2 connection** for communication.
- This enables **streaming** — data can continuously flow without reopening new connections.

#### Types of Streaming:
1. **Unary RPC** → Single request, single response (like REST).
2. **Server Streaming** → Server sends a stream of responses for one client request.
3. **Client Streaming** → Client sends a stream of requests to the server.
4. **Bidirectional Streaming** → Both client and server send streams of data simultaneously.

---

### ⚠️ Bidirectional Streaming vs WebSockets

- Although both allow data flow in both directions, **gRPC bidirectional streaming** is **not** the same as a **WebSocket connection**.
- In gRPC:
  - The client **initiates the call**.
  - Data is **serialized**, sent, processed by the server, and returned — all through **the same HTTP/2 connection**.
  - The connection exists **only for the duration of the RPC call**, not indefinitely.

> 🔍 WebSockets maintain a **long-lived open channel**.  
> gRPC streaming is **call-scoped**, meaning it ends when the RPC completes.

---

### ✅ Summary

- REST → JSON over HTTP/1.1  
- gRPC → Protobuf over HTTP/2  
- Provides **faster**, **more efficient**, and **stream-capable** communication for distributed systems.

## 📦 Protocol Buffers (Protobuf)
![[Pasted image 20251022145130.png]]
### 🧩 What is Protobuf?

**Protocol Buffers (Protobuf)** is a **language-neutral**, **platform-neutral** mechanism for **serializing and deserializing structured data**, developed by **Google**.

It serves as an **Interface Definition Language (IDL)** that defines **how data is structured** and **how services communicate**.

---

### ⚙️ Core Features

- **Developed by Google** for efficient communication across distributed systems.  
- Provides **serialization (converting data to binary)** and **deserialization (reading it back)** mechanisms.  
- Uses a **binary format**, making it **faster and more compact** than text-based formats like **JSON** or **XML**.  
- Currently, the latest and most widely used version is **Proto3**.

> 🧠 The binary format is the key reason gRPC is faster than REST — smaller payloads, faster parsing.

---

### 🧾 The `.proto` File

All Protobuf definitions are written inside a **`.proto` file**.

This file:
- Defines the **data structure** (messages).  
- Defines the **services and RPC methods** (functions that can be called remotely).  
- Acts as the **single source of truth** for both client and server.

Example:
```proto
syntax = "proto3";

service Greeter {
  rpc SayHello (HelloRequest) returns (HelloReply);
}

message HelloRequest {
  string name = 1;
}

message HelloReply {
  string message = 1;
}
```

### 💡 Language Independence

- Once the `.proto` file is defined, it can be **compiled** into many languages using the **Protobuf compiler (`protoc`)**.
- Supported languages include **JavaScript**, **Python**, **Go**, **C++**, **Java**, **C#**, and more.
---
### 🧱 Generated Code

When you compile the `.proto` file:

- It automatically generates **two main code components**:
    1. **Server Code** → Defines what happens when the RPC call is invoked.
    2. **Client Code** → Provides methods and stubs for the client to trigger those RPCs.

The generated code contains:

- **Message classes** (for structured data).
- **Service stubs** (for communication between client and server).
> 🧠 So you write just one `.proto` file, and it automatically provides client–server communication code in any supported language.

## 🔄 Language Independence in gRPC + Protobuf

- The **RPC mechanism handles serialization and deserialization automatically**, no matter what language the client or server is written in.  
- Whether the client is **JavaScript, Python, Go, or Java**, the steps remain the same:

1. The client calls the **generated stub function**.  
2. The stub **serializes the request** into **Protobuf binary format**.  
3. The server **deserializes the request**, executes the function, and **serializes the response**.  
4. The client **deserializes the response** back into usable objects.

> 🧠 This ensures that clients and servers in different languages can **communicate seamlessly**, without worrying about data format conversions.



