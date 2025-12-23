
**Cross-Site Request Forgery (CSRF)** occurs when a **malicious website causes a user’s browser to send an unauthorized request** to a trusted website **without the user’s intent**.

The attack works because the request is sent **using the user’s existing authentication context** (cookies / session).

---

## What Is Happening in CSRF

- The user is already **logged in** to a trusted website (e.g., bank website).
- The attacker tricks the user into clicking a malicious link or loading a malicious page.
- The browser automatically attaches authentication cookies.
- The trusted website receives a **valid authenticated request**.
- The action executes **without the user’s consent**.

---

## Example Scenario

If a user is logged into a bank website:

```
https://bank.com?accId=322&amount=10000
```

And the attacker embeds this URL in:
- an email
- a malicious website
- an image or hyperlink

Then:
- Clicking the link triggers the request
- The browser sends cookies automatically
- The bank processes the transfer

The server cannot tell whether the request was intentional.

---

## Why CSRF Happens

### 1. Stateless Nature of HTTP / HTTPS
HTTP is stateless:
- Each request is independent
- The server does not know **where** the request originated
- It only sees a valid request with valid credentials

---

### 2. Authentication Based Only on Tokens
- The server checks **only authentication tokens**
- It does not verify **who initiated** the request
- If the user is logged in, the request is trusted

The server assumes:
> “If the request has valid auth, it must be legitimate.”

---

## Key Characteristics of CSRF

- Happens **without user awareness**
- Exploits **browser behavior**, not server bugs
- Uses **existing login session**
- Does **not require stealing credentials**

---

## Core Idea

> CSRF abuses trust in authenticated browser requests by making users unknowingly perform actions they did not intend.

---

## CSRF — Vulnerabilities & Mitigations

---

## Common CSRF Vulnerabilities

### 1. Using GET Requests for State-Changing Actions
Using **GET** requests to perform updates or sensitive actions is dangerous.

Example:
```
http://bank.com/fundtransfer?accId=21312&amount=10000
```

Such URLs can be triggered via:
- `<a href="">` links
- `<img src="">` tags
- Embedded links in emails or malicious websites

Because browsers automatically send cookies, the action executes **without user intent**.

---

### 2. Hidden Form Submissions
Attackers can create hidden forms that auto-submit data:

```html
<form action="http://bank.com/fundtransfer" method="POST">
  <input type="hidden" name="accId" value="1231231" />
  <input type="hidden" name="amount" value="100000" />
  <input type="submit" value="Click for iPhone" />
</form>
```

If the user is logged in, the server processes the request as valid.

---

## Mitigation Strategies

### 1. Anti-CSRF Tokens
- Generate a unique token on the server
- Embed it in forms or requests
- Validate the token on submission

Example:
```html
<input type="hidden" name="csrf_token" value="${req.session.csrfToken}" />
```

Only requests with a valid token are accepted.

---

### 2. SameSite Cookies
Use SameSite cookies to restrict cross-site requests.

Example:
```js
app.use((req, res, next) => {
  res.setHeader("Set-Cookie", "SameSite=Strict; Secure");
  next();
});
```

This prevents cookies from being sent in cross-origin requests.

---

### 3. Validate Referrer / Origin
Check the `Referer` or `Origin` header to ensure the request comes from a trusted source.

This helps detect cross-site requests initiated by malicious pages.

---

### 4. Use CAPTCHA
CAPTCHA adds user interaction, making automated CSRF attacks harder.

---

### 5. Use CSP Headers
Content Security Policy (CSP) helps limit where requests and scripts can originate from, reducing attack surface.

---

### 6. Session Hygiene
- Log users out after inactivity
- Encourage strong passwords
- Reduce session lifetime

This limits the window in which CSRF attacks can succeed.

---

### 7. Never Use GET for Updates
- **GET** → only for fetching data
- **POST / PUT / DELETE** → for state-changing operations

Using GET for updates makes CSRF attacks trivial.

---

## Key Takeaway

> CSRF exploits the browser’s automatic credential handling.  
> Proper tokens, cookie policies, and request validation are essential to prevent it.


