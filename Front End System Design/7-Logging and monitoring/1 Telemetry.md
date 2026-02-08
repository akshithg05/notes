
![[namastedev.com_learn_namaste-frontend-system-design_telemetry 1.png]]

## What is Telemetry?
Telemetry is the process of:
1. Collecting data from an application
2. Classifying and analyzing that data

The goal is to understand:
- Performance
- Errors
- User behavior
- Resource usage
- Feature adoption

Telemetry helps teams observe how the system behaves in real-world usage.

---

## Why Telemetry is Important
- Identify performance bottlenecks
- Detect errors and failures early
- Understand user behavior
- Improve UX and system design
- Make data-driven decisions

---

## Types of Data Collected in Telemetry

### 1. Performance Metrics
Performance metrics help measure how fast and smooth the application is.

Examples:
- Web Vitals:
  - FCP (First Contentful Paint)
  - LCP (Largest Contentful Paint)
  - CLS (Cumulative Layout Shift)
  - FID (First Input Delay)
- API response time
- Feature or scenario execution time
- Page load time
- Resource loading time (JS, CSS, images)

Other performance indicators:
- Paint timings
- Network latency
- Frame rate (FPS)
- Frame drops
- Long tasks blocking the main thread

These metrics help identify bottlenecks and improve performance.

---

### 2. Resource Errors
Resource errors indicate when something is broken in the system.

Examples:
- 5xx server errors
- 4xx client errors
- API failures
- Network errors (offline scenarios)
- Client-side JavaScript exceptions

Example:
- A “+” button on an e-commerce app fails due to a JS error
- Without telemetry, such issues may go unnoticed

Capturing console errors and exceptions is critical for reliability.

---

### 3. User Interaction Data
User interaction telemetry helps understand how users interact with the app.

Examples:
- Clicks (which components are used the most)
- Scroll depth (how far users scroll)
- Form interactions:
  - Submission rates
  - Drop-off points
- Browser events:
  - Mouse clicks
  - Touchpad events
  - Keyboard events
  - Accessibility interactions

This data helps improve UI/UX design decisions such as:
- Icon vs text
- Button placement
- Layout changes

---

### 4. Resource Utilization
Tracks how much system resources are being used.

Examples:
- CPU utilization
- Memory usage
- Browser resource consumption

Usually visualized using dashboards and SLIs.

---

### 5. Custom Events
Custom events are business-specific metrics defined by the team.

Examples:
- Purchases
- “Buy” button clicks
- Feature usage counts
- Login methods:
  - Gmail login
  - LinkedIn login
  - Email/password login

Any meaningful user or business action can be tracked as a custom event.

---

## Dashboards & Monitoring
All telemetry data can be visualized using dashboards:
- Performance dashboards
- Error dashboards
- User behavior dashboards
- Business metrics dashboards

Dashboards help teams monitor system health in real time.

---

## Popular Telemetry & Monitoring Tools

### 1. Microsoft Clarity
- Open-source
- Session replays
- Heatmaps
- User behavior insights

### 2. Google Analytics
- Powerful reporting
- User behavior tracking
- Traffic analysis
- Conversion metrics

### 3. Sentry
- Error tracking
- Exception monitoring
- Performance monitoring

### 4. LogRocket
- Session replay
- See exactly what users did
- Debug issues visually

### 5. OpenTelemetry
- Open standard for telemetry
- Metrics, logs, and traces
- Vendor-agnostic observability

---

## Key Takeaway
Telemetry provides visibility into performance, errors, user behavior, and system health by collecting and analyzing structured application data.

---

## One-Line Interview Summary
Telemetry is the collection and analysis of performance metrics, errors, user interactions, and custom events to observe, monitor, and improve system behavior.
