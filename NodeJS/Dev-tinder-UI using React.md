We are going to use vite
One of the most popular build tool / bundler today is Vite.

![[Pasted image 20251018063440.png]]


# 🧠 CORS (Cross-Origin Resource Sharing)

## 🔍 What It Is
**CORS** stands for **Cross-Origin Resource Sharing**.  
It’s a **browser-enforced security policy** that prevents web pages from making requests to a different *origin* (domain, protocol, or port) unless explicitly allowed by the server.

- **Configured:** Server-side (via response headers)  
- **Enforced:** Client-side (by the browser)

---

## 🌐 What Counts as a Different Origin
Two URLs are **different origins** if *any one* of the following differs:
- **Protocol:** `http://` ≠ `https://`
- **Domain:** `localhost` ≠ `127.0.0.1`
- **Port:** `3000` ≠ `8000`  (Even different ports are considered different CORS)

Example:
- Frontend: `http://localhost:5173`
- Backend: `http://localhost:5000`  
➡️ These are **different origins**, so CORS applies.

---

## ⚙️ How CORS Works
When a browser sends a request to a different origin:

1. For *simple* requests (like basic GETs), the browser directly sends the request.
2. For *non-simple* requests (e.g., with custom headers, JSON body, or methods like `PUT`, `PATCH`, or `DELETE`),  
   the browser first sends a **preflight `OPTIONS` request**.

The **preflight** asks the server:
> “Am I allowed to send this request?”

If the server agrees, it replies with specific headers.

---

## 📬 Server Response (Example Headers)
The backend must respond with these headers to allow the request:

```http
Access-Control-Allow-Origin: http://localhost:5173
Access-Control-Allow-Methods: GET, POST, PUT, DELETE, OPTIONS
Access-Control-Allow-Headers: Content-Type, Authorization

```

## 🧩 Why CORS Errors Only Happen in Browsers

CORS is **enforced by browsers**, not by servers or API clients.

When you make an API request using tools like **Postman**, **curl**, or any **server-side script (Node.js, Python, etc.)**,  
they don’t follow browser-origin security policies — so the request goes through normally.

However, when a **browser** (like Chrome, Edge, or Firefox) sends a request from your frontend JavaScript code to another origin,  
it checks whether the target server allows that origin via **CORS headers**.

If not allowed, the browser **blocks the response** *before your frontend code can access it*.

### 🔑 Summary
- **Browser**: Enforces CORS → will show an error if the server doesn’t respond with the right headers.
- **Postman / curl / Node.js**: Ignore CORS → no error, since they’re not bound by browser-origin policies.

So if your API works perfectly in Postman but fails in your React app,  
it’s almost always a **CORS configuration issue on the server**.


We have to configure this cors policy in the server side and we will use express for it.