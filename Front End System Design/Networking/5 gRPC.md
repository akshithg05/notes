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


23/10/2025

## 🧩 1. Protobuf as an **IDL (Interface Definition Language)**

- The `.proto` file defines:
    - **Data structures (messages)**
    - **Service interfaces (RPCs)**
- It acts as a **contract** between client and server — describing what data can be exchanged and how.

## ⚙️ 2. Protobuf as a **Binary Serialization Format**

- When data is transmitted over the network, gRPC serializes these messages into a **compact binary format** defined by the `.proto` schema.
- This binary format is:
    - **Smaller** than JSON or XML
    - **Faster** to parse
    - **Cross-language** compatible

At runtime:
1. You write `.proto` → **acts as IDL**
2. `protoc` generates language-specific classes
3. Those classes serialize/deserialize your data → **binary format**
4. gRPC sends the **binary bytes** over **HTTP/2**


## ⚡ Benefits of Protocol Buffers (Protobuf)

### 💨 1. High Performance and Low Resource Usage
- **Protobuf uses less CPU and memory** compared to text-based formats like JSON or XML.  
- Ideal for **low-RAM or low-power devices** such as **mobile and IoT systems**.  
- **Efficient binary encoding** allows fast data transmission even on constrained hardware.

---

### 🚀 2. Fast Serialization and Deserialization
- **Serialization** (converting structured data → binary) and  
  **Deserialization** (binary → structured data) happen extremely quickly.  
- Especially beneficial when dealing with **large payloads** or **frequent network calls**.

---

### ⚙️ 3. Compact Binary Format
- Protobuf transmits data in **binary**, not human-readable text.  
- This results in:
  - Smaller message sizes  
  - Lower bandwidth usage  
  - Faster send/receive cycles

> 🧠 In short — Protobuf is optimized for **speed**, **efficiency**, and **lightweight communication** — making it ideal for microservices, mobile clients, and real-time systems.



In coding assessment the following is covered - 

Browser to gRPC client, we will use REST

gRPC client to gRPC server will be using gRPC.
![[Pasted image 20251023112049.png]]

Google uses gRPC a lot for server to server comms.

We are going to do -

CRUD operations on customer - Create, Update , Get, Delete customers.
we have to create these in out customer.proto file.

### 🧠 Why `= 1` (Sequence Number) is Used
- Each field in a Protobuf message has a **unique tag number** (like `1`, `2`, `3`, ...).
- These numbers are used during **serialization** instead of field names — making the binary data **smaller and faster to parse**.
#### 📌 Rules for Field Numbers:
- Must be **unique** within a message.
- Range: `1–15` use **1 byte** for encoding → preferred for frequently used fields.
- Range: `16–2047` use **2 bytes** → for less common fields.
- Tags **19000–19999** are reserved for internal Protobuf use.

> 🧩 In short: `id = 1` means “assign this field the unique tag number 1 for efficient binary encoding.”

![[Pasted image 20251023115130.png]]


## 🧾 CustomerService — Explanation

### 🧩 Overview
This defines a **gRPC service** called `CustomerService` which provides a full set of **CRUD (Create, Read, Update, Delete)** operations for customer data.  
It uses **Protocol Buffers (Proto3)** as the Interface Definition Language (IDL) to define structured messages exchanged between client and server.

---

### 🧱 Service Definition — `CustomerService`

The service exposes the following **remote procedure calls (RPCs):**

| RPC Method | Request Type | Response Type | Description |
|-------------|--------------|----------------|--------------|
| **GetAll** | `Empty` | `CustomerList` | Retrieves all customers. |
| **Get** | `CustomerRequestId` | `Customer` | Retrieves a customer by ID. |
| **Insert** | `Customer` | `Customer` | Adds a new customer record. |
| **Update** | `Customer` | `Customer` | Updates an existing customer record. |
| **Remove** | `CustomerRequestId` | `Empty` | Deletes a customer by ID. |

Each RPC method specifies **input** and **output message types** — these define the exact structure of the data sent and received.

---

### 📦 Message Definitions

#### 1. `Empty`
Used when an RPC method **doesn’t require input or output data**.  
Example:  
- `GetAll` takes no input.  
- `Remove` may not return any data after deletion.

---

#### 2. `CustomerRequestId`
- Contains a single field:  
  - `string id = 1` → represents the unique identifier of a customer.
- The number `1` is a **field tag number**, used by Protobuf during binary serialization.  
  Tags help encode and decode fields efficiently.

---

#### 3. `CustomerList`
- Contains a **repeated field** — meaning it can hold multiple `Customer` objects.  
- Used as the return type for `GetAll` RPCs.

---

#### 4. `Customer`
Defines the structure of a **single customer record** with the following fields:

| Field | Type | Tag | Description |
|--------|------|-----|--------------|
| `id` | `string` | `1` | Unique identifier for the customer |
| `name` | `string` | `2` | Customer’s name |
| `age` | `int32` | `3` | Customer’s age |
| `address` | `string` | `4` | Customer’s address |

---

### 🧠 Why Tag Numbers Like `= 1`, `= 2` Matter

- Tag numbers are **identifiers used for binary encoding** instead of field names.  
- This makes messages **compact** and **fast to serialize/deserialize**.  
- They also allow **backward and forward compatibility** — you can add new fields later with new tag numbers without breaking existing clients.

---

### 🚀 Key Takeaways

- `.proto` files define both **service interfaces** and **message schemas**.
- gRPC generates **client and server code** automatically in multiple languages.
- Protobuf uses **binary encoding**, which is much faster and smaller than JSON or XML.
- This makes gRPC ideal for **microservices**, **mobile**, and **low-bandwidth** environments.

---

## 24-10-2025 gRPC server code nodejs 

## ⚙️ Node.js gRPC Server Explained

This snippet demonstrates how to **set up a gRPC server in Node.js** using a `.proto` file (`customers.proto`) and the `@grpc/grpc-js` library.

---

### 1. Load the `.proto` File

```javascript
const PROTO_PATH = "./../customers.proto";
const grpc = require("@grpc/grpc-js");
const protoLoader = require("@grpc/proto-loader");

const packageDefinition = protoLoader.loadSync(PROTO_PATH, {
  keepCase: true,
  longs: String,
  enums: String,
  arrays: true,
});

const customersProto = grpc.loadPackageDefinition(packageDefinition);


```

**Explanation:**

- `protoLoader.loadSync(PROTO_PATH, options)`
    
    - Reads the `.proto` file and **converts it into a JS object** that can be used by gRPC.
        
    - Options like `keepCase` preserve field names exactly as defined in the `.proto` file.
        
- `grpc.loadPackageDefinition(packageDefinition)`
    
    - Loads the package definition and provides **client and server stubs** for the `CustomerService`.
        

---

### 2. Create a gRPC Server

`const server = new grpc.Server();`

- Creates a new **gRPC server instance** that will host the service.
    
- The server will listen for incoming RPC calls from clients.
    

---

### 3. Add Service Implementation

`server.addService(customersProto.CustomerService.service, {   getAll: (call, callback) => {},   get: (call, callback) => {},   insert: (call, callback) => {},   update: (call, callback) => {},   remove: (call, callback) => {}, });`

**Explanation:**

- `addService` binds the **gRPC service defined in the `.proto` file** to **actual server-side functions**.
    
- Each function:
    
    - Receives a `call` object containing **request data and metadata**.
        
    - Uses `callback(error, response)` to **send the response back to the client**.
        

> ⚡ At this stage, the server functions are placeholders (`{}`), so they don’t yet return actual data.  
> This is where you implement the **business logic** for each RPC.

---

### 4. Bind and Start the Server

`server.bind("127.0.0.1:30043", grpc.ServerCredentials.createInsecure()); server.start();`

- `bind` attaches the server to an **IP address and port** (`127.0.0.1:30043`).
    
- `grpc.ServerCredentials.createInsecure()` → No SSL/TLS (for development purposes).
    
- `server.start()` → Starts listening for incoming RPC requests.
    

---

### 🧠 Summary

1. **Load `.proto`** → Convert IDL to JavaScript objects (stubs).
    
2. **Create server** → Instantiate a gRPC server instance.
    
3. **Bind service** → Connect the `.proto` service definition to **actual functions**.
    
4. **Start server** → Begin listening for client requests.
    

> 🔑 Key Idea:  
> The client calls methods defined in the **client stub**.  
> The server executes the **actual implementation** of those methods and returns responses — all handled automatically by gRPC.


# 🧠 gRPC vs REST — Key Differences

|**Aspect**|**REST**|**gRPC**|
|---|---|---|
|**Protocol**|Uses **HTTP/HTTPS**|Uses **HTTP/2**|
|**Message Format**|Typically **JSON**|Uses **Protocol Buffers (Protobuf)**|
|**Language Support**|No strict language dependency — any language that can make HTTP calls|Uses a **standard IDL (Interface Definition Language)** for code generation across languages|
|**Serialization**|**Text-based (JSON)** — larger and slower to parse|**Binary serialization** — compact and faster|
|**Efficiency**|Less efficient due to HTTP/1.1 and JSON overhead|Highly efficient — supports **multiplexing**, **compression**, and **binary encoding**|
|**Flexibility**|Very flexible — can easily integrate with any system|Strongly typed, fixed **service contracts** defined via `.proto` files|
|**RPC Model**|Only **synchronous request–response**|Supports both **synchronous and asynchronous** communication|
|**Streaming Support**|Limited — typically achieved via **WebSockets**|Built-in support for **client-side**, **server-side**, and **bidirectional streaming**|
|**Service Discovery**|Uses **external tools** (e.g., Kubernetes, Consul)|**Built-in service discovery** and load balancing support|
|**Security**|Relies on **HTTPS** for security|Uses **TLS/SSL** natively|
|**Code Generation**|Uses **Swagger/OpenAPI Codegen**|Uses **Protobuf contracts** to generate client and server stubs|
|**Compatibility**|Widely adopted, **simple and interoperable** across systems|Requires **gRPC libraries** and setup — less ubiquitous|

### ⚙️ Summary

- **REST** is ideal for **public APIs**, broad compatibility, and human-readable communication.
- **gRPC** excels in **high-performance microservices**, **real-time systems**, and **inter-service communication** within controlled environments.
- gRPC trades flexibility for **speed**, **type safety**, and **streaming capabilities**.


# ⚡ Advantages and Disadvantages of gRPC

## ✅ Advantages of gRPC

1. **🚀 Extremely Fast (Up to 10x Faster Than REST)**  
   Uses **Protocol Buffers (binary format)** and **HTTP/2 multiplexing**, resulting in lower latency and faster data transmission.

2. **🔁 Built-in Streaming Support**  
   Supports **client-side**, **server-side**, and **bidirectional streaming**, enabling real-time communication natively.

3. **🔒 Strong Security via HTTP/2**  
   Leverages **TLS/SSL encryption** by default, providing robust security and authentication mechanisms.

4. **🧩 Advanced Code Generation**  
   The `.proto` contract automatically generates **client and server stubs**, ensuring consistency and reducing boilerplate.

5. **🌐 Language Agnostic**  
   Works across multiple programming languages — supports **cross-platform, cross-language communication** through Protobuf.

6. **🔍 Service Discovery & Load Balancing**  
   gRPC has **built-in mechanisms** for service discovery and load balancing, making it highly suitable for microservice architectures.

---

## ⚠️ Disadvantages of gRPC

1. **📦 Non-Human Readable Data**  
   Uses **binary encoding** (Protocol Buffers), making debugging and manual inspection harder compared to JSON.

2. **🌍 Limited Browser Support**  
   Browsers can’t directly call gRPC APIs — requires a **proxy layer** (like Envoy or gRPC-Web) for browser compatibility.

3. **🚫 No Edge Caching**  
   All gRPC calls are **POST requests**, meaning **HTTP caching** mechanisms (like CDNs) don’t work as they do in REST.

4. **📘 Steeper Learning Curve**  
   Developers need to understand **Protobuf, IDL files**, and the **gRPC ecosystem**, making it more complex to get started.
