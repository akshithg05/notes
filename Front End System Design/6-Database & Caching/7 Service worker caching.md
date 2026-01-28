
## What is a Service Worker?
A Service Worker is a JavaScript file that runs in the background and sits between:
- The web page (browser)
- The network layer

It acts as a programmable proxy that intercepts network requests and allows us to decide:
- Fetch from cache
- Fetch from network
- Fetch from network and then cache the response

---

## Why Service Worker Caching?
- Full control over caching logic
- Works even when the user is offline
- Faster asset loading
- Reduces network dependency
- Enables advanced strategies (offline-first, cache-first, network-first)

Unlike HTTP caching, this is **explicit, programmable caching**.

---

## What Can a Service Worker Control?
- Static assets (JS, CSS, images, fonts)
- API/network requests
- Cache invalidation logic
- Offline fallback behavior

Example decision:
- If image exists in cache → serve from cache
- Else → fetch from network, store in cache, then return

---

## Service Worker Lifecycle

1. Registering  
2. Installing  
3. Installed  
4. Activating  
5. Activated  

Once activated, it starts intercepting fetch requests.

---

## High-Level Flow
1. Browser loads the page
2. Service worker intercepts request
3. Checks cache
4. If found → return cached response
5. Else → fetch from network, cache it, return response

---

## HTML File (Registering the Service Worker)

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Service Worker Example</title>
    <link rel="stylesheet" href="/styles.css" />
  </head>
  <body>
    <h1>Hello, Service Worker!</h1>
    <img src="/image.gif" alt="Cached Image" />
    <script src="/app.js"></script>

    <script>
      if ("serviceWorker" in navigator) {
        navigator.serviceWorker
          .register("/sw.js")
          .then((registration) => {
            console.log(
              "Service Worker registered with scope:",
              registration.scope
            );
          })
          .catch((error) => {
            console.error("Service Worker registration failed:", error);
          });
      }
    </script>
  </body>
</html>
```

---

## Service Worker File (sw.js)

```js
const CACHE_NAME = "my-cache-v1";

const urlsToCache = [
  "/",
  "/index.html",
  "/styles.css",
  "/app.js",
  "/image.gif"
];

self.addEventListener("install", (event) => {
  event.waitUntil(
    caches.open(CACHE_NAME).then((cache) => {
      return cache.addAll(urlsToCache);
    })
  );
});

self.addEventListener("fetch", (event) => {
  event.respondWith(
    caches.match(event.request).then((response) => {
      return response || fetch(event.request);
    })
  );
});
```

---

## Caching Strategy Used Here
**Cache First**
- Try cache
- If not found → go to network
- Simple and fast for static assets

---

## Service Worker vs HTTP Caching

HTTP Caching:
- Controlled by headers
- Browser decides
- Limited flexibility

Service Worker Caching:
- Fully controlled by developer
- Custom logic
- Works offline
- More powerful

---

## Common Use Cases
- Offline-first apps
- Progressive Web Apps (PWA)
- Image and asset caching
- Reducing API latency
- Improving perceived performance

---

## One-Line Interview Summary
A service worker acts as a programmable proxy between the browser and network, enabling fine-grained control over caching, offline support, and request handling.

