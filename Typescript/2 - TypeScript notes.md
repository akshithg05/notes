
## 16/12/2025

# 1. Unions

# Unions in TypeScript — Notes

## What are Unions?
Instead of using `any`, TypeScript provides **union types**, which allow a variable to hold **one of a few specific types**.

Unions help maintain type safety while still being flexible.  
It is recommended to keep unions **limited and intentional**, rather than allowing many unrelated types.

---

## Unions with Custom Types
Unions can be used with custom data types as well.

 ![[Pasted image 20251216071005.png]]

Here, `user` can be either an `Admin` or a `User`, but nothing else.

---

## Unions in Functions
We can also use unions in function parameters and return types.

    function getUserInfo(id: string | number): string | number {
      console.log(id);
      return id;
    }

    getUserInfo(1);

In this case, TypeScript does not suggest string- or number-specific methods because it cannot be sure which type `id` is.

---

## Type Narrowing with `typeof`
To get proper method suggestions, we must **narrow the type** using checks like `typeof`.

    function getUserInfo(id: string | number): string | number {
      if (typeof id === "string") {
        console.log(id.toLowerCase());
      } else if (typeof id === "number") {
        console.log(id.toFixed(2));
      }
      return id;
    }

    getUserInfo(1);
    getUserInfo("1");

After narrowing, TypeScript knows the exact type and enables correct methods.

---

## Unions with Arrays
Unions behave differently depending on where they are applied.

    let data1: number[] = [1, 2, 3, 5];
    let data2: string[] = ["1", "2", "3"];

This means **only numbers** or **only strings**.

    let data3: string[] | number[] = [1, 2, "3"]; // ❌ wrong

This says the array must be **either all strings or all numbers**, not mixed.

    let data4: (string | number)[] = [1, 2, "3"]; // ✅ correct

This allows a mix of strings and numbers inside the array.

---

## Literal Unions
TypeScript allows unions of **exact values**, called literal types.

    let seatAllocation: "window" | "aisle" | "middle";

    seatAllocation = "window";
    seatAllocation = "aisle";
    seatAllocation = "crew"; // ❌ not allowed

This restricts the variable to only predefined values.

---

## Summary
- Unions allow multiple specific types instead of using `any`
- Type narrowing is required to safely use type-specific methods
- Union placement matters for arrays
- Literal unions restrict values to exact allowed options
- Unions provide flexibility without losing type safety

# 2. Tuples in TS - Only in TS not in JS

# Tuples in TypeScript — Notes

## What are Tuples?
Tuples are a **TypeScript-only feature** (not present in JavaScript) that represent a special kind of array where:
- The **length is fixed**
- Each position has a **specific type**

They are similar to tuples in languages like Python.

## Basic Tuple Definition
A tuple explicitly defines the type and order of elements.

    let tUser: [string, number, boolean];

    tUser = ["hc", 131, true];

Here:
- index 0 → string  
- index 1 → number  
- index 2 → boolean  

TypeScript enforces both **order** and **type**.

## More Examples

    let rgb: [number, number, number] = [255, 123, 112];

    type User = [number, string];

    const newUser: User = [112, "example@google.com"];

This guarantees:
- exactly two elements
- first is a number
- second is a string

## Why Tuples Are Useful
- They provide **strong guarantees** about data structure
- Useful when the meaning of each position is fixed
- More strict than normal arrays

## Ambiguous / Bad Behaviour of Tuples
Although tuples are fixed-length, TypeScript still allows array methods like:

- push()
- pop()
- shift()
- unshift()
- splice()

This means we can do things like:

    tUser.push("extra value");

Even though this **breaks the tuple guarantee**, TypeScript allows it due to compatibility with JavaScript array behavior.

This is a known limitation in TypeScript and is considered **not ideal**, but changing it would be a breaking change for existing codebases.

## Important Note
- Tuples are type-safe at **assignment time**
- But some array methods can bypass tuple constraints
- Developers should avoid mutating tuples using array methods

## Summary
- Tuples are fixed-length, ordered arrays with specific types
- They are a TypeScript-only feature
- They provide stronger guarantees than normal arrays
- Some array methods can still break tuple safety, so they must be used carefully
