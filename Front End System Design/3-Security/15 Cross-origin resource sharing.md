
![[Pasted image 20251218080740.png]]

When a web application tries to **access data from another domain**, the browser enforces a built-in security mechanism to check whether that domain **explicitly allows** such access.

Even if the API is public, **the browser will block the response** unless the target server permits cross-origin access via proper headers.  
This restriction is **enforced by the browser**, not by the server itself.

---

## Same-Origin Policy (SOP)

**Same-Origin Policy (SOP)** is the browser’s default security rule.

By default, the browser allows unrestricted data access **only when all three match**:
- Protocol
- Domain
- Port

If all three are the same, data can flow freely without restrictions.

---

## What Is a Cross-Origin Request?

A request is considered **cross-origin** if **any one** of the following is different:

- Protocol  
  - `http://a.com` → `https://a.com` ❌
- Domain / Subdomain  
  - `api.a.com` → `a.com` ❌
- Port  
  - `localhost:3000` → `localhost:4000` ❌

Even:
```
http://localhost:3000 → http://localhost:4000
```
is treated as **cross-origin**.

By default, such requests are **blocked by the browser**.

---

## Why CORS Exists

CORS allows the **server** to explicitly tell the browser:

> “This origin is allowed to access my resources.”

Without this permission, the browser will block access to the response.

---

## Important CORS Headers

### 1. `Access-Control-Allow-Origin`
Specifies which origin(s) are allowed to access the resource.

Example:
```
Access-Control-Allow-Origin: https://example.com
```

---

### 2. `Access-Control-Allow-Methods`
Defines which HTTP methods are allowed for cross-origin requests.

Example:
```
Access-Control-Allow-Methods: GET, POST, PUT
```

---

### 3. `Access-Control-Allow-Headers`
Specifies which custom headers the client is allowed to send.

Example:
```
Access-Control-Allow-Headers: Content-Type, Authorization
```
- Determines what headers can be sent to the different origin.
---

### 4. `Access-Control-Allow-Credentials`
Indicates whether cookies, authorization headers, or TLS credentials are allowed.

Example:
```
Access-Control-Allow-Credentials: true
```
 - Example - When a request is made to a subdomain within the same website we want the credentials to be sent, there this header will come in handy.
---

## Key Takeaways

- SOP blocks cross-origin access by default
- CORS is an **opt-in mechanism**
- Browser enforces CORS, not the server
- Even public APIs must explicitly allow cross-origin access
- Different protocol, domain, or port = cross-origin


# How does CORS work

![[Pasted image 20251218081521.png]]

## CORS Preflight Request Flow

When a client tries to access a resource from a **different origin**, the browser first checks whether the request is allowed.

---

## Step-by-Step Flow

1. **Client initiates a request**
   - The browser detects that the request is **cross-origin**.

2. **Browser sends a Preflight Request**
   - The browser sends an **HTTP OPTIONS** request to the server.
   - This is called a **CORS preflight request**.
   - ❗ This request is **not 304** — it is an **OPTIONS** request, and the response is usually **200 OK**.

3. **Server Responds with CORS Headers**
   - The server responds with headers such as:
     - `Access-Control-Allow-Origin`
     - `Access-Control-Allow-Methods`
     - `Access-Control-Allow-Headers`
     - `Access-Control-Allow-Credentials`

4. **Browser Evaluates the Response**
   - The browser checks the CORS headers.
   - If the response **permits the requesting origin and method**, the browser proceeds.

5. **Actual Request Is Sent**
   - Only after successful preflight validation does the browser send the **actual request** (GET / POST / PUT, etc.).
   - If the preflight fails, the browser **blocks the request** entirely.

---

## Important Clarifications

- The **preflight request is made by the browser**, not the client code.
- The **server does not block the request** — the **browser does**.
- The actual request is sent **only if** the preflight response allows it.
- A `304` status code is related to caching, **not CORS preflight**.

---

## Key Takeaway

> CORS preflight ensures that the server explicitly allows a cross-origin request **before** any real data is sent.

The browser enforces this rule to protect users from unauthorized cross-origin access.

