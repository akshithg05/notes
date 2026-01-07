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
