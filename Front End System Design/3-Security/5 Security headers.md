
![[Pasted image 20251211071505.png]]
# 1. Security Header: `X-Powered-By`

The `X-Powered-By` response header reveals information about the server technology used by the application.  
For example, when running a basic Express server:

```js
const express = require("express");

const app = express();

app.get("/", (req, res) => {
  res.status(200).send({
    message: "This is the security headers section",
  });
});

const port = 3000;
app.listen(port, () => {
  console.log(`Server is listening on port ${port}...`);
});
```

If you inspect the response headers in the browser, you will see:

```
X-Powered-By: Express
```

---

## Why This Is a Problem

This header **leaks information** about the underlying server framework.  
Attackers can use this information to:

- Identify the exact server technology  
- Search for known vulnerabilities specific to that server version  
- Craft targeted attacks  

Exposing this information makes the application easier to attack.

If the header is removed, the attacker has less information to work with.

---

## How to Remove the `X-Powered-By` Header

We can use a simple Express middleware to remove the header before the response is sent:

```js
const express = require("express");

const app = express();

app.use((req, res, next) => {
  res.removeHeader("X-Powered-By");
  next();
});

app.get("/", (req, res) => {
  res.status(200).send({
    message: "This is the security headers section",
  });
});

const port = 3000;
app.listen(port, () => {
  console.log(`Server is listening on port ${port}...`);
});
```

After adding this middleware, the response will **no longer contain** the `X-Powered-By` header.

---

## Summary

- `X-Powered-By` reveals server technology (e.g., Express).  
- This information can help attackers exploit known vulnerabilities.  
- Removing the header improves security by limiting information exposure.  
- Use `res.removeHeader("X-Powered-By")` to hide server details.

# 2. Security Header: Referrer-Policy

The `Referrer-Policy` header controls how much **referrer information** (the URL of the previous page) is sent when a user navigates from one page to another.

The referrer can contain sensitive details:
- Full URL
- Query parameters
- Path information  
So exposing it may leak unnecessary data.

We can control what gets sent using the `Referrer-Policy` header.

---

## Common Referrer Policy Options (Brief Notes)

### **1. `no-referrer`**
- Sends **no referrer information at all**.
- Maximum privacy.

---

### **2. `no-referrer-when-downgrade`** *(Default in many browsers)*
- Sends referrer only when navigating from HTTPS → HTTPS.
- Does **not** send referrer when going HTTPS → HTTP (downgrade).

---

### **3. `origin`**
- Sends only the **origin**, not the full URL.  
Example referrer sent:
```
https://example.com
```
Not:
```
https://example.com/dashboard?user=123
```

---

### **4. `same-origin`**
- Sends full referrer **only when navigating within the same origin**.
- Sends **nothing** to external origins.

---

### **5. `origin-when-cross-origin`**
- Same-origin → sends full referrer.
- Cross-origin → sends only the origin (not full path or params).

---

### **6. `strict-origin`**
- Sends only the origin, and **only** for HTTPS → HTTPS.
- Does not send anything if navigating to a less secure protocol.

---

### **7. `strict-origin-when-cross-origin`**
- Same-origin → full URL  
- Cross-origin + HTTPS → sends only origin  
- Cross-origin + downgrade → sends nothing  
This is one of the most secure practical settings.

---

### **8. `unsafe-url`**
- Always sends full URL as referrer to all sites.
- **Not recommended**.

---

## Key Idea

> The stricter the policy, the less information your browser leaks to other websites.


# 3. Security Header: X-Content-Type-Options

## Threat

When a browser requests a resource, it includes an **Accept** header indicating what type of content it expects:

```
Accept: image/png
```

If a **Man-in-the-Middle attacker (MiTM)** tampers with the response and changes the content type, the browser might try to **guess (sniff)** the file type.  
For example:

- Browser expects: `image/png`
- MiTM sends back **HTML containing malicious script**
- Browser “sniffs” the content and decides:  
  *“This looks like HTML, I will execute it.”*

This can lead to:

- Malicious HTML execution  
- XSS-like attacks  
- Script injection  
- Unexpected rendering behavior  

---

## Solution — `X-Content-Type-Options: nosniff`

By setting this header to `nosniff`, we tell the browser:

> **Do not try to guess the content type. Only use the declared MIME type.**

This prevents browsers from executing or rendering files that do not match their expected MIME type.

---

## Usage Example (Express)

```js
app.use((req, res, next) => {
  res.setHeader("Referrer-Policy", "origin");
  res.removeHeader("X-Powered-By");
  res.setHeader("X-Content-Type-Options", "nosniff");
  next();
});
```

### Effect:
- Browser will refuse to run files whose content type does not match what was requested.
- Blocks MIME-type confusion attacks.
- Prevents attackers from injecting scripts disguised as images or other file types.

---

## Summary

`X-Content-Type-Options: nosniff` protects against:

- MIME type tampering  
- Content-type misinterpretation  
- Malicious HTML/script execution during file downloads  

It ensures the browser **never over-rides** the declared MIME type.

# 4. Security Header: X-XSS-Protection

`X-XSS-Protection` is a security header that enables or configures the browser’s **built-in XSS filtering mechanism**.

Older browsers (especially Internet Explorer and early versions of Chrome/Safari) had basic XSS filters that attempted to detect and block simple reflected XSS attacks.

---

## What This Header Does

- It turns on the browser's native XSS protection.
- If the browser detects reflected XSS in the URL or request, it may:
  - Block the page from loading, or
  - Sanitize the injected script

Example usage:

```
X-XSS-Protection: 1; mode=block
```

This tells the browser:

- Enable XSS filtering  
- If an attack is detected, **block the whole page** instead of trying to sanitize it  

---

## Modern Status

- Modern browsers rely heavily on **Content Security Policy (CSP)** instead.
- Chrome and other browsers have **deprecated** this header.
- Some browsers ignore it entirely now.

However, setting it does not break anything — it simply provides an **extra (legacy) layer of protection** for older browsers.

---

## When You Can Skip It

If your application has a strong CSP configuration, this header is typically not needed.

# 5. Security Header: HSTS (Strict-Transport-Security)

HSTS (HTTP Strict Transport Security) is a security mechanism that ensures a website is **always** accessed over HTTPS.  
It prevents users from accidentally or unknowingly accessing the insecure HTTP version of a site.

This protects against:

- Man-in-the-middle attacks  
- Protocol downgrade attacks  
- Session hijacking over HTTP  

---

## Why HSTS Is Needed

If a website supports both HTTP and HTTPS:

- A user may accidentally type `http://...`
- An attacker on public WiFi could downgrade or intercept the request
- The first HTTP request is vulnerable  

HSTS tells the browser:

> “From now on, always use HTTPS for this domain.”

---

## How It Works (Two Steps)

### **1. First Request (HTTP → HTTPS redirect by the server)**

If the first request comes through HTTP:

- The server redirects it to HTTPS using **301**  
- The server sends the **Strict-Transport-Security** header in the HTTPS response  

Example:

```
Strict-Transport-Security: max-age=31536000; includeSubDomains; preload
```

After this, the browser remembers the rule.

---

### **2. Subsequent Requests (Browser-handled redirect)**

From the next time onward:

- The browser detects any `http://` attempt internally  
- It **does NOT** send the HTTP request to the server  
- Instead, the browser silently upgrades the request to HTTPS  
- This internal redirect is represented as a **307 Internal Redirect** (browser-side only)

The server never receives the insecure request.

---

## Special Case: Preloaded HSTS Sites

Some major sites (e.g., PayPal, Google, Facebook) are included in the browser’s **HSTS Preload List**.

For these:

- Even the **very first** HTTP request never reaches the server  
- The browser automatically forces HTTPS immediately  
- This also shows as a **307 internal redirect**  

---

## Example Middleware

```js
const redirectToHttps = (req, res, next) => {
  if (req.headers["x-forwarded-proto"] !== "https") {
    // Redirect to HTTPS
    return res.redirect(["https://", req.get("Host"), req.url].join(""));
  }
  next();
};

app.use(redirectToHttps);

app.use((req, res, next) => {
  res.setHeader("Referrer-Policy", "no-referrer");
  res.removeHeader("X-Powered-By");
  res.setHeader("X-Content-Type-Options", "nosniff");

  // HSTS header
  res.setHeader(
    "Strict-Transport-Security",
    "max-age=31536000; includeSubDomains; preload"
  );

  next();
});
```

### What This Does:

- First request (HTTP) → server redirects to HTTPS  
- HTTPS response includes HSTS header  
- Future requests: browser auto-redirects to HTTPS before sending anything  

---

## Summary

- **HSTS enforces HTTPS for all future requests**  
- First request may need server redirect (unless site is preloaded)  
- Browser performs internal **307** redirects afterward  
- Protects against protocol downgrade and MiTM attacks  



![[Pasted image 20251211072545.png]]


