![[namastedev.com_learn_namaste-frontend-system-design_rendering-pattern.png]]

Rendering patterns define **where and when** the UI is rendered — on the client, on the server, or a mix of both.  
The code structure may look similar, but the **rendering strategy and data flow differ**.

---

## a. Client-Side Rendering (CSR)

- Rendering happens entirely in the **browser**
- Server sends minimal HTML + JS bundle
- JS executes, fetches data, then renders UI

Characteristics:
- Slower initial load
- Heavy JS execution on client
- Suitable for dashboards and highly interactive apps

---

## b. Server-Side Rendering (SSR)

Rendering happens on the **server** and HTML is sent to the browser.

### Dynamic SSR
- HTML is generated **on every request**
- Fresh data per request
- Slightly higher server load

Use case:
- Personalized pages
- Authenticated user content

---

### c. Static Site Generation (SSG)

- HTML is generated **at build time**
- Served as static files
- Extremely fast and cache-friendly

Use case:
- Blogs
- Marketing pages
- Documentation sites

---

## d. React Server Components (RSC)

- Hybrid approach combining **CSR and SSR**
- Some components render on the server
- Some components render on the client
- Reduces JS sent to browser
- Improves performance and scalability

Result:
- Less client-side JavaScript
- Faster initial loads
- Better performance for large apps

---

## Next.js (Short Intro)

Next.js is a React framework that supports:
- Client-Side Rendering (CSR)
- Server-Side Rendering (SSR)
- Static Site Generation (SSG)
- React Server Components (RSC)

It provides built-in routing, data fetching, and performance optimizations.

---

## Important Next.js Notes

- Use **App Router** (`app/` directory)
- App Router is the modern and recommended approach
- Supports React Server Components by default
- Page Router (`pages/`) is older and less flexible

---

## Key Takeaway

- Same React code, different rendering strategies
- Choose rendering pattern based on performance, SEO, and UX needs
- Next.js enables mixing these patterns efficiently


# 1. Client side rendering

![[Pasted image 20260113071148.png]]


## Page Routing & Client-Side Rendering (CSR Flow)

### Page Routing (Next.js – Pages Router)
- Any file created inside the `pages/` folder automatically becomes a route.
- Example:
  - `pages/index.js` → `/`
  - `pages/profile.js` → `/profile`

Routing is file-based and handled by the framework.

---

## Why Page Routing Uses Client-Side Rendering (CSR)

In this model, the server does **not** send fully rendered content. Instead, it sends a basic HTML shell and relies on JavaScript in the browser to complete rendering.

---

## High-Level CSR Rendering Flow

1. **HTML from Server**
   - Browser requests the page
   - Server responds with a basic HTML file
   - HTML contains script tags pointing to JS bundles

2. **JS, CSS, Images Download**
   - Browser downloads JavaScript bundles, CSS, and static assets
   - React code executes in the browser

3. **Hydration**
   - HTML is already present, but it is static
   - Hydration attaches event listeners and React logic to the existing DOM
   - Makes the page interactive (clicks, inputs, state updates)
   - Rendering alone is not enough — hydration is required for interactivity

4. **API Calls**
   - After hydration, components trigger API requests
   - Data is fetched from backend services
   - Additional assets (images, etc.) may be loaded

5. **Final Render**
   - UI updates with fetched data
   - Page becomes fully usable

---

## Notes on Hydration Timing
- Hydration usually starts after initial render
- In some apps, hydration can be delayed or partial
- Interactivity depends on hydration completion

---

## Key Takeaway
- CSR relies heavily on browser-side JavaScript
- Initial load involves multiple network requests
- Performance depends on bundle size, hydration cost, and API speed
