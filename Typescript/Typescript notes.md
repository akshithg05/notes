![[Pasted image 20251208214251.png]]

![[Pasted image 20251208214804.png]]
# 1. TypeScript — Intro Notes (Enhanced)

## What TypeScript Is
- TypeScript is a **superset of JavaScript** — meaning:
  - Every valid JavaScript program is valid TypeScript.
  - TypeScript adds *extra capabilities*, mainly related to **types**.
- It does **not** add new callbacks, new loops, or new module systems.
- It lets us write JavaScript in a **more precise and predictable** way.

## Why Use TypeScript
- Its main goal is **early error detection**.
- TypeScript catches mistakes **while writing code**, not at runtime.
- It helps prevent accidental misuse of values that JavaScript normally allows.

## Compilation
- TypeScript is **compiled to JavaScript** before execution.
- Browsers and Node.js do **not** run TypeScript directly; they run the JS output.
- Think of TS as a development-time tool — not a runtime feature.

## When (Not) to Use TypeScript
- TS isn’t required everywhere, especially for:
  - very small scripts
  - quick utilities or 5–10-line files
- It’s meant for places where:
  - correctness matters  
  - the project grows  
  - multiple developers collaborate  
  - you want predictable types and fewer runtime errors  

Use it **where the benefits outweigh the overhead**.

## Core Idea: Type Safety
- JavaScript is very flexible, sometimes too flexible.
  - `"2" + 2` → `"22"`
  - `undefined + 1` → `NaN`
  - `null + 2` → `2`
- These operations technically “work,” but they’re often **logic bugs**.
- TypeScript prevents this kind of behavior by enforcing that:
  - Variables have **expected types**
  - Operations use **matching types**
  - Inconsistent or unsafe code triggers **compile-time errors**

At its heart, **TypeScript = Type Safety.**  
It helps ensure your program behaves the way you intended, *before* it even runs.


![[Pasted image 20251208221927.png]]

# 2. What TypeScript Is NOT — Notes

## TypeScript is NOT a new programming language
- TS is not a replacement for JavaScript.
- It is a **superset** that adds static type checking.
- JavaScript is still the language that actually runs.

## TS only performs static checking
- TypeScript’s main job: **analyze your code while you type**.
- Many errors TS shows would still run in plain JavaScript.
- These warnings exist to prevent future bugs.

Example:
````ts
let user = { name: "hitesh", age: 10 };
let email = user.email;   // TS error: 'email' does not exist
````

## TS is not a runtime

- Browsers and Node.js do **not** execute TypeScript directly.
- TS must be **transpiled** into plain JavaScript first.
- React uses `.tsx` when mixing TypeScript with JSX.

## TS usually means writing more code

- Types, annotations, and interfaces add extra lines.
- Example: 50 lines of TS may compile into ~10 lines of JS.
- This overhead helps maintainability and clarity.

## TS is only a development-time tool

- Production builds are always **100% JavaScript**.
- TS improves:
    - early error detection
    - predictability
    - refactoring safety
    - long-term code quality

## Summary

TypeScript is **not** a new language or a runtime.  
It is a **static analysis + type-checking layer** that makes JavaScript safer and more reliable.

## Two ways to install TypeScript
1. Global installation
2. Project-level installation using config files

Right now we focus only on the global installation.

### Global installation
npm install -g typescript  
This installs TypeScript system-wide so you can use the tsc command anywhere.

---

# 3. What is tsc?
tsc = TypeScript Compiler

## What tsc does
- Converts .ts files into .js files
- Performs static type checking before producing JavaScript
- Shows errors directly in the terminal while compiling
- Ensures the final output is valid, runnable JavaScript

## Basic usage
tsc filename.ts  
This creates: filename.js

---
# Why TS Code Cannot Run in Production

If we put TypeScript code directly into production, it will not work because browsers and Node.js cannot understand `.ts` files. This is where the tsc (TypeScript Compiler) comes in. When we run:

tsc filename.ts

the compiler converts the TypeScript file into a plain JavaScript file that the runtime can execute. The resulting JavaScript file is what actually goes into production.  

# 4. Data types

![[Pasted image 20251210154438.png]]


Some situations where typescript can be used -
![[Pasted image 20251210154933.png]]

# Common Types in TypeScript
number  
string  
boolean  
null  
undefined  
void  
object  
array  
tuple  
never  
unknown  
(and many more built-in or custom types)

These types allow TypeScript to understand what kind of data we intend to work with.

---

# Why TypeScript Helps in Real Situations

## 1. Preventing incorrect return types
When working in a team, a function might be expected to always return a specific type (for example, a string). If another developer accidentally changes the return value to a number, JavaScript will happily accept it, but TypeScript will immediately catch this mistake through static type checking.

## 2. Ensuring correct parameter types
If a function is supposed to receive two numbers, JavaScript allows passing anything — strings, null, objects, etc. This often causes runtime errors.

TypeScript enforces type safety by ensuring that the function receives only the expected types. If you pass something else, TS will flag it during development before the code runs.

`number` is for numbers like `42`. JavaScript does not have a special runtime value for integers, so there’s no equivalent to `int` or `float` - everything is simply `number`





# 5. Type Inference in TypeScript

Type annotation is optional when TypeScript can infer the type from the assigned value.

Example with explicit annotation (correct but unnecessary):
let userId: number = 3.4;

Preferred version using inference:
let userId = 3.4;

TypeScript internally treats it as:
let userId: number;

Now the type is enforced:
userId = "abc"; // Error: Type 'string' is not assignable to type 'number'

When explicit annotations are needed:
- Variables without initialization
- Function parameters
- Function return types
- Complex objects
- Union and generic types
- Public APIs
- Async patterns

Case where inference fails:
let userId; // becomes 'any' (unsafe)
userId = 5;
userId = "text"; // allowed

Correct version:
let userId: number;

Key takeaway:
Type inference reduces code, keeps type safety, and improves readability when used properly.
