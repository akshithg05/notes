## 11. What are proxies in JavaScript used for?


A **Proxy** lets you **intercept and customize operations** on an object—like reading, writing, deleting properties, or calling functions.

Think of a Proxy as a **middle layer** between your code and an object.

They are used when you want to:

- **Control access** to object properties
- **Validate data** before setting it
- **Log or track changes**
- **Create reactive systems** (like modern frameworks)
- **Define custom behavior** for normal operations

Basic Syntax 
```
const proxy = new Proxy(targetObject, handler);
```
![[Pasted image 20260105204607.png]]

![[Pasted image 20260105204631.png]]

![[Pasted image 20260105204724.png]]

## **Common Interview Traps**

❌ _“Proxies modify the original object”_  
✅ They **wrap** the object and intercept operations.

❌ _“Proxies only work for properties”_  
✅ They can intercept:

- `get`, `set`, `deleteProperty`
    
- `has` (`in` operator)
    
- `apply` (functions)
    
- `construct` (`new`)


Interview answer

JavaScript Proxies allow developers to intercept and customize fundamental operations on objects, enabling validation, logging, access control, and reactive behavior.

## 26. Iterators and Generators 

An **iterator** is an object that defines **how to iterate** over a sequence of values **one at a time**.


An **iterator** is an object that defines how values are accessed one at a time. It must implement a `next()` method that returns an object of the form `{ value, done }`. When `done` is `false`, iteration continues; when `done` is `true`, iteration is complete. JavaScript features like `for...of` rely on iterators internally via `Symbol.iterator`.

A **generator** is a special function that automatically creates an iterator. It is declared using `function*` and uses the `yield` keyword to return a value while pausing execution. The generator resumes from the paused point on the next `next()` call.

```js
function* numbers() {
  yield 1;
  yield 2;
  yield 3;
}

const gen = numbers();
gen.next(); // { value: 1, done: false }
gen.next(); // { value: 2, done: false }
gen.next(); // { value: 3, done: false }
gen.next(); // { value: undefined, done: true }
```

A generator starts executing only when `next()` is invoked. Each `yield` pauses execution and produces a value. When the generator reaches the end of its function body, or when a `return` statement is executed, the generator finishes and `done` becomes `true`. A `return` immediately terminates the generator and provides a final value, though this value is ignored by `for...of`.

Generators are lazy by nature, producing values only when requested. They return iterators, not direct values, and are synchronous by default. Compared to manually implemented iterators, generators provide cleaner syntax and built-in state management.

**Interview one-liner:**  
A generator is a special function that simplifies iterator creation by allowing execution to pause and resume using `yield`, with iteration ending when the generator completes execution.


#### [[2026-01-15]]

## Property Flags & Property Descriptors (JavaScript)

In JavaScript, every object property has **metadata** associated with it, called **property flags**. These flags define how the property behaves when accessed, modified, or iterated over. Together, the property’s value and its flags are represented using a **property descriptor**.

### Property Flags
There are three main property flags for data properties:

- **writable** → determines if the property value can be changed
- **enumerable** → determines if the property appears in loops like `for...in` or `Object.keys`
- **configurable** → determines if the property can be deleted or reconfigured

By default, properties created normally have all flags set to `true`.

---

### Property Descriptor
A **property descriptor** is an object that describes a property’s value and its flags.


You can access it using:
```js
Object.getOwnPropertyDescriptor(obj, prop)
```

```js
const user = {
  name: "Akshith"
};

console.log(Object.getOwnPropertyDescriptor(user, "name"));
```


Output: 
```js
{
  value: "Akshith",
  writable: true,
  enumerable: true,
  configurable: true
}
```

#### Defining Property Flags Manually
```js
const user = {};

Object.defineProperty(user, "id", {
  value: 101,
  writable: false,
  enumerable: false,
  configurable: false
});

```

#### Interview answer 

Property flags define how an object property behaves, and property descriptors expose and control these flags using methods like `Object.getOwnPropertyDescriptor` and `Object.defineProperty`.

[[2026-01-21]]

## call, apply, bind (JavaScript)

call, apply, and bind are JavaScript methods used to explicitly control the value of `this` when invoking a function. They are useful when a function needs to run with a specific execution context.

call() invokes the function immediately and accepts arguments one by one.

Example:
    function greet(city) {
      console.log(this.name + " from " + city);
    }

    const user = { name: "Akshith" };
    greet.call(user, "Bangalore");

apply() also invokes the function immediately, but it accepts arguments as an array, which is helpful when arguments are already grouped.

Example:
    greet.apply(user, ["Bangalore"]);

bind() does not invoke the function immediately. Instead, it returns a new function with `this` permanently bound to the provided object, which can be executed later.

Example:
    const boundGreet = greet.bind(user, "Bangalore");
    boundGreet();

Key differences:
- call → immediate invocation, arguments passed individually
- apply → immediate invocation, arguments passed as an array
- bind → returns a new function, executed later

Interview one-liner:
call and apply invoke a function immediately with a specific `this` value, while bind returns a new function with `this` bound for future invocation.


### Arrow functions vs functions with "function" keyword caveat

**Arrow functions do not have their own `this`; they lexically bind `this` from their surrounding scope.**  
Functions declared with the `function` keyword have a **dynamic `this`**, which is determined by how the function is called.

So:

- ✅ Arrow functions **fix `this` at creation time**
    
- ❌ `function` keyword functions **do not fix `this` automatically**, but **can be fixed using `bind`, `call`, or `apply`**
    

---

## Why Arrow Functions “Fix” `this`

Arrow functions:

- Do **not** create their own `this`
    
- Inherit `this` from the enclosing scope
    

`const obj = {   name: "Akshith",   greet: () => {     console.log(this.name);   } };  obj.greet(); // undefined (or global this)`

📌 `this` comes from where the function is **defined**, not how it’s called.

---

## `function` Keyword Has Dynamic `this`

`const obj = {   name: "Akshith",   greet: function () {     console.log(this.name);   } };  obj.greet(); // Akshith`

Here, `this` depends on the **call-site**.

---

## Fixing `this` with `function`

Even though `function` does not fix `this` by default, you **can** fix it explicitly:

`const greet = function () {   console.log(this.name); };  const boundGreet = greet.bind({ name: "Akshith" }); boundGreet(); // Akshith`

---

## Interview-Safe Summary (Say This)

> Arrow functions lexically bind `this` from their surrounding scope, whereas functions declared with the `function` keyword have a dynamic `this` that depends on how they are called, though it can be fixed explicitly using `bind`.

---

## Common Interview Trap ❌

> “Arrow functions always have `this` bound to the object”

❌ False  
Arrow functions **do not bind to the object**, they bind to the **lexical scope**.

---

## Ultra-Short Version

> Arrow functions capture `this` lexically, while normal functions determine `this` at runtime based on the call-site.


## Interview-Ready Explanation - DOM

The **DOM (Document Object Model)** is a **programming interface for web documents**.  
It represents an HTML or XML document as a **hierarchical tree of nodes**, where each node corresponds to a part of the document such as elements, attributes, or text.

The browser creates the DOM after parsing the HTML. JavaScript can then **read, modify, add, or remove nodes** using DOM APIs, which allows web pages to become **dynamic and interactive**.

The DOM tree starts with the `document` object at the top, followed by elements like `<html>`, `<head>`, and `<body>`, and continues down to individual elements and text nodes.

Event listeners can be attached to DOM nodes to handle user interactions, and styles can be applied via CSS or modified dynamically through JavaScript.

### [[2026-02-11]]

# 113. Polyfills 

A **polyfill** in JavaScript is code that adds support for a newer feature in environments (usually older browsers) that don’t support it yet.

Think of it as:

> “If the environment doesn’t have this feature, I’ll provide my own implementation.”

---

# 🧠 Why Polyfills Exist

JavaScript evolves fast (ES6, ES2017, ES2020, etc.), but not all browsers update at the same speed.

For example:

- `Promise` didn’t exist in older browsers
    
- `Array.prototype.includes()` wasn’t always available
    
- `fetch()` wasn’t supported in older versions of Internet Explorer
    

Polyfills allow you to use modern features while still supporting older environments.

---

# 🔧 Example: Simple Polyfill

### Problem:

Older browsers don’t support:

`Array.prototype.includes()`

### Polyfill:

`if (!Array.prototype.includes) {   Array.prototype.includes = function(value) {     return this.indexOf(value) !== -1;   }; }`

### What’s happening:

1. Check if `includes` exists
    
2. If not → define it
    
3. Older browsers now behave like modern ones
    

---

# 🧩 Real Example: Promise Polyfill

Before `Promise` was native, libraries like:

- `core-js`
    
- `es6-promise`
    

provided Promise implementations for older browsers.



[[2026-03-11]]

# 5. Simple Throttle Implementation

function throttle(fn, delay) {  
  let lastTime = 0;  
  
  return function () {  
    const now = Date.now();  
  
    if (now - lastTime >= delay) {  
      fn();  
      lastTime = now;  
    }  
  };  
}

---

# 6. How It Works

### Step 1

When the function runs the first time:

lastTime = 0

Current time:

now = 1000

Check:

1000 - 0 >= delay

True → run function.

Update:

lastTime = now

---

### Step 2 (next call quickly)

now = 1200

Check:

1200 - 1000 >= 1000

False.

So the function **does not run**.

---

### Step 3 (after delay)

now = 2100

Check:

2100 - 1000 >= 1000

True → run again.

---

# 7. Using Throttle

Example:

function logScroll() {  
  console.log("scroll event");  
}  
  
const throttledScroll = throttle(logScroll, 1000);  
  
window.addEventListener("scroll", throttledScroll);

Now even if scroll fires **100 times**, the function runs **once per second**.


# Debouncing

# 1. When `debounce` is first executed

``` js
const debouncedHello = debounce(sayHello, 2000);
```


At this moment:

```js
function debounce(fn, delay) {  
  let timer;   // created here  
  
  return function () {  
    clearTimeout(timer);  
    timer = setTimeout(() => {  
      fn();  
    }, delay);  
  };  
}
```

A **single `timer` variable** is created.

The returned function **remembers this variable** through a closure.

So internally it looks like:

debouncedHello  
   ↓  
closure memory  
   timer

---

# 2. First call

debouncedHello();

Execution:

timer = setTimeout(...)

Suppose the browser gives timer id:

timer = 101

---

# 3. Second call (before 2 seconds)

debouncedHello();

Now the same function runs again.

But `timer` still exists in the closure.

So:

clearTimeout(timer)  
clearTimeout(101)

This **cancels the previous timer**.

Then a new timer is created:

timer = setTimeout(...)  
timer = 102

---

# 4. Third call

Again:

clearTimeout(102)  
timer = 103

So every time:

old timer → cancelled  
new timer → created

---

# 5. Timeline example

Calls happen quickly:

t=0ms     debouncedHello() → timer=101  
t=200ms   debouncedHello() → cancel 101 → timer=102  
t=400ms   debouncedHello() → cancel 102 → timer=103

No more calls.

After **2000ms from last call**:

timer 103 executes → sayHello()

---

# 6. Why the same timer variable works

Because of **closure**.

The returned function keeps access to the **same `timer` variable** created when `debounce` ran.

So all calls operate on **one shared variable**, not separate ones.

Visual:

debouncedHello()  
       │  
       │  
       ▼  
  closure memory  
  ┌──────────┐  
  │ timer=103│  
  └──────────┘

Every call updates that same `timer`.

---

# 7. If closure didn't exist

Each call would create a **new timer variable**, and debouncing would fail.

You'd get:

timer1  
timer2  
timer3

All running independently.

---

✅ **Simple summary**

The timer is cancelled because **all calls share the same `timer` variable stored in a closure**, allowing `clearTimeout(timer)` to cancel the previously scheduled execution.