# Subresource Integrity (SRI)

![alt text](image.png)


Subresource Integrity (SRI) is used to ensure that **external resources loaded by your application have not been tampered with**.  

Even if a domain is trusted, the **resource itself** might be compromised.

---
## The Core Problem  

Consider:
- Your application is hosted on **a.com**
- You load external resources from **b.com** (CDN, third-party domain)

You may trust:
- The domain (`b.com`)
- The CORS or CSP configuration

But:
- The CDN can be hacked
- The resource file can be modified
- Malicious code can be injected

So trusting the **domain alone is not enough**.

  

---
## How SRI Solves This

When loading an external resource, you attach an **integrity attribute** containing a cryptographic hash of the expected file.
Example:

```html

<link

  href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css"

  rel="stylesheet"

  integrity="sha384-T3c6CoIi6uLrA9TneNEoa7RxnatzjcDSCmG1MXxSR1GAsXEV/Dwwykc2MPK8M2HN"

  crossorigin="anonymous"

/>

```

The hash acts as a **fingerprint** of the resource.

  

---

  

## How the Browser Verifies the Resource

  

1. Browser downloads the resource from the CDN  
2. Browser generates a **cryptographic hash** (SHA-256 / SHA-384 / SHA-512)  
   - Based on the **content + hashing algorithm**
1. Browser compares the generated hash with the value in the `integrity` attribute  
2. Resource is loaded **only if the hashes match**  
  

If the hashes do not match:
- The resource is **blocked**
- It is **not executed or applied**
---
## Why This Works

  
- The hash is the **source of truth**
- Any change in the file (even 1 character) changes the hash
- If the CDN resource is modified or hacked, the integrity check fails


This guarantees that:

> The resource loaded by the browser is **exactly the same** as the one you intended to load.

---
## Key Idea

- You may trust a domain
- But **SRI ensures you trust the exact resource**
- Protects against compromised CDNs and supply-chain attacks
---
## Summary

  

- SRI protects external scripts and stylesheets

- Uses cryptographic hashes (`sha256`, `sha384`, `sha512`)

- Browser validates resource integrity before execution

- Prevents tampered or malicious external resources from loading

  

### Benefits

  

1. **Detects Compromised Third-Party Resources**  

   If a third-party CDN resource is compromised or tampered with, the computed hash will not match the expected integrity value, and the browser will block the resource.

  

2. **Detects Unexpected Content Changes**  

   If the content of an external resource changes (even a small change), the hash changes.  

   This helps identify updates that may:

   - Break your application

   - Introduce unexpected behavior

   - Modify trusted code without notice

  

---

  

## Integrity Hash Generation

  

- The `integrity` value is generated using a cryptographic hash (e.g., `sha256`, `sha384`, `sha512`).

- Tools like **SRI hash generators** can be used to compute this hash.

- As long as:

  - The resource content is the same

  - The integrity hash is the same  

  the browser will load and apply the resource.

  

---

  

## `crossorigin="anonymous"`

  

When using SRI with cross-origin resources, the attribute below should be added:

  

```html

crossorigin="anonymous"

```

  

This ensures:

- The resource is fetched **without credentials**

- The browser can correctly perform the integrity check

- Avoids CORS-related issues with SRI

  

---

  

## What Happens If Integrity Check Fails

  

If the computed hash does not match the integrity attribute:

- The browser **blocks the resource**

- The resource is **not executed or applied**

- An error is shown in the browser console, like the one in the screenshot

  

This prevents unsafe or altered resources from affecting the application.

## How Do We Know the Resource Isn’t Already Tampered When Generating the SRI Hash?
  

**Short answer:**  

👉 We don’t cryptographically know — this is a **trust-on-first-use** model.

---
## The Practical Reality

  

When you first generate an SRI hash, you are **implicitly trusting the source at that moment**.

  

Typically, the hash is generated when:


- The resource comes from a **well-known, reputable CDN**  
  (e.g., jsDelivr, Cloudflare, Google CDN)
- The resource is fetched over **HTTPS**
- The library version is **official and documented**


At this point, you assume:

> “This is the correct, intended version of the library.”

  

You then **freeze that trust** by generating the SRI hash.

---


## One-Line Summary (Interview-Ready)

  

> **SRI is based on trust-on-first-use — you trust the resource once, generate the hash, and from then on the browser guarantees the resource can never change silently.**

  

This is exactly why SRI is so powerful in real-world security.