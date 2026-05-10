REST API Basics-
![[Pasted image 20251010120131.png]]

Earlier front end backend used to be in the same application and hosted on the same place and same build.

Architecture
![[Pasted image 20251010122049.png]]

3 tier architecture
![[Pasted image 20251010122416.png]]

# 🕸️ Evolution of Web Application Architectures

## 🧱 1-Tier Architecture (Monolithic Era)
- **Description:**  
  In the early days, web applications followed a **single-tier (monolithic)** architecture.  
  Both the **frontend** (UI) and **backend** (business logic + data handling) were combined into one application and deployed on a **single server** or machine.  

- **Tech Stack:**  
  Entirely built using **one technology stack** (e.g., PHP, ASP.NET, Java).  

- **Advantages:**  
  - Simple to develop and deploy.  
  - Low infrastructure cost.  

- **Limitations:**  
  - Hard to **scale** — frontend and backend couldn’t scale independently.  
  - Changes in one layer often required redeploying the entire system.  
  - Tight coupling made maintenance and updates difficult.  


---

## ⚙️ 2-Tier Architecture
- **Description:**  
  As user bases grew, companies shifted to a **two-tier architecture** separating the **frontend** and **backend**.  

- **Structure:**  
  - **Frontend:** Runs on the **client’s browser** (HTML, CSS, JavaScript).  
  - **Backend:** Runs on a **remote server** that handles business logic and data.  

- **Advantages:**  
  - Frontend and backend can evolve independently.  
  - Easier to scale and maintain than monoliths.  

- **Limitations:**  
  - Still limited in scalability — all backend services share the same environment.  
  - No isolation between different backend concerns (e.g., messaging, notifications, etc.).  


---

## 🧩 3-Tier Architecture
- **Description:**  
  To address backend complexity, the **database/storage layer** was separated out, forming a **three-tier architecture**.  

- **Structure:**  
  1. **Presentation Layer (Frontend):** User interface (HTML, CSS, JS).  
  2. **Application Layer (Backend):** Business logic (e.g., Node.js, Django, Spring).  
  3. **Data Layer (Storage):** Database and file storage (e.g., MySQL, PostgreSQL, MongoDB).  

- **Advantages:**  
  - Clear separation of concerns.  
  - Each layer can be scaled independently.  
  - Easier maintenance and security.  

- **Limitations:**  
  - Still relatively rigid — backend services are often large and interdependent.  


---

## 🧱➡️🧩 Microservices Architecture
- **Description:**  
  Modern systems evolved toward **microservices architecture**, where the backend is split into **independent services**, each responsible for a specific function (e.g., user service, payment service, notification service).  

- **Structure:**  
  - **Frontend:** Often a SPA (Single Page Application) or mobile client.  
  - **Microservices:** Independent backend services communicating via APIs (usually REST or gRPC). 
  - **Database per service** (optional but common).  

- **Advantages:**  
  - Highly **scalable** and **fault-tolerant**.  
  - Independent deployment and tech stacks per service.  
  - Easier to maintain and iterate on individual modules.  

- **Challenges:**  
  - Increased complexity in orchestration, monitoring, and communication.  
  - Requires robust DevOps practices (e.g., containerization, CI/CD, Kubernetes).  


---

> [!tip] 💡 **Further Reading**
> - *Monolithic vs Microservices Architecture* — Martin Fowler  
> - *The Evolution of Web Architecture* — AWS Whitepaper  
> - *RESTful vs gRPC Communication Models*  

---
 
# 🌐 API Communication & REST

## 🧩 Why APIs?
- In **microservices architecture**, different services need to **communicate** with each other — for example:
  - A **user service** might talk to an **authentication service**.
  - A **payment service** might need data from an **order service**.
- To enable this, applications use **APIs** — *Application Programming Interfaces*.

### 🧠 What is an API?
- An **API** defines **how two software systems interact** — the rules, data formats, and endpoints for communication.
- It makes communication **programming language–agnostic**, meaning:
  - A backend in Python can easily talk to another service written in Go or Node.js.
- APIs abstract away internal logic and expose only the **necessary functions or data**.

---

## 🌍 REST APIs
- One of the most popular ways for web services to communicate is through **REST APIs** —  
  **REST** stands for **Representational State Transfer**.
- It’s not a protocol but an **architectural style** that defines *how* web services should be designed and accessed.

### 🧱 REST API Basics
- REST APIs are built **on top of the HTTP protocol**.
- They use standard HTTP methods to perform actions:
  - `GET` → Retrieve data  
  - `POST` → Send or create data  
  - `PUT` → Update data  
  - `DELETE` → Remove data
- Data is typically exchanged in **JSON** format.

---

## 🌐 Role of HTTP
- **HTTP (Hypertext Transfer Protocol)** defines *how data is transferred* between clients and servers.
- REST leverages HTTP to:
  - Define how requests and responses are structured.
  - Handle status codes (e.g., `200 OK`, `404 Not Found`, `500 Internal Server Error`).
  - Enable communication between different systems over the web.



## 🧭 Quick Summary: REST vs HTTP

- **HTTP (Hypertext Transfer Protocol)**  
  → Defines **how data is transferred** between clients and servers.  
  → It sets the **rules and methods** (like `GET`, `POST`, `PUT`, `DELETE`) for communication over the web.  
  → Think of it as the **transport layer** for web communication.

- **REST (Representational State Transfer)**  
  → An **architectural style** or **set of principles** for designing **web APIs**.  
  → It defines **how web services should behave**, how resources are represented, and how clients interact with them — typically using HTTP as the underlying protocol.  
  → Think of it as the **design philosophy** that rides on top of HTTP.

> 🧩 **In short:**  
> HTTP defines **how** communication happens.  
> REST defines **what rules and practices** an API should follow to communicate effectively over HTTP.


# ⚡ Benefits of REST APIs

REST APIs are widely adopted in modern web applications because they are **simple, scalable, and flexible**.  
They are built on top of **HTTP**, making them language- and platform-independent.

---

## 🌟 Key Advantages

### 1. Ease of Use & Accessibility
- REST APIs are easy to **design, use, and integrate**.
- They use standard HTTP methods (`GET`, `POST`, `PUT`, `DELETE`) which are intuitive and widely supported.
- Most programming languages provide built-in libraries to interact with RESTful endpoints.

---

### 2. Statelessness
- Every request made to the server is **independent** x— it contains **all the information** needed for the server to process it.  
- The server does **not store any session data** between requests.  
- The client must include all required details (e.g., authentication tokens, parameters) each time.
- **Benefits:**
  - Simpler design  
  - Easier to scale horizontally (add more servers easily)
  - No server-side dependency on previous interactions

---

### 3. Scalability
- Because REST is **stateless**, any server can handle any request — there’s no need to store session data.  
- This allows for easy **load balancing** and **horizontal scaling** by simply adding more servers or increasing CPU capacity.

---

### 4. Flexibility
- REST supports multiple **data formats** for communication, including:
  - `JSON` (most common)
  - `XML`
  - `Plain text`
  - `HTML`
- Earlier systems (like SOAP) were limited to XML; REST provides more freedom of choice.

---

### 5. Uniform Interface
- REST enforces a **consistent and predictable structure** for URLs and resource access.  
- Follows standard HTTP conventions for:
  - Resource identification (`/users`, `/orders`)
  - Actions via HTTP verbs (`GET`, `POST`, etc.)
- This makes REST **language-agnostic** and **self-descriptive**.

---

### 6. Caching
- RESTful communication benefits from **HTTP caching mechanisms**.
- Responses can be cached at various levels (browser, proxy, CDN) to reduce server load and latency.
- Headers like `Cache-Control`, `ETag`, and `Expires` are used to manage caching effectively.

---

### 7. Separation of Concerns
- REST naturally supports the separation between:
  - **Client** (frontend, user interface)
  - **Server** (backend, business logic)
- Each can evolve independently as long as the API contract remains consistent.

---

### 8. Interoperability
- REST APIs are **language- and platform-independent**.  
- A Python client can easily consume data from a Java or Go backend.  
- Makes integration between heterogeneous systems straightforward.

---

### 9. Ease of Testing
- REST APIs are simple to test using tools like:
  - **Postman**
  - **cURL**
  - **HTTPie**
- Clear request-response structure enables easy debugging and automation testing.

---

### 10. Security
- REST leverages the **security features of HTTP/HTTPS**, such as:
  - `SSL/TLS` encryption
  - Authentication mechanisms (`Bearer tokens`, `Basic Auth`, `API Keys`)
  - Authorization frameworks (OAuth 2.0, JWT)
- Security is handled through **headers** and **tokens**, keeping the system stateless yet secure.

---

> [!tip] 💡 **In Summary**
> REST APIs combine **simplicity**, **scalability**, and **flexibility**,  
> making them one of the most widely used methods for building and connecting modern web services.

---


## 11/10/2025 - Diving Deep into each building block

## 🧭 Who Defines the Structure of Requests & Responses — HTTP or REST?

### ✅ Short Answer
The **structure of the request and response** — like headers, status codes, methods (`GET`, `POST`, etc.), and message format —  
is defined by **HTTP**, *not* REST.

---

### 🌐 HTTP Defines the Communication Rules
- **HTTP (Hypertext Transfer Protocol)** is the *transport protocol* (Application layer protocol )that defines:
  - How a request is made (method, headers, body)
  - How a response is returned (status code, headers, body)
  - The syntax and semantics for communication between a client and a server
- Every web communication (including REST) follows this structure:


---

### 🧱 REST Defines How to *Use* HTTP
- **REST** builds *on top of HTTP* and defines **how web services should be designed** using those existing HTTP features.  
- It gives guidelines like:
- Use URLs to represent **resources** (`/users`, `/orders/123`).
- Use HTTP methods to define **actions** on those resources (`GET`, `POST`, `PUT`, `DELETE`).
- Use standard HTTP **status codes** to indicate results (`200 OK`, `201 Created`, `404 Not Found`).
- In short, REST says *how to behave when using HTTP* for web communication.

---

> 🧩 **Analogy:**  
> - **HTTP** = The grammar and syntax of the language (how to form sentences).  
> - **REST** = The style guide that tells you how to write clean, consistent, and meaningful sentences using that grammar.

---

> [!tip] 💡 **Key takeaway**
> - The **request/response structure** → defined by **HTTP**  
> - The **principles for designing APIs** that use this structure → defined by **REST**

Building blocks 
![[Pasted image 20251011071332.png]]



## Breaking down a HTTP Request

![[Pasted image 20251011071705.png]]

## 🧩 1. Request Line
- This is the **first line** of the HTTP request.
- It contains **three key elements**:
  1. **HTTP Method** — Defines the type of operation to be performed.  
     Examples: `GET`, `POST`, `PUT`, `DELETE`
  2. **Request URL / Path** — Identifies the resource being requested.  
     Example: `/api/users` or `/products/123`
  3. **HTTP Version** — Specifies which HTTP version is being used (e.g., `HTTP/1.1`, `HTTP/2`, `HTTP/3`)

📘 **Example:** ```GET /api/users HTTP/1.1

## 🧠 2. Request Headers
- The **headers section** provides **metadata** about the request.
- They define how the client and server should communicate.
- Common headers include:
  - `Host:` → The domain name of the server  
  - `Authorization:` → Tokens or credentials for authentication  
  - `Accept:` → Expected response format (e.g., `application/json`)  
  - `Content-Type:` → Format of the request body (e.g., `application/json`)  
  - `Origin:` and `Access-Control-Allow-Origin:` → For CORS handling  
  - `Accept-Encoding:` → Compression formats supported by the client

	Host: api.example.com  
	Authorization: Bearer token  
	Accept: application/json  
	Content-Type: application/json

## 🧾 3. Request Body (Optional)
- The **body** carries the actual **data** being sent to the server.  
- It’s usually present in methods like `POST` or `PUT`, where data (like form fields or JSON objects) is required.
- Common formats:
  - `JSON` → `{ "username": "akshith", "password": "12345" }`
  - `XML` → `<user><name>akshith</name></user>`
  - `Form data` → `application/x-www-form-urlencoded`

📘 **Example:**
{  
"username": "akshith",  
"password": "12345"  
}


# 📬 Structure of an HTTP Response

![[Pasted image 20251011072456.png]]

After the client sends a request, the server processes it and returns a **response**.  
Like the request, an HTTP response also follows a well-defined structure made up of **three main components**:
## 🧩 1. Status Line
- The **first line** of the response.  
- It contains **three key parts**:
  1. **HTTP Version** — Indicates which version of HTTP is being used.  
     Example: `HTTP/1.1`
  2. **Status Code** — A 3-digit number indicating the result of the request.  
     Examples: `200`, `404`, `500`
  3. **Status Message (Reason Phrase)** — A short text describing the status code.  
     Examples: `OK`, `Not Found`, `Internal Server Error`

## 🧠 2. Response Headers
- The **headers section** provides **metadata** about the response and how the client should interpret it.
- Common response headers include:
  - `Content-Type:` → Format of the returned data (e.g., `application/json`)
  - `Content-Length:` → Size of the response body
  - `Cache-Control:` → Caching instructions
  - `Set-Cookie:` → Sends cookies to the client
  - `Access-Control-Allow-Origin:` → Defines which origins can access the resource (CORS)
  - `Server:` → Provides information about the web server software

## 🧾 3. Response Body (Optional)
- The **body** carries the actual data returned by the server.
- It can include HTML, JSON, XML, or other content depending on the `Content-Type`.
- For REST APIs, JSON is most common.


# 🌐 Breaking Down a URL

A **URL (Uniform Resource Locator)** uniquely identifies and locates a resource on the web.  
It helps the client (like a browser or an API client) **query exactly what it needs** from a server.

---
## 🧩 Basic Structure of a URL

![[Pasted image 20251011075921.png]]


Example: https://www.example.com/learn?page=2#intro


Let’s break this down step by step 👇

---
### **1. Scheme (Protocol)**
- Defines the **protocol** used to access the resource.
- Common examples:  
  - `http` → HyperText Transfer Protocol  
  - `https` → Secure version of HTTP (encrypted via SSL/TLS)
  - Others: `ftp`, `mailto`, `file`, `ws`, `wss`

📘 Example: https://

---
### **2. Subdomain**
- The **prefix before the main domain**, often used to categorize sections of a website.
- Common example: `www`
- You might also see:
  - `blog.example.com`
  - `api.example.com`

📘 Example: [https://www](https://www).

### **3. Domain Name**
- The **main readable name** that identifies the website or organization.
- Example: `example` in `example.com`

---
### **4. Top-Level Domain (TLD)**
- The **suffix** at the end of the domain name.
- Common TLDs: `.com`, `.org`, `.in`, `.edu`, `.io`, etc.

### 🏠 Hostname
- The **hostname** is made up of:
  - Subdomain  
  - Domain name  
  - Top-level domain (TLD)

📘 Example: www.example.com

### **5. Path / Subdirectory**
- Comes **after the hostname**, separated by `/`
- It represents the **location of a resource** on the server.
- Think of it as the “folders” or “routes” that lead to specific content.

📘 Example: /learn


💡 On a real server, this might be:
- A **physical folder**
- Or a **dynamic route** handled by backend logic. Most of the times it is a dynamic route itself

---
### **6. Query String**
- Begins **after a `?`** in the URL.
- Contains **key-value pairs** that pass additional parameters to the server.
- Used to **filter, search, or customize** data in the response.

📘 Example: ?page=2&sort=asc

---
### **7. Fragment**
Begins **after a `#`** in the URL.  
Points to a **specific section within a web page**.  
Used mainly for navigation within a page (e.g., scrolling to a heading).  

⚠️ **Important:** The fragment is **not sent to the server** — it’s handled entirely by the browser/client.

**Example:** #intro


---

## 🧭 Full URL Example Breakdown

| Component                  | Example   | Description                                  |
| -------------------------- | --------- | -------------------------------------------- |
| **Scheme**                 | `https`   | Protocol used for communication              |
| **Subdomain**              | `www`     | Section or category of the main domain       |
| **Domain Name**            | `example` | The main readable name                       |
| **Top-Level Domain (TLD)** | `.com`    | Defines the domain category or region        |
| **Path / Subdirectory**    | `/learn`  | Route to a resource                          |
| **Query String**           | `?page=2` | Extra parameters for filtering/customization |
| **Fragment**               | `#intro`  | Section of the web page (not sent to server) |

**Full URL:** https://www.example.com/learn?page=2#intro

---

> [!tip] 🌟 **Quick Recap**
> - The **host** = subdomain + domain name + TLD  
> - The **path** identifies where the resource lives on the server  
> - The **query string** passes dynamic data  
> - The **fragment** is for client-side navigation only



## 12/10/2025

# ⚙️ Advanced HTTP Methods

Beyond the common CRUD methods (`GET`, `POST`, `PUT`, `DELETE`), HTTP defines several **special-purpose methods** that serve diagnostic, connectivity, and permission-related roles.  
These methods are less frequently used in application development but are crucial for understanding how the web handles connections and security under the hood.

## 🧠 1. `HEAD` Method

**Purpose:**  
Requests the **headers** of a resource **without fetching the actual body/content**.

**Use Case:**  
- To check if a resource exists or is accessible.  
- To get **metadata** (like content length, last modified date, or type) before downloading large files.


🧩 **Note:**  
`HEAD` behaves exactly like a `GET` request — except the response **omits the body**.  
This helps clients check information *without downloading the entire resource.*

---

## 🌐 2. `OPTIONS` Method

**Purpose:**  
Used to **describe the communication options** available for a given resource or server.  
Commonly used for **CORS (Cross-Origin Resource Sharing)** preflight checks.

**CORS Preflight Scenario:**
- When a browser makes a request to a **different origin** (domain, port, or protocol), it first sends an `OPTIONS` request.  
- This “preflight” call asks the server if the actual request (like a `POST` or `PUT`) is allowed.
- The server responds with headers specifying what is permitted.


💡 **Key Insight:**  
If the browser receives a response allowing the origin and method, it proceeds with the actual request.  
Otherwise, the main request is **blocked** for security reasons.

---

## 🔗 3. `CONNECT` Method

**Purpose:**  
Used to **establish a tunnel** between the client and the target server — often through an **HTTP proxy**.

**Primary Use Case:**  
- Commonly used for **HTTPS connections** via proxies.
- Allows clients to set up an encrypted channel (TCP tunnel) through which subsequent requests can flow securely and efficiently.

🔒 **In short:**  
`CONNECT` sets up the secure link, after which the client can send encrypted HTTPS data through that tunnel — improving security and speed for subsequent requests.

---

## 🧰 4. `TRACE` Method

**Purpose:**  
Used for **diagnostic purposes** — it echoes back the received request so that the client can see how intermediate servers (proxies, gateways) modify the message.


Whenever we send data over the network we send serialized stringified data. We have to parse it on the server side and use it. We can use express.json() in express or bodyParser.

IN our browser whenever we make a request its always a get call. We need a client to do this.


## 14/10/2025

## Request Headers

![[Pasted image 20251015073030.png]]
### 🏠 Host

**Definition:**  
Specifies the **target server (domain and port)** to which the request is being sent.

**Purpose:**  
- Identifies the destination host for the HTTP request.  
- Essential for servers hosting multiple domains (virtual hosting).  
- Without it, the server wouldn’t know *which site* you want (when several share the same IP).

Example - api.example.com

---
## 🌍 Origin

**Definition:**  
Indicates the **source (scheme + domain + port)** from which the request originated.

Example - Origin: https://frontend.example.com

**Purpose:**  
- Used primarily for **CORS (Cross-Origin Resource Sharing)**.  
- Helps the server decide whether to allow or block a request based on the requesting site.  
- Unlike `Referer`, it **never includes paths or query strings** — only identifies the origin for security checks.

**Typical Usage:**
- Sent automatically by browsers in **cross-origin requests** (like `fetch` or `XHR`).
- Server responds with headers like:

## 🔗 Referer

**Definition:**  
Specifies the **URL of the page** that made the request — i.e., where the user came from.

**Example:** https://google.com/search?q=laptops

**Purpose:**  
- Lets the server know which page or site referred the request.  
- Used for analytics, logging, and sometimes security (e.g., detecting CSRF).

**Privacy Notes:**
- Can leak sensitive info (like tokens or query params).  
- Controlled by the browser via the `Referrer-Policy` header.

**Common Referrer Policies:**
| Policy | Behavior |
|--------|-----------|
| `no-referrer` | Don’t send any referrer info. |
| `origin` | Send only scheme + domain. |
| `strict-origin-when-cross-origin` | Default in most browsers. |
| `unsafe-url` | Always send full URL (not recommended). 

## 🧑‍💻 User-Agent

---
#### 🧩 Definition
The **`User-Agent`** header identifies the **client software** making the HTTP request — typically a web browser, mobile app, or other HTTP client.

It includes detailed information such as:
- Browser name and version  
- Operating system and version  
- Rendering engine (like Blink, Gecko, or WebKit)  
- Device type (desktop, mobile, tablet, etc.)

---
#### 🧠 Purpose
- Helps the **server understand the client’s environment** and send optimized resources accordingly.  
- For example:
  - A mobile browser may receive lighter images or a responsive layout.  
  - Older browsers might get polyfilled JS bundles or fallback CSS.
#### Example-
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64)  
AppleWebKit/537.36 (KHTML, like Gecko)  
Chrome/118.0.5993.88 Safari/537.36

## 📦 Accept 

### Definition
The **`Accept`** header tells the server what **content types (MIME types)** the client is willing to receive in the response.  
This lets the server choose the most suitable format (like JSON, HTML, or XML) for the reply.

---
### Purpose
It specifies **preferred response formats** so that the server can perform **content negotiation**.

---
Example
application/json
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,_/_;q=0.8

## 🌐 Accept-Language

The **`Accept-Language`** header tells the server which languages the client prefers for the response. It’s mainly used for localization, allowing servers to send content in the user’s preferred language. For example,  
`Accept-Language: en-US,en;q=0.9,fr;q=0.8`  
means the client prefers English (US) first, then English in general, and finally French. This helps servers deliver region-specific or translated content for a better user experience.

![[Pasted image 20251015072757.png]]

## ⚙️ Accept-Encoding

The **`Accept-Encoding`** header tells the server what types of **content encoding (compression algorithms)** the client can handle in the response. This helps reduce payload size and improve performance. For example:  
`Accept-Encoding: gzip, deflate, br`  
means the client supports compressed responses using **gzip**, **deflate**, or **Brotli** (`br`). The server then chooses one supported method and includes it in the `Content-Encoding` header of its response.

## 🔗 Connection

The **`Connection`** header controls whether the **TCP connection** between the client and server should remain open after the current request.  
If set to `keep-alive`, the same connection is reused for multiple requests, avoiding repeated TCP handshakes and improving performance.  
If set to `close`, the connection is terminated after the response.  
Example:  
`Connection: keep-alive`


## 🔐 Authorization

The **`Authorization`** header is used by the client to send **credentials** to the server for authentication.  
It verifies whether the user or client has permission to access a resource.  
Common examples include:  
- `Authorization: Basic <base64encoded-credentials>`  
- `Authorization: Bearer <JWT-token>`  
This helps implement authentication mechanisms like **Basic Auth**, **Bearer Tokens**, and **OAuth**.

---

## 🍪 Cookie

The **`Cookie`** header allows the client to send small pieces of **data** (like session IDs, JWTs, or authentication tokens) back to the server with each request.  
These cookies are usually set by the server using the `Set-Cookie` response header and stored on the client side.  
They enable **stateful sessions**, user tracking, and persistent logins.  
Example:  
`Cookie: session_id=abc123; token=xyz789`

## ⏳ If-Modified-Since

The **`If-Modified-Since`** header is used by the client to make **conditional requests**.  
It tells the server: “Only send the data if it has been modified since this specific date and time.”  
If the resource hasn’t changed, the server responds with **`304 Not Modified`**, saving bandwidth and improving performance.  
Example:  
`If-Modified-Since: Wed, 09 Oct 2025 10:00:00 GMT`

---

## 🗃️ Cache-Control

The **`Cache-Control`** header defines **caching policies** for both clients and intermediate proxies (like CDNs).  
It tells them **how, where, and for how long** a resource can be cached.  
Examples:  
- `Cache-Control: no-cache` → Always revalidate before using cached data.  
- `Cache-Control: no-store` → Don’t cache this response at all.  
- `Cache-Control: max-age=3600` → Cache for 1 hour (3600 seconds).  
- `Cache-Control: public` / `private` → Specifies who can cache the response.  

This header helps optimize performance by reducing redundant requests and speeding up data delivery.

We will comeback to cache control in detail later on.



# Response Headers

![[Pasted image 20251015075723.png]]
![[Pasted image 20251016081818.png]]
## 🕒 Date

The **`Date`** header shows the **exact time and date** when the response was generated on the server (in GMT format).  
It helps with **cache validation**, ensuring freshness, and is often used along with headers like `If-Modified-Since` and `Cache-Control`.  
Example:  
`Date: Fri, 10 Oct 2025 12:30:00 GMT`

---

## 🖥️ Server

The **`Server`** header identifies the **software** used by the server to handle the request — e.g., Apache, Nginx, or Node.js.  
While useful for diagnostics, it can expose **sensitive infrastructure details**, making it a **potential security risk**.  
Best practice: either **omit** or **anonymize** this header in production.  
Example:  
`Server: nginx/1.24.0`

---

## 📦 Content-Type

The **`Content-Type`** header specifies the **media type (MIME type)** and **character encoding** of the response body.  
It tells the client how to interpret the returned content.  
Examples:  
- `Content-Type: application/json; charset=utf-8`  
- `Content-Type: text/html`  
- `Content-Type: image/png`

This header is essential for **data interpretation** and **proper rendering** on the client side.

## 📏 Content-Length

The **`Content-Length`** header indicates the **size of the response body** in **bytes**.  
It tells the client how much data to expect, which helps in tracking **download progress**, managing **data streams**, and verifying **complete data transfer**.  
Example:  
`Content-Length: 2048`  
This means the response body is 2048 bytes long.

## 🍪 Set-Cookie

The **`Set-Cookie`** header is sent by the **server** to the **client** to store cookies for future requests.  
It defines key–value pairs along with optional attributes like expiration, path, domain, and security flags.  
These cookies are then sent back to the server in subsequent requests using the `Cookie` header.  
Example:  
`Set-Cookie: session_id=abc123; Expires=Wed, 15 Oct 2025 10:00:00 GMT; Path=/; Secure; HttpOnly`

## ⚙️ Content-Encoding

The **`Content-Encoding`** header tells the client what kind of **compression or encoding** the server applied to the response body.  
It helps the client correctly **decode** and **decompress** the received data before using it.  
Common values include:  
- `gzip`  
- `deflate`  
- `br` (Brotli)  
Example:  
`Content-Encoding: gzip`


## 🗃️ Cache-Control / Expires / Last-Modified

These headers help control **how responses are cached** by the browser or intermediate proxies.

- **Cache-Control:** Defines caching rules like duration, visibility, and revalidation.  
  Example: `Cache-Control: max-age=3600` → cache for 1 hour.  

- **Expires:** Specifies an **absolute date/time** after which the response is considered stale.  
  Example: `Expires: Wed, 15 Oct 2025 10:00:00 GMT`  

- **Last-Modified:** Indicates the **timestamp of the resource’s last change**.  
  Clients can use this with `If-Modified-Since` to check if cached data is still fresh.  
  Example: `Last-Modified: Tue, 14 Oct 2025 09:30:00 GMT`

## 🏷️ ETag (Entity Tag)

- **ETag** is a unique identifier assigned by the server to a specific version of a resource.  
- When the resource changes, its ETag value also changes.  
- The browser can send this ETag back to the server using `If-None-Match` to check if the cached version is still valid.  
- If unchanged → server returns **304 Not Modified**, saving bandwidth. 


# Status Codes

Status codes help identify the outcome of an HTTP request — whether it was **successful**, **redirected**, **unauthorized**, or resulted in an **error**.  
They act as identifiers that communicate the **status of the response** from the server to the client.

![[Pasted image 20251016091945.png]]
![[Pasted image 20251016092309.png]]

### HTTP Status Codes  

Status codes indicate the **result of an HTTP request**, helping the client understand whether it was successful, redirected, failed due to client error, or failed due to a server issue.

---

#### 🟦 1XX — Informational  
Used to convey **information or acknowledgements** before the final response.  
- **100 Continue** → The client can continue sending the request body.  
- **101 Switching Protocols** → The server agrees to switch protocols (e.g., HTTP → WebSocket). *(Rare)*  

🧠 *Think of it like a waiter saying, “I’ve noted your order, it’s being prepared.”*

---

#### 🟩 2XX — Success  
Indicates that the **request was successfully received, understood, and processed**.  
- **200 OK** → Request processed successfully.  
- **201 Created** → Resource successfully created.  
- **202 Accepted** → Request accepted for processing, response will come later.  
- **204 No Content** → Request processed, no response body (e.g., after deletion).  
- **206 Partial Content** → Partial data sent (useful for large downloads or media streaming).  

💡 *Backend developers should use specific codes instead of returning 200 for everything.*

---

#### 🟨 3XX — Redirection  
Indicates that the **client must take additional action** to complete the request, usually following a new URL.  
- **301 Moved Permanently** → Resource moved to a new location.  
- **302 Found (Temporary Redirect)** → Temporary redirect, original URL may be valid later.  
- **307 Temporary Redirect** → Like 302, but retains the original HTTP method.  
- **308 Permanent Redirect** → Like 301, but also retains the HTTP method.  

🌐 *Useful when APIs or endpoints are moved or restructured.*

---

#### 🟥 4XX — Client Errors  
Indicates **errors caused by the client**, such as invalid requests, authentication issues, or missing resources.  
- **400 Bad Request** → Invalid or improperly formatted request.  
- **401 Unauthorized** → Authentication required or invalid credentials.  
- **403 Forbidden** → Authenticated but not authorized (e.g., no admin rights).  
- **404 Not Found** → Resource doesn’t exist.  
- **405 Method Not Allowed** → HTTP method not supported on this route.  
- **429 Too Many Requests** → Rate limit exceeded, try again later.  

🚫 *These are typically caused by incorrect client-side input or permissions.*

---

#### ⛔ 5XX — Server Errors  
Indicates **problems on the server side** while processing a valid client request.  
- **500 Internal Server Error** → General server failure.  
- **502 Bad Gateway** → Invalid response from an upstream server.  
- **503 Service Unavailable** → Server down or overloaded.  
- **504 Gateway Timeout** → Upstream server didn’t respond in time.  
- **507 Insufficient Storage** → Server out of space (e.g., large uploads).  

🔥 *These indicate issues that need backend or infrastructure attention.*

---

💭 **Summary Table**

| Range | Category | Meaning |
|-------|-----------|----------|
| 1XX | Informational | Request received, continuing process |
| 2XX | Success | Request successfully processed |
| 3XX | Redirection | Client must follow another location |
| 4XX | Client Error | Problem with the request |
| 5XX | Server Error | Problem with the server |

###  Why Status Codes Matter for Frontend Engineers  

Status codes are crucial for frontend developers because they help determine **how the UI should respond** to different situations.  

They allow developers to **write smart error-handling logic** — deciding when to retry a request, show an error message, or prompt the user to take action.  

For example:  
- If the error is **404 (Not Found)** or **403 (Forbidden)** → there’s **no point retrying**, since the issue is permanent (wrong URL or insufficient permissions).  
- If the error is **429 (Too Many Requests)**, **500 (Internal Server Error)**, or **504 (Gateway Timeout)** → it’s likely **temporary**, and the request can be **retried automatically** or after a short delay.  

💡 **In short:**  
Status codes help the frontend **react intelligently** — avoiding unnecessary retries, improving user experience, and providing meaningful feedback instead of generic “something went wrong” messages.

Therefore status codes matter for every type of web developer, not only for front end or backend engineer.


