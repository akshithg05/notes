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


[[2026-01-14]]
# 2. Server-Side Rendering (SSR)

### What happens in SSR
- The client makes a request to the server
- The **server generates the HTML** (including data fetched from APIs)
- The fully rendered HTML is sent to the browser
- The browser’s main job is **hydration**

In SSR, most of the heavy lifting (data fetching + HTML generation) happens on the **server**, not the browser.

---

### Why hydration is still needed
- The server can generate HTML but **cannot attach event listeners**
- Interactions (clicks, inputs, state changes) only work in the browser
- Hydration attaches React’s event listeners to the server-rendered DOM
- This makes the page interactive

So:
- Server → renders HTML
- Browser → hydrates HTML

---

### CSR vs SSR (Conceptual Difference)

**CSR flow**
1. HTML shell from server
2. JS, CSS, images downloaded
3. Hydration happens
4. API calls from browser
5. Data rendered on client

**SSR flow**
1. Request to server
2. Server makes API calls
3. Server generates full HTML
4. HTML sent to browser
5. Browser hydrates only

---

### Hooks and State in SSR
- Hooks like `useState`, `useEffect` are **client-side concepts**
- They are used in CSR for client-side data fetching and state updates
- In SSR, data is fetched **before render**, so:
  - No `useEffect` for data fetching
  - Data is passed using **props**
- Components remain mostly the same, but **data source changes**

---

## Example: CSR vs SSR in Next.js

### CSR Page (Client-Side Rendering)
- Data fetched in the browser
- Uses `useState` and `useEffect`

Key points:
- Initial render happens without data
- API call happens after hydration
- Slower first meaningful paint for data-heavy pages

---

### SSR Page (Server-Side Rendering)
- Data fetched on the server
- Passed to component as props

`getServerSideProps`:
- Runs **on the server**
- Executes on **every request**
- Fetches data and returns it as props
- Ensures fresh data per request

Key points:
- HTML already contains data
- Faster initial render
- Better SEO and perceived performance

---

### getServerSideProps (Next.js)
- Provided by Next.js
- Runs only on the server
- Executes on every request
- Used for dynamic, request-specific data

Returns:
- An object with `props`
- These props are injected into the page component

---

### Key Takeaways
- SSR shifts work from browser to server
- Faster first paint and better SEO
- Browser handles hydration only
- CSR uses hooks for data fetching
- SSR relies on server-side data + props


- In Server-Side Rendering, **too much logic on the server** can delay HTML generation.
- If the server spends a long time fetching data or running heavy computations:
  - The **HTML response is delayed**
  - **First Contentful Paint (FCP)** becomes slow
- In such cases, the browser receives **nothing to render** until the server finishes.

### Side Note: Over-optimizing SSR Can Hurt Performance

- Balance what runs on the server vs the client
- Server: critical data needed for initial render
- Client: non-critical data, interactions, secondary features
- Always evaluate:
  - FCP
  - Server response time
  - Overall user-perceived performance

# 3.  Static Site Generation (SSG)

### What is SSG?
Static Site Generation means **HTML is generated at build time**, not on every request.
The generated HTML is stored as a **static file** and served directly to the browser.

- No server-side computation on each request
- Browser receives **ready-to-render HTML**
- Only **hydration** happens on the client

---

### When to Use SSG
Use SSG when:
- Content is **same for all users**
- Content **does not change frequently**
- Pages are mostly **informational**

**Examples:**
- Blogs
- Documentation
- Articles
- Marketing pages
- Help pages

---

### SSG Flow (High Level)
1. During build time:
   - API calls are made
   - HTML is generated
   - JS and CSS bundles are created
2. Generated HTML is stored (static files / CDN)
3. Browser request:
   - HTML is served instantly
   - Hydration happens on client
4. No server work at request time

➡️ **Very fast FCP and LCP**

---

### SSG vs SSR
**SSG**
- Build-time rendering
- Extremely fast
- Best for static content
- Rebuild required for updates

**SSR**
- Rendered on every request
- Needed for dynamic, user-specific data
- More server cost
- Slower than SSG

---

### Next.js Support for SSG
In Next.js, SSG is enabled using:

- `getStaticProps()`

This function:
- Runs **only at build time**
- Fetches data
- Returns props for the page
- HTML is generated once and reused

---

### SSG Code Example (Next.js)

```js
import Image from 'next/image';

const Tutorials = ({ video }) => {
  return (
    <li className="mb-6">
      <a
        href={`https://www.youtube.com/watch?v=${video.id}`}
        target="_blank"
        rel="noopener noreferrer"
      >
        <Image
          src={video.image}
          alt={video.title}
          width={420}
          height={200}
        />
        <h4>{video.title}</h4>
        <div>{video.views} • {video.published}</div>
      </a>
    </li>
  );
};

export default function Home({ videos }) {
  return (
    <>
      <h1>Tutorials</h1>
      <ul>
        {videos.map((video, index) => (
          <Tutorials video={video} key={index} />
        ))}
      </ul>
    </>
  );
}

// Runs at build time
export async function getStaticProps() {
  const res = await fetch('http://localhost:4000/tutorials');
  const videos = await res.json();

  return {
    props: { videos }
  };
}
```


