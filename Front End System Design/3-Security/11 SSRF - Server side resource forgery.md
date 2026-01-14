![[Pasted image 20251215195407.png]]
 # Server-Side Request Forgery (SSRF)

SSRF (Server-Side Request Forgery) is a vulnerability where an attacker tricks the **server** into making unintended requests on their behalf.

Instead of the attacker directly accessing restricted resources, the **server itself** performs the request using its internal permissions.

---

## What an Attacker Can Do with SSRF

By exploiting SSRF, an attacker can:

- Access **internal/private network resources**
- Steal sensitive data
- Perform unauthorized operations
- Interact with internal services (DB, internal APIs, metadata services)
- Abuse server trust boundaries

---

## Example Scenario

- A company exposes a **public website**.
- That website has access to the company’s **private network** (DBs, internal APIs).
- The server accepts a user-provided URL and fetches data from it.
- An attacker sends a crafted payload so the server fetches:
  - Internal resources
  - Private network services
  - Restricted endpoints

The attacker never accesses the internal network directly — the **server does it for them**.

---

## Common Causes of SSRF

### 1. Unvalidated User Input
If user input (like URLs) is not validated or sanitized, attackers can inject malicious destinations.

Example risk:
```js
const userUrl = req.query.url;
// Server blindly uses this URL
```

---

### 2. Lack of Whitelisting
If the server allows requests to **any domain**, attackers can redirect requests to internal services.

### Mitigation:
Only allow requests to **trusted, whitelisted domains**.

Example:
```js
const allowedDomains = ['api.example.com', 'internal-service.local'];

function isAllowedDomain(url) {
  const parsedURL = new URL(url);
  return allowedDomains.includes(parsedURL.hostname);
}
```

---

### 3. Insufficient Access Control
If there are no policies defining:
- What network resources can be accessed
- What internal services are allowed
- What DB endpoints are exposed

then SSRF impact increases significantly.

Using libraries like **Axios** or **node-fetch** (instead of low-level raw requests) helps enforce safer defaults and better control.

---

## Mitigation Techniques (From Your Notes)

- Validate and sanitize all user-provided URLs
- Enforce **domain whitelisting**
- Restrict internal network access via policies
- Avoid direct raw XML/HTML-based requests
- Use controlled HTTP clients (Axios, node-fetch)
- Apply strict access control rules

---

# XML External Entity (XXE)

XXE (XML External Entity) is a vulnerability that occurs when an application processes **untrusted XML input** and allows external entities to be resolved.

XML looks similar to HTML but has powerful features like **entities**, which can be abused.

---

## How XXE Works

An attacker submits malicious XML containing an external entity:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [
  <!ELEMENT foo ANY >
  <!ENTITY xxe SYSTEM "file:///etc/passwd" >
]>
<foo>&xxe;</foo>
```

If the XML parser is insecure:
- The external entity gets resolved
- The server reads sensitive files
- The contents may be returned in the response

---

## What XXE Can Lead To

- Reading local server files
- Disclosure of sensitive system data
- Internal service access
- In some cases, SSRF-like behavior

---

## Key Idea

- XML is **not just data** — it can reference external resources.
- If entity resolution is enabled, attackers can abuse it.
- This is especially dangerous in legacy systems or older XML parsers.

---

## Summary

- **SSRF**: Attacker makes the server send requests it should not
- **Root causes**: unvalidated input, no whitelisting, weak access control
- **XXE**: XML entities allow attackers to access internal files/resources
- Both exploit **server trust and internal access**

Proper validation, whitelisting, and secure parsers are essential to prevent these attacks.

