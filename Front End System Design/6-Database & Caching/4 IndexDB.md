## IndexedDB – Client-Side Storage Notes

### 1. What is IndexedDB?
IndexedDB is a **client-side database** used for **persistent storage of large and complex data** in the browser.  
It is more powerful than Local Storage, Session Storage, and Cookies.

---

### 2. How It Works
IndexedDB is based on a **transactional database model**:
- Open a database using `indexedDB.open()`
- Create **object stores** (similar to tables)
- Perform operations using **transactions**
- Supports indexes for faster lookup and search

All operations are **asynchronous**.

---

### 3. Size Limit
- Supports **very large storage** (100 MB+)
- Exact limit depends on browser and user permissions
- Suitable for large datasets

---

### 4. Performance Characteristics
- **Asynchronous and non-blocking**
- Does not block the main thread
- Supports complex queries and indexing
- Efficient for large reads/writes and searches

---

### 5. Data Persistence
- Data **persists across browser sessions**
- Survives page reloads and browser restarts
- Data must be explicitly cleared

---

### 6. Data Structure
- Key–value based
- Values can be:
  - Objects
  - Arrays
  - Files
  - Blobs
- Much more flexible than Local/Session Storage

---

### 7. Security Considerations
- Accessible via JavaScript → vulnerable to **XSS**
- No built-in encryption
- Same-Origin Policy enforced
- Must clean up data on logout
- Avoid storing sensitive or credential data

---

### 8. When to Use IndexedDB
✅ Ideal use cases:
- Large datasets
- Offline-first applications
- Chat history (e.g., Slack, WhatsApp Web)
- Document editors (e.g., Google Docs)
- Client-side caching
- Data-heavy applications

---

### 9. When NOT to Use IndexedDB
❌ Avoid for:
- Small datasets
- Simple key-value storage
- Sensitive or secure data
- Synchronous or trivial operations

For small or simple data:
- Prefer Local Storage

---

### 10. IndexedDB APIs
IndexedDB exposes multiple low-level APIs, which can be verbose and complex to use directly.

---

### 11. Dexie (Wrapper Library)
Dexie is a **popular wrapper around IndexedDB** that:
- Simplifies IndexedDB usage
- Provides a cleaner, promise-based API
- Reduces boilerplate
- Improves developer experience

Dexie is recommended for most real-world IndexedDB use cases.

---

### Interview One-Liner
IndexedDB is an asynchronous, large-capacity, client-side database designed for storing complex and offline-capable data, suitable for data-heavy web applications.
