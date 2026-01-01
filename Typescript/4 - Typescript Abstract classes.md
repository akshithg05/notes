# 1. Abstract Classes in TypeScript 

## Understanding the Context
Before abstract classes, it’s important to understand **interfaces**.

- When a class uses an interface → we use the `implements` keyword  
- `implements` is **only for interfaces**

For abstract classes, we use a different keyword: **`extends`**

---

## What is an Abstract Class?
An abstract class is a **blueprint** for other classes.

Key rules:
- We **cannot create objects** directly from an abstract class
- Objects can only be created from a **class that extends** the abstract class
- Abstract classes are meant to be inherited, not instantiated

This is a major difference between interfaces and abstract classes.

---

## Abstract Classes vs Interfaces

### Interfaces
- Only define structure
- Cannot contain implemented methods
- All methods are just definitions (contracts)

### Abstract Classes
- Can define **abstract methods** (blueprints using the `abstract` keyword)
- Can also define **fully implemented methods**
- Can contain constructors and state
- Act as a mix of blueprint + partial implementation

---

## Abstract Methods
Abstract methods:
- Are declared using the `abstract` keyword
- Have **no implementation**
- Must be implemented by the child class

---

## Example

    abstract class TakePhoto {
      public cameraMode: string;
      public filter: string;
      public burst: number;

      constructor(cameraMode: string, filter: string, burst: number) {
        this.cameraMode = cameraMode;
        this.filter = filter;
        this.burst = burst;
      }

      abstract getSepia(): void;

      get getBurst(): number {
        return this.burst;
      }
    }

    class Instagram extends TakePhoto {
      constructor(
        public cameraMode: string,
        public filter: string,
        public burst: number
      ) {
        super(cameraMode, filter, burst);
      }

      getSepia(): void {
        console.log("Get sepia");
      }
    }

    // const akshith = new TakePhoto("normal", "paris", 3); // ❌ Not allowed
    const akshith = new Instagram("normal", "paris", 3); // ✅ Allowed
    akshith.getSepia();
    akshith.getBurst;

---

## Key Takeaways
- Abstract classes use `extends`, not `implements`
- You cannot create instances of abstract classes
- Abstract classes can contain both abstract and concrete methods
- Child classes must implement all abstract methods
- Abstract classes allow shared logic, unlike interfaces

---

## Summary
Abstract classes provide a powerful way to define a base class with shared logic and required methods, combining the strengths of interfaces and classes while enforcing correct inheritance.

# 2. Generics in TypeScript 

## What are Generics?
Generics allow us to write **reusable and flexible code** while still preserving **type safety**.  
They help create components (not just React components, but any reusable piece of logic) that work with **multiple types** without losing information.

Even arrays in TypeScript are generics under the hood.

---

## Problem Without Generics
Without generics, we have two bad options:

### Using a specific type
    function identity(arg: number): number {
      return arg;
    }

This works, but it is **not reusable** for other types.

### Using `any`
    function identity(arg: any): any {
      return arg;
    }

This accepts all types, but:
- Loses type information
- The return type is no longer predictable
- Type safety is gone

---

## Using Unions (`|`)
    function identityOne(val: boolean | number): boolean | number {
      return val;
    }

This works, but:
- Becomes messy with more types
- Still doesn’t guarantee the return type matches the input exactly

---

## Generics Solution
Generics solve this by **capturing the type at runtime and reusing it**.

    function identityThree<Type>(val: Type): Type {
      return val;
    }

Here:
- `Type` is a placeholder
- Whatever type goes in, the **same type comes out**
- TypeScript automatically infers the type

    identityThree("3");
    identityThree(3);

---

## Shorter Generic Syntax
A common and shorter convention is using `T` instead of `Type`.

    function identityFour<T>(val: T): T {
      return val;
    }

This is functionally the same, just cleaner and more commonly used.

---

## Generics with Arrays
Arrays themselves are generics.

    const score: Array<number> = [];
    const names: Array<string> = [];

This shows how TypeScript uses generics internally for reusable structures.

---

## Why Generics Are Powerful
- Preserve type information
- Avoid `any`
- Reduce need for unions
- Enable highly reusable code
- Provide strong type inference automatically

---

## Summary
- Generics make code reusable and type-safe
- They are better than `any` and cleaner than unions
- Input and output types stay consistent
- Widely used across TypeScript (arrays, promises, APIs)
- One of the most powerful features of TypeScript


# 3. Generics with Arrays in TypeScript

## Using Generics with Arrays
Generics work very naturally with arrays and are commonly used when writing reusable functions that operate on lists of values.

Instead of fixing the array to a single type, we use a generic type parameter so the function can work with **any array type**, while still preserving type safety.

---

## Example: Generic Function with Array
    function getSearchedProduct<T>(products: T[]): T {
      // some database operations
      const myIndex = 2;
      return products[myIndex];
    }

Here:
- `T[]` means an array of some generic type `T`
- The function returns a value of type `T`
- Whatever type the array contains, the returned value will be of the **same type**

This ensures:
- No use of `any`
- Full type inference
- Reusable logic

---

## Arrow Function with Generics
Generics can also be used with arrow functions.

    const getMoreSearchProducts = <T>(products: T[]): T => {
      const myIndex = 4;
      return products[myIndex];
    };

Important note:
- The `<T>` is placed **before** the function parameters
- This syntax tells TypeScript that the function is generic

---

## Why This Is Useful
- Maintains strict type safety
- Works for arrays of numbers, strings, objects, etc.
- Ensures the return value matches the array element type
- Avoids unions and `any`

---

## Summary
- Arrays work seamlessly with generics
- `T[]` represents an array of a generic type
- Generic array functions are reusable and type-safe
- Arrow functions support generics using `<T>` syntax

# 4. Generics classes

## Multiple Generics in Functions
Generic functions can accept **more than one generic type**.

    function anotherFunction<T, U>(valueOne: T, valueTwo: U): object {
      return { valueOne, valueTwo };
    }

    anotherFunction(1, "2");

Here:
- `T` and `U` can be different types
- The function remains reusable
- TypeScript infers types automatically

---

## Constraining Generics Using `extends`
We can restrict a generic type using `extends`.

    function anotherFunction2<T, U extends number>(
      valueOne: T,
      valueTwo: U
    ): object {
      return { valueOne, valueTwo };
    }

In this case:
- `U` must be a number
- Passing a non-number for `valueTwo` causes an error
- This gives flexibility while still enforcing rules

This same idea can also be applied using object shapes or interfaces, not just primitives.

---

## Generic Classes

### What is a Generic Class?
A generic class allows the class to work with **any type**, while keeping strict type safety.

Instead of fixing the type inside the class, we use a generic placeholder.

    class Sellable<T> {
      public cart: T[] = [];

      addToCart(product: T) {
        this.cart.push(product);
      }
    }

---

## How to Understand Generic Classes
- `T` represents the type of items stored in the class
- The type is decided **when creating an instance**
- After that, the class only accepts that type

Example usage:

    const productCart = new Sellable<string>();
    productCart.addToCart("Shoes");
    // productCart.addToCart(123); ❌ not allowed

    const numberCart = new Sellable<number>();
    numberCart.addToCart(99);

Same class, different types, no duplication, full type safety.

---

## Why Generic Classes Are Useful
- Avoid code duplication
- Strong type safety without using `any`
- Reusable data containers (carts, lists, services)
- Very common in real-world TypeScript code

---

## Summary
- Functions can use multiple generics
- `extends` constrains generic types
- Generic classes store and operate on a chosen type
- The type is fixed at instantiation time
- Generics make TypeScript highly reusable and safe
