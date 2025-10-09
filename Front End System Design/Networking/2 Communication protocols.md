### Networking Layers (Simplified)

#### 1. **Network Layer (Layer 3)**
- Responsible for **routing packets** across networks.  
- The main protocol here is **IP (Internet Protocol)**.  
- IP defines *how* data packets travel from one machine to another across the internet.  
- Example protocols:  
  - **IPv4**, **IPv6**

#### 2. **Transport Layer (Layer 4)**
- Responsible for **end-to-end data delivery** and reliability.  
- Defines *how data is sent and received* between two endpoints.  
- Example protocols:  
  - **TCP (Transmission Control Protocol)** → reliable, ordered delivery  
  - **UDP (User Datagram Protocol)** → fast, but unreliable

#### 3. **Application Layer (Layer 7)**
- Defines *how applications communicate* over the internet.  
- These are **Internet protocols** that rely on TCP or UDP underneath.  
- Example protocols:  
  - **HTTP / HTTPS** → built on **TCP**  
  - **WebSockets** → starts with HTTP handshake, then runs over **TCP**  
  - **DNS** → typically runs on **UDP** (sometimes TCP)  
  - **FTP**, **SMTP**, etc.

✅ **Summary**
- **IP** → handles addressing and routing.  
- **TCP / UDP** → handle data transport.  
- **HTTP, HTTPS, WebSockets** → are **Application Layer protocols** that use TCP (and in the case of HTTP/3, UDP) underneath.


![[Pasted image 20251008130900.png]]

## **TCP — Transmission Control Protocol**

### 🔹 Overview
- **TCP** ensures **reliable**, **ordered**, and **error-checked** delivery of data between applications.
- Commonly used for **web browsing (HTTP/HTTPS)**, **email (SMTP, IMAP, POP3)**, and **file transfers (FTP)**.

---
### 🔹 3-Way Handshake
1. **SYN** → Client requests a connection to the server.
2. **SYN + ACK** → Server acknowledges and sends its own sequence number.
3. **ACK** → Client confirms acknowledgment, connection established.
✅ After this, both sides can start sending data packets.

---
### 🔹 Reliable Data Transfer
- Large data is **broken into packets** (segments).
- Each packet has a **sequence number** for correct ordering.
- Client **reassembles** packets based on sequence numbers.
- If any packet is **lost or corrupted**, client requests retransmission → ensures reliability.

---
### 🔹 Key Properties

- **Connection-oriented**
- **Reliable**
- **Ordered delivery**
- **Error detection and correction**
- **Flow and congestion control**

## **TCP Intuition — The Reliable Infrastructure**

- TCP acts as the **underlying infrastructure** for data transfer between two endpoints.
- It ensures that data flows **reliably**, **in order**, and **without loss** — like a well-managed transport network.
- Think of it as:
    - **Road system** → TCP
    - **Vehicles** → Data packets
    - **Addresses** → IP addresses
    - **Traffic lights and signals** → Flow & congestion control
- The application layer (e.g., HTTP, SMTP) just puts its data onto the “road” built by TCP.


## **UDP — The Lightweight Data Courier**

- **UDP (User Datagram Protocol)** is a **connectionless** protocol — it sends data without establishing a dedicated connection between client and server.

- **No reliability checks:**    
    - If packets are lost, duplicated, or arrive out of order, **UDP doesn’t care**.
    - No acknowledgments, no retransmissions, no congestion control.
- **Fast and efficient:** Because it avoids the overhead of reliability mechanisms, it’s ideal for **real-time communication**.
    
- **Use cases:**
    - Video calls (e.g., Zoom, WhatsApp)
    - Live streaming (e.g., YouTube Live, Twitch)
    - Online gaming
- **Analogy:**
    - **TCP** = well-structured road network with signals and toll booths (safe but slower).
    - **UDP** = drones or paper airplanes — fast delivery, but no guarantees of arrival.


### Application Layer Protocols -


![[Pasted image 20251008131327.png]]


HTTP/3 is the latest version of the Hypertext Transfer Protocol and is built on top of **QUIC (Quick UDP Internet Connections)**, a transport protocol developed by Google that runs over **UDP** instead of TCP. Unlike TCP, which requires a three-way handshake and separate TLS negotiation, QUIC combines connection setup and encryption into a single step, significantly reducing latency. It also supports multiplexing, meaning multiple data streams can be sent over the same connection without the head-of-line blocking issue that existed in HTTP/2. Even though QUIC uses UDP, it adds its own mechanisms for **reliability**, **congestion control**, and **security**, providing TCP-like dependability with much faster connection establishment. This makes HTTP/3 ideal for modern web applications, particularly on mobile and unstable networks, as it improves performance, reduces connection time, and maintains built-in encryption through TLS 1.3.
### WebSockets

- WebSockets are a **full-duplex communication protocol** that allows real-time, bidirectional communication between a client and a server over a single persistent connection.  
- Unlike traditional HTTP, which follows a request–response model and closes the connection after each exchange, WebSockets **keep the connection alive** until either side terminates it.  
- This enables both the client and the server to **send data anytime** without waiting for a request.  
- WebSockets are ideal for **real-time applications** such as:
  - Chat systems  
  - Live dashboards  
  - Online gaming  
  - Collaborative tools (e.g., Google Docs-style editing)  
- The WebSocket connection begins with an **HTTP handshake** for compatibility and then upgrades to the WebSocket protocol for continuous, low-latency communication.


### 📧 SMTP (Simple Mail Transfer Protocol)
- **Layer:** Application Layer  
- **Built on:** TCP  
- **Purpose:** Used for **sending emails** between mail servers or from a client to a mail server.  
- **Reliability:** Ensures reliable delivery of outgoing mail.  
- **Ports:** 25 (default), 465 (secure), 587 (submission)  
- **Example:** When you send an email via Gmail, the client uses SMTP to send the message to the mail server.

---

### 📂 FTP (File Transfer Protocol)
- **Layer:** Application Layer  
- **Built on:** TCP  
- **Purpose:** Used to **transfer files** between client and server over a network.  
- **Ports:** 20 (data), 21 (control)  
- **Use Case:** Uploading or downloading large files from a remote file server.  
- **Notes:**  
  - Supports authentication (username/password).  
  - Has a secure version: **FTPS (FTP Secure)** or **SFTP (SSH File Transfer Protocol)**.


