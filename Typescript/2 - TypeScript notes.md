
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

[[2025-12-17]]

# 3. Enums in TypeScript 

## What are Enums?
Enums are used to **restrict user choices** to a predefined set of values.  
They are a TypeScript feature that helps make code more readable and less error-prone by avoiding arbitrary values.

---

## Basic Enum
By default, enum values are **numeric** and start from `0`.

    enum SeatAllocation {
      AISLE,
      MIDDLE,
      WINDOW,
    }

    const mySeat = SeatAllocation.WINDOW;
    console.log(mySeat); // outputs 2

Here:
- AISLE → 0  
- MIDDLE → 1  
- WINDOW → 2  

---

## Custom Numeric Values
We can explicitly set the starting value. The rest will auto-increment.

    enum SeatAllocation2 {
      AISLE = 10,
      MIDDLE,
      WINDOW,
    }

Here:
- AISLE → 10  
- MIDDLE → 11  
- WINDOW → 12  

---

## String Enums
If we start using strings, **every enum member must have an explicit value**.

    enum SeatAllocation3 {
      AISLE = "AISLE",
      MIDDLE = "MIDDLE",
      WINDOW = "WINDOW",
    }

TypeScript enforces this to avoid ambiguity.

---

## Mixed Enums
We can mix string and number enums, but once a string is used, values must be explicitly defined.

    enum SeatAllocation4 {
      AISLE = "AISLE",
      MIDDLE = 3,
      WINDOW,
    }

Here:
- WINDOW will continue numeric incrementing after `MIDDLE`.

---

## `const enum` (Performance Optimization)
Sometimes TypeScript generates **extra JavaScript** for enums.  
To reduce this, we can use `const enum`.

    const enum SeatAllocation5 {
      AISLE,
      MIDDLE,
      WINDOW,
    }

This tells TypeScript to **inline the values** directly and generate less JS code.

---

## Summary
- Enums restrict values to a fixed set of options
- Default enums are numeric and start from 0
- Numeric values can be customized
- String enums require explicit values
- `const enum` reduces generated JavaScript and improves performance


# 4. Interfaces in TypeScript 

## What are Interfaces?
Interfaces are like a **blueprint** or a **loose form of a class**.  
They define the **structure** of an object — fields and method signatures — but **do not provide implementations**.

They are superficial in the sense that they describe *what* an object should look like, not *how* it works.

---

## Defining an Interface
An interface can define:
- properties (including `readonly` and optional ones)
- methods (with parameters and return types)

Example:

    interface User {
      readonly dbId: number;
      userId: number;
      name: string;
      googleId?: string;
      isActive: boolean;

      // Different ways of defining functions in interfaces
      startTrial: () => string;
      startTrial2(): string;
      getDiscount(couponcode: string): number;
    }

---

## Implementing an Interface
When an object implements an interface, it **must** follow the structure exactly.

    const user: User = {
      dbId: 123,
      userId: 1,
      name: "Akshith",
      isActive: true,

      startTrial: () => {
        return "trial started";
      },

      startTrial2: () => {
        return "trial 2 started";
      },

      getDiscount: (name: "NEWUSER") => {
        return 10;
      },
    };

- `readonly` properties cannot be modified
- Optional properties may be omitted
- All required methods must be implemented
- Method parameter names can differ, but **types must match**

---

## Why Interfaces Are Useful
- Enforce consistent object structure
- Improve readability and maintainability
- Great for defining contracts in teams
- Widely used with objects, classes, and APIs

---

## Summary
- Interfaces define the shape of objects
- They contain no implementation logic
- Methods can be defined in multiple syntactic ways
- Interfaces act as contracts for objects in TypeScript

[[2025-12-18]]

# 5. Interfaces vs Type Aliases 

## Re-opening Interfaces
One key feature of interfaces is that they can be **re-opened** and extended by declaring them multiple times.

    interface User {
      readonly dbId: number;
      userId: number;
      name: string;
      googleId?: string;
      isActive: boolean;

      startTrial: () => string;
      startTrial2(): string;
      getDiscount(couponcode: string): number;
    }

    interface User {
      githubToken: string;
    }

Here, the second `User` interface automatically **merges** with the first one, adding `githubToken`.

---

## Interface Inheritance
Interfaces support **inheritance** using the `extends` keyword.

    interface Admin extends User {
      role: "ADMIN" | "STUDENT" | "TA";
    }

This means `Admin` inherits all properties of `User` and adds its own.

---

## Using Interfaces
Any object typed as an interface must fully follow its structure.

    const user: User = {
      dbId: 123,
      userId: 1,
      name: "Akshith",
      isActive: true,
      githubToken: "abc",

      startTrial: () => {
        return "trial started";
      },

      startTrial2: () => {
        return "trial 2 started";
      },

      getDiscount: (name: "NEWUSER") => {
        return 10;
      },
    };

    const admin: Admin = {
      dbId: 456,
      userId: 1,
      name: "Anu",
      isActive: true,
      githubToken: "def",

      startTrial: () => {
        return "trial started";
      },

      startTrial2: () => {
        return "trial 2 started";
      },

      getDiscount: (name: "NEWUSER") => {
        return 20;
      },
      role: "ADMIN",
    };

---

## Key Differences Between Interfaces and Type Aliases

### Extending an Interface
Interfaces use `extends` for inheritance.

    interface Animal {
      name: string;
    }

    interface Bear extends Animal {
      honey: boolean;
    }

---

### Extending a Type Alias
Type aliases use **intersection types (`&`)** to combine structures.

    type Animal = {
      name: string;
    };

    type Bear = Animal & {
      honey: boolean;
    };

---

### Adding New Fields
Interfaces can be augmented after creation.

    interface Window {
      title: string;
    }

    interface Window {
      ts: TypeScriptAPI;
    }

This is commonly used in real-world scenarios like extending global browser objects.

Type aliases **cannot** be re-opened.

    type Window = {
      title: string;
    };

    type Window = {
      ts: TypeScriptAPI;
    };

This causes an error: duplicate identifier.

---

## Summary
- Interfaces are **extendable and mergeable**
- Interfaces support inheritance using `extends`
- Type aliases are **fixed once defined**
- Type aliases use intersections (`&`) instead of inheritance
- Prefer interfaces for object shapes and public APIs
- Prefer type aliases for unions, primitives, and complex compositions
