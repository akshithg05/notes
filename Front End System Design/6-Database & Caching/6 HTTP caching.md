
![[namastedev.com_learn_namaste-frontend-system-design_http-caching.png]]

## What is HTTP Caching?
HTTP caching is a mechanism to store web resources (JS, CSS, images, fonts, HTML, etc.) in the browser so that repeated requests do not always hit the server.

Instead of fetching the same resource again and again from the server, the browser can reuse cached data, improving performance and reducing server load.

---

## Why HTTP Caching is Important
- Improves UX (faster page loads, tab switches, navigation)
- Reduces server load
- Saves network bandwidth
- Improves overall app performance
- Essential for scalable frontend systems

---

## High-Level Flow
1. Client (Browser) requests a resource from the server
2. Browser checks cache
3. If valid cache exists → use cached response
4. Otherwise → request from server and store response in cache

---

## What Can Be Cached?
- JavaScript files
- CSS files
- Images
- Fonts
- HTML pages
- Any static or cacheable resource

---

## HTTP Headers Used for Caching

### 1. Cache-Control (Highest Priority – P0)
Controls how and for how long a resource can be cached.

Example:
Cache-Control: public, max-age=86400

- public → can be cached by browser and proxies
- max-age → relative time (in seconds)
- Browser directly serves from cache if fresh

---

### 2. Expires (P1)
Defines an absolute expiry date for the resource.

Example:
Expires: Sat, 27 Jan 2023 11:20:39 GMT

- Uses server date-time
- Less flexible than Cache-Control
- Ignored if Cache-Control is present

---

### 3. Last-Modified (P2)
Tells when the resource was last changed.

Flow:
- Browser sends request with If-Modified-Since
- Server compares timestamps
- If unchanged → returns 304 Not Modified
- If changed → returns new data

---

### 4. ETag (P3)
A hash generated from the resource content.

Flow:
- Browser sends If-None-Match with ETag
- Server compares hash
- Same hash → 304 Not Modified
- Different hash → return new content

---

## Cache Validation vs Cache Usage
- Cache-Control → browser uses cache directly (no network call)
- Last-Modified & ETag → browser still makes a request, but server may respond with 304

---

## Priority Order of Headers
1. Cache-Control (P0)
2. Expires (P1)
3. Last-Modified (P2)
4. ETag (P2)

---

## Common Challenge: Always Fetch Fresh Data
If you want to bypass cache (for example, always load a new image):

Technique:
- Add a query parameter to the URL

Example:
image.gif?v=12345

This tricks the browser into treating it as a new resource.

---

## Demo: HTML Code

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>HTTP Caching Demo</title>
    <style>
      body {
        font-family: Arial, sans-serif;
        margin: 20px;
      }
      #content {
        max-width: 800px;
        margin: 0 auto;
      }
      img {
        max-width: 100%;
        height: auto;
      }
    </style>
  </head>
  <body>
    <div id="content">
      <h1>HTTP Caching Demo</h1>
      <p>This demo showcases HTTP caching using Cache-Control.</p>

      <h2>Cached Image</h2>
      <img src="image.gif" id="cachedImage" />

      <h2>Fetch New Image</h2>
      <button onclick="fetchNewImage()">Fetch New Image</button>
    </div>

    <script>
      function fetchNewImage() {
        const randomQuery = Math.random().toString(36).substring(7);
        document.getElementById("cachedImage").src =
          `image.gif?${randomQuery}`;
      }
    </script>
  </body>
</html>
```

---

## Server Logic (Node + Express)

```js
const express = require("express");
const path = require("path");

const app = express();

app.use((req, res, next) => {
  res.setHeader("Cache-Control", "public, max-age=86400");
  res.setHeader("Expires", "Sat, 27 Jan 2023 11:20:39 GMT");
  next();
});

app.use(
  express.static(path.join(__dirname, "public"), {
    // cacheControl: false,
    // etag: false,
    // lastModified: false,
  }),
);

app.listen(3000, () => {
  console.log("Server running on port 3000");
});

```
---

## One-Line Interview Summary
HTTP caching stores web resources in the browser using cache headers to improve performance, reduce server load, and optimize network usage.
