## Cookies – Web Storage Notes

### 1. What are Cookies?
Cookies are a **web storage mechanism** used to store **small pieces of persistent data** on the client.  
They are similar to Local Storage and Session Storage but are **automatically sent with HTTP requests**.

---

### 2. How Cookies Work
- Cookies can be **set by the server or the client**
- Cookies are **automatically included in every HTTP request** to the matching domain
- Server can always read cookies
- Client-side JavaScript **may or may not** read cookies depending on configuration (e.g., `HttpOnly`)

---

### 3. Types of Cookies
- **Session Cookies**
  - No expiry date
  - Deleted when the browser is closed
- **Persistent Cookies**
  - Have an explicit expiry (`Expires` or `Max-Age`)
  - Persist until expiry or manual deletion

---

### 4. Size Limit
- **~4 KB per cookie**
- Scoped per **protocol + domain + port**
- Browsers also limit the **number of cookies per domain**

---

### 5. Performance Considerations
- Cookies are sent **with every HTTP request**
- Large or excessive cookies increase request/response size
- Can **slow down network performance and TTFB** ( **[Time to First Byte](https://www.google.com/search?q=Time+to+First+Byte&oq=ttfb&gs_lcrp=EgRlZGdlKgkIABBFGDkYgAQyCQgAEEUYORiABDINCAEQABiDARixAxiABDIKCAIQABixAxiABDIHCAMQABiABDINCAQQABiDARixAxiABDIKCAUQABixAxiABDINCAYQABiDARixAxiABDIHCAcQABiABDIICAgQ6QcY_FXSAQgxNzUxajBqMagCALACAA&sourceid=chrome&ie=UTF-8&ved=2ahUKEwj0pZHtlJ6SAxWIe2wGHbP6H4MQgK4QegYIAQgAEAU)**, measures how long a browser waits to get the first bit of data from a web server after a user requests a page)
- Avoid storing unnecessary data in cookies

---

### 6. Data Persistence
- Controlled using:
  - `Expires` (fixed date)
  - `Max-Age` (relative time)
- Without expiry → treated as session cookie

---

### 7. Data Structure
- Stored as **key=value** pairs
- Values are **strings only**
- No native support for complex data (needs manual serialization)

---

### 8. Security Considerations
Important cookie attributes:

- **HttpOnly**
  - Cookie cannot be accessed via JavaScript
  - Protects against XSS
- **Secure**
  - Cookie sent only over HTTPS
- **SameSite**
  - Controls cross-site cookie behavior
  - `Strict`, `Lax`, or `None` (mitigates CSRF)
- **Domain**
  - Defines which subdomains can access the cookie
- **Path**
  - Restricts cookie access to specific URL paths

⚠️ Vulnerabilities:
- XSS (if not HttpOnly)
- CSRF (if SameSite not configured)
- Cookie theft if improperly scoped or exposed

---

### 9. When to Use Cookies
✅ Suitable for:
- Authentication/session identifiers
- Authorization tokens (prefer HttpOnly)
- Small user preferences
- Server-required state

---

### 10. When NOT to Use Cookies
❌ Avoid for:
- Large datasets
- Client-heavy data access
- Sensitive data stored without HttpOnly/Secure
- High-frequency read/write operations

---

### Interview One-Liner
Cookies are small (~4 KB), domain-scoped storage sent automatically with HTTP requests, ideal for authentication and server-managed state but must be used carefully due to performance and security implications.

## Clear-Site-Data Header

### What is Clear-Site-Data?
`Clear-Site-Data` is a **response header** that instructs the browser to **clear stored data for a specific origin**.

It is commonly used during:
- Logout
- Account deletion
- Security incidents
- Forced re-authentication

---

### What It Can Clear
Depending on the directive used, it can clear:

- **Cookies**
- **Local Storage**
- **Session Storage**
- **Cache**
- **IndexedDB**
- **Service Worker data**

All clearing is scoped to the **current domain (origin)**.

---

### Example Usage (Server-Side)

```js
Clear-Site-Data: "cache", "cookies", "storage"

app.post("/logout", (req, res) => {
  res.setHeader("Clear-Site-Data", '"cache", "cookies", "storage"');
  res.send("Logged out and site data cleared");
});
```

