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