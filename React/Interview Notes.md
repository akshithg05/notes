
For form validation in big projects use library like - formik , easier to handle forms and form validations.

### 🧠 **Why use `e.preventDefault()` when submitting a form?**

By default, when an HTML form is submitted:
- The **browser reloads the page** (i.e., full page refresh).
- The form data is sent to the `action` URL (if provided).    
- You **lose JavaScript state**, and SPA frameworks like React/Vue/Next.js don't handle that well.

---

### ✅ `e.preventDefault()` **stops that default behavior** so you can:
1. **Handle the form submission with JavaScript**
2. Validate inputs
3. Send the data via `fetch()` or `axios` (AJAX-style)
4. Stay on the same page (single-page app behavior)

---

### 📦 Example in React:

`function handleSubmit(e) {   e.preventDefault(); // Stop the page from refreshing   // Your logic: validate, send data, show feedback, etc. }`

### 🧪 Without `e.preventDefault()`:

The browser will reload the page and possibly submit the form data via HTTP — which is **not** what you usually want in React or client-driven apps.

## UseRef()
### 🧠 What is `useRef`?

`useRef` is a React Hook that lets you reference a value that’s not needed for rendering.
`useRef` is a tool in React that lets you:

1. **Keep a secret box** to store something that **doesn’t change the screen when it updates**.
2. **Point to an actual HTML element** (like an input box) and do things like focus on it.

### 📦 Think of it like:

- `useState` is like a **notebook**: you write a value, and React says “Okay! I’ll update the screen.”
- `useRef` is like a **sticky note**: you jot down something you want to remember **but don’t need to tell React** to update the screen when it changes.

| Feature/Use Case                                 | `useState`  | `useRef`                    |
| ------------------------------------------------ | ----------- | --------------------------- |
| Triggers re-render on update                     | ✅ Yes       | ❌ No                        |
| Stores values between renders                    | ✅ Yes       | ✅ Yes                       |
| Accesses DOM elements directly                   | ❌ No        | ✅ Yes                       |
| Good for frequent updates (e.g., timers, scroll) | ❌ No (slow) | ✅ Yes (fast, no re-renders) |
When you use `useRef` to reference a DOM element in React, it **stores an object** with a single property called `.current`, which **points to the actual DOM element** once it's rendered.

When using useRef with an input in React, you generally do not need an onChange handler to manage the input's value if you are creating an "uncontrolled component."

### Here's why:
Uncontrolled Components:
With useRef, you are directly interacting with the DOM element. The input's value is managed by the DOM itself. You would typically access the input's value when a specific event occurs, such as a form submission, by using inputRef.current.value. In this scenario, onChange is not required for updating the component's state or triggering re-renders, as useRef does not trigger re-renders when its current property changes.

Controlled Components:
If you need the input's value to be part of your component's state and to trigger re-renders when it changes, you would use useState and an onChange handler to update that state. This is the more common and recommended approach for managing input values in React, as it provides a clear and predictable way to handle data flow and component updates.

In summary:
No onChange needed:
If you are using useRef to directly access the DOM element and retrieve its value at a specific point (e.g., form submission), you don't need onChange.

onChange is needed:
If you are managing the input's value as part of your component's state and want to re-render the component when the input changes, you should use useState and an onChange handler.

In React, ==controlled components rely on the component's state to manage form data, while uncontrolled components manage data directly through the DOM==. Controlled components offer greater control and predictability, especially in complex forms, while uncontrolled components can be simpler and potentially more performant for basic forms. 

Here's a more detailed breakdown:

Controlled Components:

- **State Management:** React component manages the state of the form elements, such as input fields, text areas, or select dropdowns. 

- **Data Flow:** React state is the "single source of truth" for the form data. 

- **Event Handling:** `onChange` event handlers are used to update the component's state whenever the input value changes. 

- **Validation:** Enables easier and more immediate form validation since the data is readily available in the state. 

- **Example:**

Code

```
    function ControlledInput() {      const [value, setValue] = useState("");          const handleChange = (event) => {        setValue(event.target.value);      };          return (        <input type="text" value={value} onChange={handleChange} />      );    }
```

Uncontrolled Components:

- **DOM Interaction:** The component interacts directly with the DOM to access and update the form data, typically using refs. 

- **State Management:** The component's state is not directly used to manage the input values. 

- **Data Retrieval:** Values are typically accessed using `useRef` to get the current value from the DOM element. 

- **Simpler Implementation:** Can be simpler to implement for basic forms where you don't need to react to every input change. 

- **Example:**

Code

```
    function UncontrolledInput() {      const inputRef = useRef(null);          const handleSubmit = () => {        alert("A value was submitted: " + inputRef.current.value);      };          return (        <>          <input type="text" ref={inputRef} />          <button onClick={handleSubmit}>Submit</button>        </>      );    }
```

Choosing between Controlled and Uncontrolled Components: 

- **Controlled components:**
    
    Recommended for forms where you need to control the data flow, perform real-time validation, or integrate with other components that rely on the form data. 
    

- **Uncontrolled components:**
    
    Suitable for simpler forms where you don't need to validate input, or when interacting with legacy code or third-party libraries.

What is specificity, in as much depth as you can give? Would you ever unit test CSS? What are some concerns to keep in mind with web accessibility in HTML and CSS? What is your general workflow when adapting a Figma design for use in a website? When would you use :has() or :not() in your selectors? Why choose SCSS over CSS? What are some common considerations when adapting for different screen sizes? What does it mean for a browser to repaint and reflow? What is a DOM hit? Why might a developer choose to implement aspects of a UI in Javascript over HTML or CSS files, such as animations?
