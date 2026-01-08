# Performance Tools

> **Performance always comes with a cost**, so it is important to **prioritize** what to measure and optimize.

Performance tools can be grouped based on **who is consuming the data** and **how the data is collected**.

---

## 1. Developer Mode (Local / Lab Testing)

Used mainly by developers during development to **identify bottlenecks and delays**.

### a. Lighthouse
- Helps audit and optimize performance
- Identifies issues related to:
  - LCP
  - CLS
  - FCP
  - Best practices
  - Accessibility
- Provides actionable suggestions

---

### b. Network Tab (Chrome DevTools)
Used to analyze network-level issues.

Key parameters:
- Request status
- Protocol (HTTP/HTTPS)
- Priority
- Individual request timing
- Total network time
- SSL / TLS time

---

### c. Performance Tab (Chrome DevTools)
- Records page load and interactions
- Shows:
  - Rendering
  - Scripting
  - Layout
  - Painting
- Useful for deep debugging of performance issues

---

### Rules / Best Practices While Testing
- Run Lighthouse in **Incognito mode**
- Keep DevTools in a **separate window**, not docked
- Select correct **device type** (mobile / desktop)
  - Mobile has lower RAM and CPU
  - Results differ significantly

---

## 2. Simulated Data (Mock / Lab Data)

Used to simulate performance under controlled conditions.

### a. WebPageTest (webpagetest.org)
- Very powerful for simulated testing
- Allows testing with:
  - Different devices
  - Different locations
  - Different network speeds
- Provides detailed metrics and visual analytics

---

## 3. Real User Data (Field Data)

Collected from **actual users** interacting with the website.

---

### a. CrUX (Chrome User Experience Report)
- Contains performance data from a **large set of real Chrome users**
- Aggregated and anonymized data
- Used by Google and third-party tools
- Reflects **real-world Chrome user experiences**

✔ Your understanding is correct:  
CrUX tracks **Chrome-based real user performance data** at scale.

---

### b. PageSpeed Insights (pagespeed.web.dev)
- Combines:
  - User-centric metrics (field data from CrUX)
  - Browser-centric metrics (lab data)
- Reports:
  - LCP
  - FCP
  - CLS
  - INP
  - TTFB

---

### c. RequestMetrics
- Collects performance metrics from **your own application**
- Useful for monitoring real production traffic

---

### d. Microsoft Clarity (clarity.microsoft.com)
- Similar to Google Analytics
- Requires inserting a script
- Tracks:
  - User behavior
  - Performance insights
  - Session recordings and heatmaps

---

### e. New Relic
- Enterprise-grade performance monitoring
- Tracks frontend and backend metrics
- Very powerful but comes with cost

---

### f. Sentry
- Primarily error tracking
- Also provides performance monitoring
- Helps correlate performance issues with errors

---

### g. Google Analytics
- Tracks user behavior and engagement
- Can be combined with performance metrics
- Useful for understanding performance impact on business KPIs

---

## Key Takeaway

- **Developer tools** → find technical issues early
- **Simulated data tools** → test controlled scenarios
- **Real user data tools** → understand real-world experience
- Always prioritize metrics based on **business impact and cost**

> Performance optimization should be data-driven, not assumption-driven.

```
