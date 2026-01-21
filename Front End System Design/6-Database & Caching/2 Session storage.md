## Session Storage – Analysis & Notes

### 1. What is Session Storage?
Session Storage is a **browser-provided storage mechanism** used to store data **persistently for a single browser tab session**.  
Data lives as long as the tab is open.

---

### 2. How It Works
Session Storage exposes the same API as Local Storage:
- `setItem(key, value)`
- `getItem(key)`
- `removeItem(key)`
- `clear()`

All operations are **synchronous**.

---

### 3. Size Limit
- **~5 MB per origin** (protocol + domain + port)
- Storage is **isolated per tab**

---

### 4. Performance
- Operations are **synchronous**
- Heavy reads/writes or large JSON parsing can **block the main thread**
- Avoid complex or frequent operations

---

### 5. Persistence Behavior (Very Important)
- Data **persists on page reload**
- Data is **cleared when the tab or browser window is closed**
- Data is **NOT shared across tabs**

Special cases:
- **Duplicating a tab** → a *copy of the current session storage* is created initially
- **Opening the same URL in a new tab** → storage is NOT copied

---

### 6. Data Structure
- Key–value based
- Values are always **strings**
- Objects/arrays must be stored using `JSON.stringify`
- Retrieved using `JSON.parse`

---

### 7. Security Considerations
- Accessible by JavaScript → **vulnerable to XSS**
- No encryption by default
- No HttpOnly or Secure flags
- does **not** have a built-in, time-based expiry like cookies. but can be set.

❌ Still avoid storing:
- Auth tokens
- Passwords
- Highly sensitive data

---

### 8. When to Use Session Storage
✅ Good use cases:
- Temporary sensitive data (OTP state, form drafts)
- Multi-step forms
- Temporary user flows (checkout steps)
- Wizard or onboarding state
- Data that should reset when tab closes

---

### 9. When NOT to Use Session Storage
❌ Avoid for:
- Large datasets
- Long-term persistence
- Async-heavy operations
- Cross-tab or cross-session data sharing

---

## React Example – Todo App Using Session Storage

```js
import { useState } from 'react';
import './App.css';

export default function App() {
  const [todos, setTodos] = useState(
    JSON.parse(sessionStorage.getItem('notes')) || []
  );
  const [inputValue, setInputValue] = useState('');

  const handleAddTodo = () => {
    if (inputValue.trim()) {
      const newNotes = [...todos, { id: Date.now(), text: inputValue }];
      setTodos(newNotes);
      sessionStorage.setItem('notes', JSON.stringify(newNotes));
      setInputValue('');
    }
  };

  const handleDeleteTodo = (id) => {
    const updatedNotes = todos.filter((todo) => todo.id !== id);
    setTodos(updatedNotes);
    sessionStorage.setItem('notes', JSON.stringify(updatedNotes));
  };

  const handleKeyPress = (e) => {
    if (e.key === 'Enter') {
      handleAddTodo();
    }
  };

  return (
    <div className="app-container">
      <div className="todo-wrapper">
        <h1 className="todo-title">📝 My Todo List</h1>

        <div className="input-container">
          <input
            type="text"
            className="todo-input"
            placeholder="Add a new todo..."
            value={inputValue}
            onChange={(e) => setInputValue(e.target.value)}
            onKeyPress={handleKeyPress}
          />
          <button className="add-button" onClick={handleAddTodo}>
            Add
          </button>
        </div>

        <ul className="todo-list">
          {todos.length === 0 ? (
            <div className="empty-state">No todos yet. Add one above!</div>
          ) : (
            todos.map((todo) => (
              <li key={todo.id} className="todo-item">
                <span className="todo-text">{todo.text}</span>
                <button
                  className="delete-button"
                  onClick={() => handleDeleteTodo(todo.id)}
                >
                  Delete
                </button>
              </li>
            ))
          )}
        </ul>
      </div>
    </div>
  );
}
```

### Interview One-Liner

Session Storage is a synchronous, tab-scoped browser storage (~5 MB per origin) that persists across reloads but is cleared when the tab closes, making it ideal for temporary session data.
