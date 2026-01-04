# Security Testing (Frontend Perspective)

As a frontend engineer, it is important to **understand common security threats**, even though **security testing is generally not the primary responsibility of developers**.

Having basic security testing knowledge helps in:
- Identifying vulnerabilities early
- Writing safer frontend code
- Collaborating better with security teams

---

## Security Testing & Penetration Testing

Security testing focuses on identifying vulnerabilities that attackers could exploit.

One common approach is **penetration testing (pentesting)**, where tools simulate real-world attacks to uncover weaknesses.

---

## Burp Suite

**Burp Suite** is a popular tool used for penetration testing.

### How Burp Suite Works
- Acts as a **proxy (middleman)** between:
  - The browser
  - The server
- Intercepts and inspects:
  - Requests
  - Responses
  - Headers
  - Payloads

This allows testers to:
- Modify requests
- Replay requests
- Analyze security behavior

---

## HTTP vs HTTPS Testing

- Burp Suite works easily with **HTTP** applications.
- For **HTTPS** applications:
  - A **Burp-generated certificate** must be installed in the browser
  - This allows Burp to decrypt and inspect HTTPS traffic
- Without installing the certificate, HTTPS traffic cannot be intercepted.

---

## Key Takeaway

> Security testing tools like Burp Suite help simulate real attacks by acting as a proxy between the browser and server, enabling detection of vulnerabilities.

---

## Summary

- Security testing awareness is important for frontend engineers
- Burp Suite is commonly used for pentesting
- Acts as a proxy between browser and server
- HTTPS testing requires installing certificates

