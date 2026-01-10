# Network Optimization — Critical Rendering Path (CRP)

Network optimization is a **knowledge-heavy but extremely important** part of frontend performance.  
One of the most critical concepts is the **Critical Rendering Path**.

---

## Topics Covered in This Section (Overview)

1. Critical Rendering Path  
2. Async / Defer loading of JavaScript  
3. Minimizing HTTP requests  
4. Avoiding redirections  
5. Resource Hinting  
6. Fetch Priority  
7. HTTP versions (HTTP/1.1 vs HTTP/2 vs HTTP/3)  
8. Compression (Brotli / Gzip)  
9. HTTP caching  
10. Caching using Service Workers  

---

# 1. Critical Rendering Path (CRP)

The **Critical Rendering Path** describes the sequence of steps the browser follows to **convert HTML, CSS, and JavaScript into pixels on the screen**.

---

## How the Browser Processes Resources

When the browser makes a request to the server:

- The response is received in **packets**
- As soon as packets arrive, the browser starts processing them

### HTML
- If a packet contains **HTML**, the browser starts parsing it
- This leads to the creation of the **DOM (Document Object Model)**

### CSS
- If a packet contains **CSS**, the browser starts parsing it
- This leads to the creation of the **CSSOM (CSS Object Model)**

### JavaScript
- JavaScript is parsed and executed by the browser
- DOM and CSSOM are combined with JS execution results

---

## Render Tree Creation

- DOM + CSSOM → **Render Tree**
- Once the render tree is ready, the browser can:
  - Layout elements
  - Paint pixels on the screen

---

## Blocking Behavior (Very Important)

### CSS is Render-Blocking
- Rendering **cannot complete** until CSS is downloaded and parsed
- Browser waits for CSSOM before painting

---

### JavaScript is Parsing-Blocking
- When the browser encounters a `<script>` tag:
  - HTML parsing **pauses**
  - JavaScript is executed
  - HTML parsing resumes afterward

This is why uncontrolled JS loading can delay page rendering.

---

## The 14KB First Packet Rule

- The **first packet** sent from server to browser is approximately **14 KB**
- If critical HTML, CSS, and minimal JS fit within this first packet:
  - Browser can create an initial render tree
  - Something meaningful can be rendered quickly

This improves:
- **FCP (First Contentful Paint)**
- Perceived performance

---

## Why This Matters

If the browser can render **something quickly**:
- Users feel the page is fast
- Bounce rate reduces
- Performance metrics improve

> Faster CRP → Faster FCP → Better UX

---

## Key Takeaway

> Optimizing the Critical Rendering Path helps the browser render meaningful content as early as possible, directly improving perceived performance.

---

# 2. Minimizing Network Requests & Async JavaScript

---

## 2. Minimizing Network Requests

More network requests usually mean:
- Higher **latency**
- Slower **UX**
- Worse **performance metrics**

> In many cases, **5 requests of 2 KB** can be slower than **1 request of 10 KB**, due to connection overhead.

---

## Why Too Many Requests Are Slow

Each network request has overhead:
- TCP handshake
- SSL/TLS negotiation
- DNS lookup
- Browser connection limits

### Browser Limits
- Browsers allow **~6–10 parallel requests per domain**
- Extra requests are **queued**, delaying loading

---

## Optimization Strategies (For Critical Rendering Path)

### 1. Inline Critical CSS
- Inline only **critical CSS** required for above-the-fold content
- Avoid large inline styles; rest can be external

### 2. Inline Critical JavaScript
- Only for **critical render logic**
- Non-critical JS should be external and deferred

### 3. SVG Instead of `<img>`
- SVGs can be:
  - Inlined
  - Styled with CSS
  - Avoid extra network requests

### 4. Base64 Images (Use Carefully)
- Useful for **very small assets**
- Avoid for large images (increases HTML size)

---

## Important Caveat ⚠️

> These optimizations are **only for the initial load (FCP)**.

- Do **not inline everything**
- Keep non-critical JS and CSS in separate files
- Balance readability, caching, and performance

---

## Example Pattern

```html
<style>
  /* Inline only critical CSS */
</style>

<script defer src="./index.js"></script>
```

- CSS inline → Faster render
- JS deferred → No parser blocking

---

## Async JavaScript

### Default Script Behavior (Bad for Performance)

```html
<script src="app.js"></script>
```

- HTML parsing **stops**
- JS downloads and executes
- HTML parsing resumes after execution
- **Parser-blocking**

---

## `async` Script

```html
<script async src="app.js"></script>
```

### Behavior:
- JS downloads **in parallel** with HTML parsing
- When JS finishes downloading:
  - HTML parsing **pauses**
  - JS executes
  - HTML parsing resumes

### Key Points:
- Execution order **not guaranteed**
- Useful for **independent scripts**
- Can still interrupt rendering

---

## `defer` Script (Recommended for Most Cases)

```html
<script defer src="app.js"></script>
```

### Behavior:
- JS downloads **in parallel** with HTML parsing
- HTML parsing completes first
- JS executes **after DOM is fully parsed**

### Key Points:
- Execution order **preserved**
- No parser blocking
- Best choice for most application scripts

---

## Async vs Defer — Summary

| Feature | async | defer |
|------|------|------|
| Downloads in parallel | ✅ | ✅ |
| Blocks HTML parsing | ⚠️ (during execution) | ❌ |
| Execution order guaranteed | ❌ | ✅ |
| Runs after DOM ready | ❌ | ✅ |

---

## Final Takeaways

- Reduce network requests for faster FCP
- Inline only **critical** CSS/JS
- Use **SVGs** where possible
- Prefer `defer` for application JavaScript
- Use `async` only for truly independent scripts

---


# 3. Network Optimization — Redirects & Resource Hinting

---

## Avoid Redirections

Redirections add **extra network hops**, increasing latency and slowing down page load.

### HTTP → HTTPS Redirection Problem
- If a user enters `http://example.com`
- Browser first hits HTTP
- Server redirects (301/302) to HTTPS
- Extra round trip = slower load

### Optimized Approach (HSTS Preload)
- Using **HSTS preload**, the browser already knows the site is HTTPS-only
- Browser upgrades request to HTTPS **before** sending it
- HTTP request never reaches the server

### How It Works
- Site is registered at **hstspreload.org**
- Browser ships with a preloaded HSTS list
- Automatic HTTPS upgrade at browser level

✅ Improves performance  
✅ Improves security  

---

## Resource Hinting

Resource hinting helps the browser **prepare early** for resources that will be needed later.

Problem:
- Resources are discovered late (fonts via CSS, images via API, third-party JS)
- Each discovery triggers DNS lookup + TLS + request
- Delays rendering and interaction

Solution:
- Tell the browser **in advance** what it should prepare for

---

## Types of Resource Hints

### 1. `preconnect`
Establishes early connection (DNS + TCP + TLS) to a domain.

```html
<link rel="preconnect" href="https://cdn.example.com" crossorigin />
```

Best for:
- Third-party APIs
- CDNs
- Fonts

---

### 2. `dns-prefetch`
Performs only DNS lookup in advance.

```html
<link rel="dns-prefetch" href="https://cdn.example.com" />
```

Best for:
- Low-priority third-party domains

---

### 3. `preload`
Fetches a **critical resource early** with high priority.

```html
<link rel="preload" href="/hero-image.png" as="image" />
```

Best for:
- Hero images
- Fonts
- Critical CSS/JS

---

### 4. `prefetch`
Fetches resources needed in the **near future** with low priority.

```html
<link rel="prefetch" href="/next-page.js" />
```

Best for:
- Next page navigation
- Likely user actions

---

### 5. `prerender`
Loads an entire page and its dependencies in the background (hidden).

```html
<link rel="prerender" href="/dashboard" />
```

⚠️ Heavy operation — use carefully

---

## Key Takeaways

- Avoid redirects using **HSTS preload**
- Use `preconnect` for critical third-party domains
- Use `dns-prefetch` for low-priority domains
- Use `preload` only for **critical render path**
- Use `prefetch` for **future navigation**
- Resource hints run **in parallel with HTML parsing**

---

# 4. Resource Hint Priority (fetchpriority)

`fetchpriority` allows us to tell the browser how important a resource is during page load so that critical resources are not delayed by non-critical ones.

### Why fetchpriority is needed
Not all resources are equally important. Some are required for first paint and interaction, while others (images, analytics, secondary scripts) can be delayed. Without priority hints, the browser may waste bandwidth on low-value resources early.

---

### Using fetchpriority with scripts
Non-critical scripts should be deprioritized so they do not block important resources.

Example:
<link rel="preload" href="/js/script.js" as="script" fetchpriority="low">

---

### Preloading CSS without blocking rendering
CSS is render-blocking by default. We can preload it without blocking HTML parsing and apply it after loading.

Example:
<link rel="preload" as="style" href="theme.css" fetchpriority="low" onload="this.rel='stylesheet'">

What this does:
- CSS downloads early
- HTML parsing is not blocked
- Styles are applied only after the file is ready

---

### Using fetchpriority with images
Images that are below the fold should be loaded with lower priority.

Example:
<img src="image.jpg" fetchpriority="low">

This prevents images from delaying HTML, CSS, or critical JavaScript.

---

![[Pasted image 20260110084845.png]]
![[Pasted image 20260110084859.png]]

### Summary
- fetchpriority="high" → critical resources
- fetchpriority="low" → non-critical resources
- Helps improve FCP and LCP
- Gives the browser better control over download scheduling
