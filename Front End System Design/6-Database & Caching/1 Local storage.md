## Local Storage – Analysis & Notes

### 1. What is Local Storage?
Local Storage is a **browser-provided persistent storage mechanism** that allows web applications to store data on the **user’s device** in the form of key–value pairs.

---

### 2. How It Works
Local Storage exposes a simple synchronous API:
- `setItem(key, value)`
- `getItem(key)`
- `removeItem(key)`
- `clear()`

These operations directly read/write data from the browser’s storage.

---

### 3. Size Limit
- **~5 MB per domain**
- Shared across all tabs and windows of the same domain
- Not per tab — per **origin (protocol + domain + port)**

---

### 4. Performance Characteristics
- All operations are **synchronous**
- Heavy reads/writes or large JSON parsing can **block the main thread**
- Avoid frequent or complex operations in performance-critical paths

---

### 5. Data Persistence
- Data **persists across page reloads, tab close, and browser restarts**
- Data is removed only when:
  - Manually cleared via code
  - User clears browser data
  - Site storage is cleared

---

### 6. Data Structure
- Stores data as **key–value pairs**
- **Values are always strings**
- Objects/arrays must be serialized using `JSON.stringify`
- Data must be deserialized using `JSON.parse` when read

---

### 7. Security Considerations
- Accessible by **any JavaScript running on the page**
- No built-in encryption
- Vulnerable to **XSS attacks**
- Not protected by HttpOnly or Secure flags
- Same-origin restricted (CORS applies)

❌ Do NOT store:
- Auth tokens
- Passwords
- Sensitive user data
- PII or credentials

---

### 8. When to Use Local Storage
✅ Suitable use cases:
- User preferences (theme: dark/light mode)
- UI state (toggles, layout preferences)
- Simple todo lists
- Shopping cart data (non-sensitive)
- Feature flags or onboarding status

---

### 9. When NOT to Use Local Storage
❌ Avoid for:
- Large datasets
- Sensitive information (tokens, passwords)
- Cross-device or cross-profile data
- Frequently changing data

---

## Simple React Example – Theme Toggle Using Local Storage

```js
import { useState } from "react";
import "./App.css";

export default function App() {
  const [theme, setTheme] = useState(localStorage.getItem("mode") || "light");

  return (
    <div className={`app-container ${theme}`}>
      <h1 className="heading">This is the heading</h1>
      <button
        className="button"
        onClick={() => {
          const newTheme = theme === "light" ? "dark" : "light";
          setTheme(newTheme);
          localStorage.setItem("mode", newTheme);
        }}
      >
        Toggle theme
      </button>
    </div>
  );
}
```

### Interview One-Liner

Local Storage is a synchronous, persistent, key-value browser storage (≈5 MB per origin) best suited for non-sensitive, long-lived UI preferences.