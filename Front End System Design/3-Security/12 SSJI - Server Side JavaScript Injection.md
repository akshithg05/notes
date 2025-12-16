Careful while handling - eval , new Function, setTimeout, setInterval

# Server-Side JavaScript Injection (SSJI)

Server-Side JavaScript Injection (SSJI) occurs when **user-controlled input is executed as JavaScript on the server**.  
This allows attackers to run unintended code, access internal resources, or manipulate server behavior.

---

## What Causes SSJI

### 1. Inadequate Input Validation
User input is not properly validated or sanitized before being processed.

Example risk:
```js
const userInput = req.body.input; // untrusted input
```

If this input is later executed or trusted blindly, it can lead to injection.

---

### 2. Direct Execution of User-Provided Code
Executing user input as JavaScript is extremely dangerous.

Example (insecure):
```js
const userCode = req.body.code;
eval(userCode); // Executes attacker-controlled code
```

This allows full server-side code execution.

---

### 3. Using Dangerous Functions
Functions like:
- `eval()`
- `new Function()`

can execute dynamic code and must **never** be used with user input.

Example risk:
```js
new Function(userInput)();
```

---

### 4. Insecure Deserialization
Deserializing user-provided data without validation can allow attackers to inject malicious structures or logic.

Example risk:
```js
const serializedData = req.body.data;
const obj = deserialize(serializedData); // unsafe
```

---

## Mitigation Strategies

### 1. Validate User Input
Always validate input using strict rules (whitelisting preferred).

Example:
```js
function isValidInput(input) {
  const regex = /^[a-zA-Z0-9\s]+$/;
  return regex.test(input);
}
```

Reject anything that does not match expected patterns.

---

### 2. Never Use `eval()`
Do **not** execute user input as code.

Correct approach:
```js
const userInput = req.body.input;
// Treat as data, not executable code
```

---

### 3. Avoid `new Function()`
Do not dynamically create functions from user input.  
Use predefined logic instead of dynamic execution.

---

### 4. Validate Before Deserialization
Only deserialize trusted formats and validate the resulting object.

Example (safer approach):
```js
try {
  const data = JSON.parse(req.body.data);
  if (isValidData(data)) {
    // process data
  } else {
    res.status(400).send('Invalid data');
  }
} catch (err) {
  res.status(500).send('Error while deserializing data');
}
```

---

## Summary

SSJI happens when:
- User input is treated as executable JavaScript
- `eval()` or `new Function()` is used
- Deserialization is done without validation

Key defenses:
- Strict input validation
- Never execute user-provided code
- Avoid dangerous JavaScript functions
- Validate data before deserialization

Server-side JavaScript must **always treat user input as data, never as code**.
