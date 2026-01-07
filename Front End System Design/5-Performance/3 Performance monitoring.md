
# 1. Basics
Performance metrics help us measure how fast, responsive, and stable a website feels to users.

Just like humans have vital signs, websites also have **Web Vitals**.


---
![[Pasted image 20260107074646.png]]

## 1. Core Web Vitals

Core Web Vitals are a set of **user-centric performance metrics** defined by Google to measure real-world user experience.

---

### 1. Largest Contentful Paint (LCP)
- Measures the time taken for the **largest visible content element** to load.
- Calculated from the **start of page load**.
- Represents when the user actually sees most of the page, happens usually when images are loaded on to the screen.

> Lower LCP = faster perceived load time

---

### 2. First Input Delay (FID)
- Measures the delay between:
  - A user’s **first interaction** (click, tap, key press)
  - And the browser’s response to that interaction
- Happens **during page load**
- Not related to API response time

> Lower FID = better interactivity

---

### 3. Cumulative Layout Shift (CLS)
- Measures **visual instability** on the page.
- Occurs when elements unexpectedly move or shift.
- Common causes:
  - Images without fixed dimensions
  - Ads loading late
  - Dynamic content pushing layout

Important:
- CLS is calculated over the **entire lifecycle of the page**
- Not a one-time measurement

> Lower CLS = more stable UI

---

### 4. First Contentful Paint (FCP)
- Measures the time from page load start to the **first visible content** rendered on the screen.
- Indicates when users first see something meaningful.

> FCP shows *something is loading*, LCP shows *most content is ready*

---
![[Pasted image 20260107074659.png]]
## Summary

- Core Web Vitals focus on **real user experience**
- Key metrics:
  - LCP → Loading experience
  - FID → Interactivity
  - CLS → Visual stability
  - FCP → First visible content
- These metrics are critical for:
  - UX
  - SEO
  - Performance optimization

---

# 2. Detailed view of metrics
## 1. FCP and LCP

![[Pasted image 20260107074901.png]]

## 2.  More on CLS (Cumulative Layout Shift)

**Cumulative Layout Shift (CLS)** measures how much the **visible content shifts unexpectedly** during the user’s time on a page.

---

## Example Scenarios

- The page loads and the user starts reading content.
- Later, an **ad banner** appears at the top.
- The existing content is pushed downward.
- Images load late and cause sections to shift.
- While scrolling, additional ads or images appear and move content again.

Each of these is an **independent layout shift event**.

---

## How CLS Is Calculated

- CLS is the **sum of all individual layout shifts**
- It is measured across the **entire lifecycle of the page**
- Not limited to initial page load

Even small shifts add up over time and increase the CLS score.

---

## Why CLS Is Important

- Layout shifts frustrate users
- Users may click the wrong elements
- Reading experience is disrupted

> Lower CLS = more stable and predictable UI

---

## 3. Monitoring Performance Metrics

To monitor performance metrics:

- Open **Chrome DevTools**
- Go to the **Performance** tab
- Reload the website
- Analyze the timeline and metrics shown

This helps visualize:
- Loading
- Rendering
- Script execution
- User interactions

---

## 4. Limitations of Existing Metrics

Even though Core Web Vitals exist, **performance is more than just initial load**.

Example concern:
- **FID** measures only the *first* user interaction.
- It does not account for:
  - Later clicks
  - Keyboard interactions
  - Scrolling
  - API-driven UI updates

A performant app should remain **smooth throughout its entire lifecycle**, not just during initial load.

---

## 5. INP (Interaction to Next Paint)

**INP** is a newer performance metric designed to address these gaps.

### What INP Measures
- Tracks **all user interactions** (clicks, taps, key presses)
- Measures the delay from:
  - User interaction
  - To the **next visual update (paint)**
- Considers interactions across the **entire session**

---

### How INP Is Calculated
- Among all interactions, the **worst (slowest) interaction delay** is used
- That value becomes the INP score

> Lower INP = smoother and more responsive application

---

## Why INP Matters

- Reflects real-world interactivity
- Captures performance beyond first load
- Helps identify UI jank and slow interactions

---

## Key Takeaway

> INP provides a more accurate picture of user experience by measuring interaction responsiveness throughout the page lifecycle.


### "If we cannot measure something we will not be able to improve it"

We can use tools like lighthouse as well for performance metrics,

![[Pasted image 20260107082436.png]]

# 3. Types of Performance Metrics

Performance metrics can broadly be divided into **two categories** based on what they measure and who they matter to.

---

## 1. Browser-Centric Metrics

These metrics are focused on **loading, rendering, and network behavior** from the browser’s point of view.

- More technical in nature
- Mostly number-driven (time, size, counts)
- Useful for identifying **technical and infrastructure issues**

### When to Use
- Debugging performance bottlenecks
- Optimizing loading processes
- Diagnosing network or server delays

### Common Browser-Centric Metrics
- **TTFB (Time to First Byte)**  
  Time taken for the first byte to arrive from the server  
  Depends on network latency and server response time

- Network request timing
- DNS resolution time
- DOMContentLoaded
- Page load time

---

## 2. User-Centric Metrics

These metrics focus on **how fast and smooth the website feels to users**.

- Measure perceived performance
- Directly impact UX
- Monitored continuously while the user interacts with the site

### When to Use
- Improving user experience
- Reducing frustration and bounce rate
- Ensuring smooth interactions across the entire session

### Common User-Centric Metrics
- **FCP (First Contentful Paint)**
- **LCP (Largest Contentful Paint)**
- **CLS (Cumulative Layout Shift)**
- **INP (Interaction to Next Paint)**
- **FID (First Input Delay)**
- **Total Blocking Time (TBT)**  
  Time between FCP and when the page becomes fully interactive

---

## Key Insight

- Browser-centric metrics help find **technical problems**
- User-centric metrics help improve **real user experience**
- Both are important and complement each other

---

## 7. Performance Budget (Very Important)

Performance optimization has **no natural end**.

Without limits:
- Teams may over-optimize
- Time and resources can be wasted

**Always define a performance budget**:
- Target load times
- Acceptable interaction delays
- Bundle size limits

> A performance budget helps balance performance gains with development effort.

