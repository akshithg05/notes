## 9/12/2025
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
## 10/12/2025

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


# 6. ANY Keyword

## What is `any`?
The `any` keyword is often used by developers to “get away” from TypeScript’s type system. It is not a good practice because it essentially turns off all type checking for that variable.

`any` is not a special advanced type — it simply disables TypeScript’s safety checks. When we use `any`, we lose all the benefits TS provides, making it almost the same as plain JavaScript. Even the official TypeScript documentation strongly recommends avoiding `any` whenever possible.

---

## Example
If we write something like:

let hero;

function getHero() {
  return "thor";
}

hero = getHero();
console.log(hero);

In this case, `hero` becomes `any` because we did not specify a type and TypeScript cannot infer one. This means `hero` can later be reassigned to anything without TypeScript warning us.

---

## noImplicitAny
When you don’t specify a type and TypeScript cannot infer one from the context, the compiler defaults the variable to `any`.

This is usually undesirable because `any` bypasses type checking.

The compiler option noImplicitAny forces TypeScript to report an error whenever it encounters a variable that ends up with an implicit `any`. Enabling this flag helps maintain stricter and safer code by ensuring that every variable has a known, predictable type.

---

## Summary
- `any` disables TypeScript’s type safety.
- It should be avoided unless absolutely necessary.
- The compiler flag noImplicitAny prevents accidental or unintentional usage of `any`.



# 7. Functions
![[Pasted image 20251211174150.png]]
In this function which is a regular function, again we see that the type is any, which is not a good practice.
We can easily do operations like num.toUpperCase(), we should not be allowed to do this.

## Why Type Annotations Matter
In JavaScript, functions allow anything to be passed in, which can lead to unexpected behavior. Example:

function addTwo(num) {
  return num + "2";
}

addTwo(5);

Here, JS allows mixing a number with a string. In TypeScript, if we don’t specify the type, `num` becomes `any`, which is bad practice because it disables type safety.

---
## Correct Approach: Explicit Parameter Types
function addTwo(num: number) {
  return num + 3;
}

addTwo(5);

By specifying `num: number`, TypeScript ensures:
- Only numbers can be passed  
- The return value is consistent  
- The editor shows number-related methods and prevents invalid operations  

---
## Multiple Parameters Example
function login(username: string, password: string, name: string) {
  const data = { username, password, name };
  return data;
}

login(1, 2, 3);

JavaScript would accept this, but TypeScript will stop it immediately. Each parameter must match the declared type, ensuring correct usage.

---
## Default Parameters in TypeScript
let signUp = (username: string, password: string, isPaid: boolean = false) => {
  const data = { username, password };
};

signUp("Akshith", "pass");

Here, `isPaid` has a default value (`false`). This means:
- You can omit the parameter when calling the function  
- TypeScript still enforces correct types if you choose to pass it  

---
## Summary
- Always type your function parameters to avoid implicit `any`.
- TypeScript prevents incorrect arguments and enforces predictable behavior.
- Default parameters work exactly the same as in JavaScript but with type safety added.

## 12/12/2025

# 8. Function Return Types in TypeScript — Notes

## Parameter Type ≠ Return Type
In TypeScript, typing only the parameter does not restrict the return value:

function addTwo(num: number) {
  return "hello";
}

This is allowed because the function has **no declared return type**, so TS infers the return type as `string`.

---

## Enforcing the Return Type
To ensure the function returns the correct type, explicitly specify it:

function addTwo(num: number): number {
  return num + 2;
}

Now, returning anything other than a number will throw an error.

---

## Summary
- Parameter types control *inputs*.
- Declared return types control *outputs*.
- Always specify a return type when you want predictable, safe behavior.


# Type Inference in Array Methods 

When working with arrays, TypeScript is smart enough to infer the types of elements automatically.

Example:

const heros = ["thor", "ironman", "superman"];

heros.map((hero): string => {
  return hero;
});

TypeScript understands that:
- `heros` is an array of strings  
- therefore, each `hero` inside `.map()` is also a string  

Even though TS can infer the type of the **parameter**, we still explicitly specify the **return type** (`: string`) to ensure the function returns the correct and expected value.

This automatic inference keeps code clean while maintaining type safety.

## `void`
`void` is used when a function **does not return any value**.  
It may perform an action (like logging) but it does not return anything meaningful.

Example:
function consoleError(errmsg: string): void {
  console.log(errmsg);
}

A `void` function finishes normally but returns `undefined` behind the scenes.

---

## `never`
`never` is used when a function **never returns at all**.

This happens when:
- the function throws an error, or  
- the function enters an infinite loop  

Example:
function handleError(errmsg: string): never {
  throw new Error(errmsg);
}

Here the function will **never reach a return statement** — not even `null` or `undefined`.  
It simply stops execution by throwing an error, so the correct return type is `never`.

---

## Summary
- Use **void** when the function ends normally but returns nothing.
- Use **never** when the function cannot complete normally and will never return a value of any kind.


# 9. Bad behavior of objects in JS

## Typing Objects in Function Parameters
We can define object parameter types directly inside a function:

function createCourse(
  { name, fees }: { name: string; fees: number }
): { name: string; fees: number } {
  return { name, fees };
}

This syntax defines:
- the type of the object passed into the function  
- and the type of the object returned by the function  

However, this inline typing can be confusing and hard to read for larger objects.

---

## The "Bad Behaviour" of Objects
Consider the example:

function createUser({ name: string, isPaid: boolean }) {}

let newUser = { name: "hitesh", isPaid: false, email: "h@h.com" };

createUser(newUser);

Here’s the issue:
- If we pass the object **directly** into the function call, TypeScript will complain if there are extra properties.
- But if we assign the object to a variable **first**, and then pass that variable, TypeScript does **not** complain — even if the object contains extra properties like `email`.

This is a known loophole in how TypeScript handles *excess property checks*:
- **Direct object literals** → strictly checked  
- **Objects stored in variables** → allowed to have extra properties  

This can sometimes lead to unexpected or “bad” behaviour.

---

## Future Topic: Interfaces
To fix this and avoid confusing inline types, we will later use **interfaces** which provide a cleaner, stricter, and more readable way of typing objects.

We will revisit this in the upcoming section.

## 13/12/2025

# 10. Type Aliases

## What are Type Aliases?
Type aliases allow us to define a **custom named type** and reuse it across our codebase.  
This helps avoid passing complex inline type definitions directly into function parameters and return types.

They are similar to creating a **custom data type** and then using it across our code, which results in cleaner and more maintainable code.

## Example

    type Point = {
      x: number;
      y: number;
    };

    function distance(point1: Point, point2: Point): number {
      const distance = Math.sqrt(
        Math.pow(point1.x - point2.x, 2) +
        Math.pow(point1.y - point2.y, 2)
      );
      return distance;
    }

    const dist = distance({ x: 2, y: 0 }, { x: 4, y: 0 });
    console.log(dist);

## Why Type Aliases Are Useful
- They help avoid repeating complex object type definitions.
- They make function signatures cleaner and easier to read.
- They improve maintainability by allowing changes in one place.
- They clearly communicate intent by naming data structures.

## Summary
Type aliases help write cleaner, more readable, and more maintainable TypeScript code by defining and reusing custom data types consistently.

# 11. Readonly, Optional Properties & Type Composition 

## `readonly`
The `readonly` keyword is used to prevent modification of a property after it has been set.  
If someone tries to change a `readonly` field, TypeScript will throw an error during development.

This is useful for fields like IDs that should never change.

## Optional Properties
Optional fields can be defined using the `?` symbol.  
This means the property may or may not be present on the object.

TypeScript will not force the user to provide that field, but if it exists, it must match the specified type.

## Combining Types Using `&`
TypeScript allows us to **mix and match multiple types** using the intersection operator `&`.  
This is useful when a type is composed of multiple smaller, reusable parts.

A common use case is modeling structured data like credit card details.

## Example

    type User = {
      readonly _id: number;
      name: string;
      email?: string;
      isActive: boolean;
      creditCard?: CardDetails;
    };

    type CardNumber = {
      number: string;
    };

    type CardDate = {
      date: string;
    };

    type CardDetails = CardNumber & CardDate & { cvv: number };

    const user: User = {
      _id: 12345,
      name: "Akshith",
      email: "akshithg01@gmail.com",
      isActive: false,
      creditCard: {
        number: "123 123 123",
        date: "12/12/25",
        cvv: 123,
      },
    };

## Summary
- `readonly` prevents modification of important fields.
- `?` allows optional properties.
- `&` helps combine multiple types into a single, meaningful structure.
- These features make TypeScript models more expressive and maintainable.
