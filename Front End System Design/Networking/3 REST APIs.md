REST API Basics-
![[Pasted image 20251010120131.png]]

Earlier front end backend used to be in the same application and hosted on the same place and 

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

> 🧭 Think of it like this:
> - **HTTP** → The road that connects two cities (handles data transfer).  
> - **REST API** → The traffic rules that define *how* vehicles (data) move on that road.


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
