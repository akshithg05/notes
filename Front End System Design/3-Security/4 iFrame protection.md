![[Pasted image 20251209064332.png]]

# iFrame Protection

iFrames are sections inside a webpage where we can embed content from another website.  
They are commonly used for things like:

- Advertisements  
- YouTube videos  
- External widgets or tools  

Although useful, iFrames introduce potential security risks.

---

## Why iFrames Can Be Dangerous

If we embed external content inside an iFrame, we must be careful because:

- The iFrame content may try to **interact with or control the main website**  
- It might attempt to **steal credentials** or sensitive information  
- It could trigger **unauthorized actions** that the user or website never intended  

Therefore, improper iFrame usage can expose the application to serious vulnerabilities if the embedded content is malicious or compromised.

# iFrame Vulnerabilities

When using iFrames, the embedded content can introduce several security risks. Below are the main vulnerabilities discussed:

---

## 1. Click Hijacking

This happens when an attacker places a transparent iFrame **on top of your actual UI elements**.  
So when the user thinks they are clicking a button on your site, they are actually clicking a hidden button inside the attacker’s iFrame.

This can lead to **unintended actions** being performed without the user knowing.

(Your understanding is correct.)

---

## 2. Data Theft via JavaScript

If not protected, an iFrame can attempt to:

- access data from the parent page  
- manipulate or read the parent DOM  
- perform actions using scripts  

Similarly, the parent can also potentially access sensitive content from the iFrame.  
This creates a risk of **data leakage** if either side is not trusted.

---

## 3. Session and Data Theft (Parent ↔ iFrame)

If proper restrictions are not applied:

- The iFrame may try to read session-related data from the parent  
- The parent may unintentionally expose sensitive information to the iFrame  
- Cross-origin communication may leak data between parent and child frames  

This can result in **session data, user info, or other sensitive details leaking** between the main site and the embedded iFrame.

# Clickjacking Example — Coding Demonstration

Below is a simple example showing how **clickjacking** works.  
The idea is that an attacker places a transparent iFrame on top of the real page UI, making the user click something they did not intend.

---

## Example Code 1 - Click Hijacking

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Clickjacking Example</title>
  </head>
  <body>
    <h1>Clickjacking Example</h1>
    <p>Click the button below to see a simple clickjacking demonstration.</p>

    <!-- Attacker overlays a transparent iframe from another website -->
    <iframe src="http://localhost:5011/iframe-website1" id="legit-iframe"></iframe>

    <!-- The user believes they are clicking this button -->
    <button id="overlay-button">Click Me!</button>

    <style>
      #legit-iframe {
        background-color: #ccc;
        opacity: 0;                  /* Makes iframe invisible */
        position: absolute;
        top: 0px;
        left: 0;
        width: 100%;
        height: 100%;
        z-index: 1;                  /* Places iframe on top of everything */
      }
    </style>

    <script>
      // Normal button action
      document.getElementById("overlay-button").addEventListener("click", () => {
        alert("Button clicked!");
      });
    </script>
  </body>
</html>
```

---

## What This Demonstrates

- The `<iframe>` is positioned above the real UI using `z-index: 1`.
- `opacity: 0` makes the iFrame completely **transparent**.
- The user sees the button labeled **"Click Me!"**, but their click actually interacts with the invisible iFrame.
- This is exactly how clickjacking tricks the user into performing unintended actions.

---

## Why This Is a Vulnerability

- Users think they are clicking your website’s button.
- In reality, they are clicking a hidden element inside the attacker’s iFrame.
- This can cause unauthorized actions like:
  - Liking a post  
  - Transferring money  
  - Changing account settings  
  - Following a malicious profile  

This example clearly demonstrates how easy it is to overlay a transparent iFrame and hijack user clicks.


# iFrame Vulnerability — Data Theft Example

Below is an example demonstrating how a malicious iFrame might attempt to **steal data** from the parent window.

---

## Example Code

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Malicious iframe</title>
  </head>
  <body>
    <h1>Malicious iframe</h1>
    <p>This iframe attempts to steal data from the parent window.</p>

    <script>
      window.alert("Hi");

      // Malicious JavaScript code in the iframe
      window.onload = function () {
        try {
          const parentWindow = window.parent;
          const parentDocument = parentWindow.document;

          // Attempt to read HTML from parent
          const stolenData = parentDocument.innerHtml;
          alert("Stolen Data: " + stolenData);
        } catch (error) {
          console.error("Data theft failed:", error);
        }
      };
    </script>
  </body>
</html>
```

---

## What This Example Tries To Do

- The iFrame loads as a “malicious child page.”
- On `window.onload`, it tries:

  ```js
  const parentWindow = window.parent;
  const parentDocument = parentWindow.document;
  ```

- Then it attempts to read:

  ```js
  parentDocument.innerHtml
  ```

- This would allow the iFrame to steal:
  - Parent DOM content  
  - Sensitive information  
  - Even cookies in older browsers  

---

## Why This Fails on Modern Websites

Modern browsers enforce **same-origin policy**, meaning:

- If the parent and child iFrames are from **different origins**, JavaScript cannot:
  - Access `window.parent.document`
  - Read DOM content
  - Read cookies  
  - Manipulate parent or child windows

Therefore:

> **Cross-origin access of the document is not allowed.**

The `try/catch` in the example logs an error, proving the browser blocks the attempt.

---

## When This Worked in Older Browsers

Older browser versions (and poorly configured websites) allowed:

- Cross-origin document access  
- Cross-origin cookie access  
- Parent ↔ child DOM reading  

This made it possible for:

- Data theft  
- Session hijacking  
- Credential exposure  

Modern browsers have mostly eliminated this vulnerability — but older systems or outdated sites may still be affected.

# iFrame Mitigation Strategies

To protect a website from iframe-related attacks such as clickjacking or data theft, we can use specific security headers. These headers tell the browser **whether or not the site is allowed to be embedded inside an iframe**.

---

## 1. `X-Frame-Options` Header

If you are the website owner and you want to completely prevent your site from being embedded in any iframe, you can use:

### **Options:**

- **DENY**  
  Disallow embedding the site in an iframe **entirely**.

- **SAMEORIGIN**  
  Allows the site to be embedded **only by pages from the same origin**.

### Example:

```
X-Frame-Options: DENY
```

Or:

```
X-Frame-Options: SAMEORIGIN
```

These headers protect your website from being placed inside a malicious iframe.

---

## 2. CSP Header — `frame-ancestors`

CSP provides a newer and more flexible way to restrict iframe usage.

### Example Using Express:

```js
app.use((req, res, next) => {
  res.setHeader('Content-Security-Policy', "frame-ancestors 'none'");
  next();
});
```

### What This Does:

- `"frame-ancestors 'none'"`  
  Ensures **no other website** can embed your site as an iframe under any circumstance.

This is the modern replacement for `X-Frame-Options` and provides more control.

---
# Allowing iFrames Safely — Using the `sandbox` Attribute

Sometimes we **want** to allow an iframe on our site, but we **do not** want the embedded iframe to:

- run JavaScript  
- open modals  
- perform actions  
- interact with the parent page  

For this, we can use the HTML **`sandbox`** attribute on the `<iframe>` tag.

When an iframe is sandboxed **without extra permissions**, it becomes extremely restricted:

- No JavaScript execution  
- No forms  
- No popups or modals  
- No top-level navigation  
- No access to parent window  

This allows you to **display** content (ads, static pages, etc.) **without executing any scripts** inside the iframe.

---

## Example — iFrame With No Script Execution

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Sandboxed iFrame Demo</title>
  </head>
  <body>
    <h1>Safe iFrame Example</h1>

    <!-- Sandboxed iframe: scripts inside this iframe will NOT run -->
    <iframe
      src="https://example.com"
      sandbox
      width="600"
      height="400"
    ></iframe>

  </body>
</html>
```

### Explanation:

- The `sandbox` attribute is present **without any permissions**.
- This means:
  - **No JavaScript is allowed**
  - **No popups/modals**
  - **No form submission**
  - **No navigation**
  - **No access to parent window**

Only **static HTML** will display.

---

## Example — iFrame With Some Permissions (still safe)

If you want the iframe to show content but still restrict scripts:

```html
<iframe
  src="https://example.com"
  sandbox="allow-same-origin"
  width="600"
  height="400"
></iframe>
```

### Behavior:
- Iframe can **load content normally**  
- Still **cannot run JavaScript** (because `allow-scripts` is *not* included)  
- Still **cannot open modals**  
- Still **cannot access parent window**  

# Setting Extra Security Headers in Cookies

When setting cookies, we can add certain flags that improve security and reduce common attacks such as XSS and CSRF.

---

## `httpOnly: true`
- When a cookie has the **HttpOnly** flag, it is **not accessible via JavaScript**.
- This means scripts cannot read it using `document.cookie`.
- Helps prevent cookie theft through XSS attacks.

Example:
```js
res.cookie("sessionId", token, {
  httpOnly: true
});
```

---

## `secure: true`
- The cookie will only be sent over **HTTPS** connections.
- Prevents the cookie from being transmitted in plain text over HTTP.
- Ensures confidentiality of sensitive cookies (like session cookies).

Example:
```js
res.cookie("sessionId", token, {
  secure: true
});
```

---

## `sameSite: 'strict'`
- Controls whether cookies are sent along with **cross-site requests**.
- With `"strict"` mode:
  - Cookies are **not sent** when the request originates from another domain.
  - Helps protect against CSRF attacks.
  - The browser only sends cookies when navigating **within the same site**.

Example:
```js
res.cookie("sessionId", token, {
  sameSite: "strict"
});
```

---

## Summary

| Cookie Flag | Purpose |
|-------------|---------|
| **httpOnly** | Prevents JavaScript from accessing cookies |
| **secure** | Sends cookie only over HTTPS |
| **sameSite: 'strict'** | Prevents cookies from being sent to other domains |

These flags together help strengthen cookie-based authentication security.