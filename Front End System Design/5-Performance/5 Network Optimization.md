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


