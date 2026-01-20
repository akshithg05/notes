![[Pasted image 20260118221849.png]]


LOCAL and SESSION storage - very important.
![[Pasted image 20260119065442.png]]


[[2026-01-20]]

### Overview

![[namastedev.com_learn_namaste-frontend-system-design_database-caching-overview.png]]

## Caching Overview (Frontend Perspective)

Caching is a performance optimization technique used to store data temporarily so that future requests can be served faster without recomputing or refetching the data.

In frontend applications, caching can happen at **multiple levels**, mainly inside the **browser** and **application state**.

---

## Browser-Level Caching (3 Levels)

### 1. HTTP Caching
- Managed automatically by the browser
- Controlled using response headers sent by the server
- Examples of headers:
  - Cache-Control
  - Expires
  - ETag
  - Last-Modified
- Best for:
  - Static assets (JS, CSS, images, fonts)
  - Reducing network calls
- Happens **between Server ↔ Browser**

---

### 2. Service Worker Caching
- Runs between the browser and the network
- Gives developers full control over caching logic
- Can intercept requests and responses
- Enables:
  - Offline support
  - Advanced caching strategies (cache-first, network-first, stale-while-revalidate)
- Commonly used in:
  - PWAs (Progressive Web Apps)

---

### 3. API Caching (Browser Side)
- Caching API responses on the client
- Usually implemented using:
  - Fetch cache
  - Service workers
  - Data-fetching libraries
- Reduces repeated API calls
- Improves perceived performance

---

## Application-Level Caching (State Management)

Caching can also happen **inside the application**, typically using state management or data-fetching libraries.

Examples:
- Redux
- React Query / TanStack Query
- SWR
- Zustand

What gets cached:
- API responses
- Derived or computed data
- User session data

Benefits:
- Avoids unnecessary re-fetching
- Faster UI updates
- Better user experience

---

## High-Level Summary

- HTTP Cache → Automatic, browser-controlled
- Service Worker → Developer-controlled, powerful
- API Cache → Optimizes repeated network calls
- State Cache → Application-level performance boost

Caching works best when **multiple layers are combined intelligently**.


### Databases

![[namastedev.com_learn_namaste-frontend-system-design_database-caching-overview 1.png]]

