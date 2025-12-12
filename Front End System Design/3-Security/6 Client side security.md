
![[Pasted image 20251212071326.png]]
---
## 1. Storing Sensitive Information on the Client storage

### a. **Prefer storing on the server (safest option)**
If possible, do **not** store sensitive information (passwords, tokens, credentials) on the client at all.  
Server-side storage is always the safest because:

- The data never reaches the browser  
- It cannot be exposed through XSS  
- Attackers cannot read memory or localStorage  

Whenever possible, keep sensitive data on the server.

---
### b. **If you MUST store it on the client, encrypt it**

Example flow:

```js
const sensitiveData = 'mySecretPassword';
const encryptedData = encryptFunction(sensitiveData);

localStorage.setItem('encryptedData', encryptedData);
```

Even though encryption in the browser is not perfect (because the key may also be accessible),  
it is still **better than storing raw values**.

---
### c. **Always set token expiry—even in localStorage**

If your app stores tokens temporarily in `localStorage`, ensure they are removed after a short duration.

Example:

```js
const token = generateToken();
localStorage.setItem('token', token);

setTimeout(() => {
  // Token expired; remove it
  localStorage.removeItem('token');
}, tokenExpirationTime);
```

This reduces risk in case:

- The user leaves their device unlocked  
- Someone steals/misuses the token  
- XSS vulnerability attempts to read stored data  

Even though localStorage does not have a built-in expiry system, you can manually enforce it.

---

## Summary of Point 1

1. **Best:** avoid storing sensitive info on client  
2. **If needed:** store only encrypted values  
3. **Always:** enforce token expiry even in localStorage  



## 2. Authentication

### a. Use JWT
Prefer using **JWT** instead of direct authentication.  
It avoids sending credentials repeatedly and works well with stateless APIs.

### b. Token Expiry
Always ensure tokens have an **expiry time**.  
Short-lived tokens reduce risk if they are stolen.

### c. MFA
Enable **multi-factor authentication** (OTP or authenticator apps) for an extra layer of login security.

## 3. Data Integrity

### a. Use Checksums
A **checksum** is a small computed value (like a hash) that represents the original data.  
If someone tampers with the data, the checksum will no longer match.

This helps detect whether the data in client-side storage has been modified.

### Example

```js
// Storing data with checksum
const dataToStore = 'myData';
const checksum = calculateChecksum(dataToStore);

localStorage.setItem('data', dataToStore);
localStorage.setItem('checksum', checksum);

// Validating data integrity
const storedData = localStorage.getItem('data');
const storedChecksum = localStorage.getItem('checksum');

if (calculateChecksum(storedData) === storedChecksum) {
  // Data is intact
} else {
  // Data was tampered
}
```

If the data changes even slightly, the checksum changes — making tampering easier to detect.

## 4. Storage Limit

### Local Storage Limit
LocalStorage typically allows **5–10 MB** of data per origin.  
Storing more than this can lead to:

- Data loss  
- Incomplete writes  
- Unexpected overwrites  

Always clear old data before adding new data.

---

### Typical Browser Storage Limits

| Storage Type       | Typical Limit |
|--------------------|---------------|
| **localStorage**   | ~5–10 MB      |
| **sessionStorage** | ~5 MB         |
| **cookies**        | ~4 KB per cookie (very small) |
| **IndexedDB**      | Hundreds of MB to several GB (varies by browser and free disk space) |
| **Cache Storage (Service Worker Cache)** | Up to hundreds of MB (depends on disk availability) |

These limits vary across browsers, but the above values reflect common practical limits.

---

### Checking Available Storage (Example)

```js
function hasEnoughSpaceForData() {
  if ('storage' in navigator && 'estimate' in navigator.storage) {
    navigator.storage.estimate().then(estimate => {
      console.log("Usage: " + (estimate.usage / 1024 / 1024).toFixed(2) + " MB");
      console.log("Quota: " + (estimate.quota / 1024 / 1024).toFixed(2) + " MB");
    });
  } else {
    console.log("StorageManager API is not supported in this browser.");
  }
}
```

## 5. Session Management

When storing any session-related token — especially **cookies** — we must apply the correct security flags.

### a. Use `httpOnly`
- Prevents JavaScript from reading the cookie (`document.cookie` cannot access it).
- Protects the token from XSS attacks.
- Ensures the cookie is only handled by the browser and the server.

### b. Use `secure`
- Cookie is only sent over **HTTPS**.
- Prevents session leakage on unsecured networks.
- Ensures encrypted transport of sensitive session data.

### c. Do Not Read Cookies on the Client
Cookies used for authentication (like session tokens) **must not** be read or manipulated from client-side JavaScript.  
They should be:

- Written by the server  
- Sent automatically by the browser based on domain + path rules  
- Protected with security flags  

---

### Example Cookie Setup

```js
res.cookie("sessionToken", token, {
  httpOnly: true,
  secure: true,
});
```

This ensures the session token is safe from client-side access and always transmitted securely.


## Note - 

### Why httpOnly Cookies Can Still Be Read on the Server

- `httpOnly: true` only blocks **browser JavaScript** from reading the cookie (`document.cookie` cannot access it).
- It does **not** block the browser from sending the cookie to the server.
- The server can always read cookies through `req.headers.cookie`.

### Why secure Cookies Work on localhost

- `secure: true` requires HTTPS.
- But browsers treat **localhost as a secure context**, so secure cookies are still sent even over `http://localhost`.

