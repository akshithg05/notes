
## 1. `instanceof` Narrowing
`instanceof` is similar to `typeof`, but it is used to check whether an object was **created from a specific class** (using the `new` keyword).

It is commonly used when working with class-based objects.

Example:

    function typeNarrowing(x: Date | string) {
      if (x instanceof Date) {
        x.toDateString();
      } else {
        x.toUpperCase();
      }
    }

Here:
- If `x` is a `Date`, TypeScript allows Date-specific methods
- Otherwise, `x` is treated as a string
- `instanceof` works only with classes, not plain object types

---

## 2. Custom Type Guards (Basic Form)
When working with object types (not classes), we often need **custom logic** to narrow types.

Example:

    type Fish = { swim: () => void };
    type Bird = { fly: () => void };

    function isFish(pet: Bird | Fish) {
      return (pet as Fish).swim !== undefined;
    }

This works logically, but TypeScript does **not fully understand** what this function guarantees.  
So inside another function, TypeScript may still treat `pet` as `Bird | Fish`.

---

## 3. User-Defined Type Guards (`pet is Fish`)
To make TypeScript fully understand the narrowing, we use a **type predicate**.

    function isFish(pet: Bird | Fish): pet is Fish {
      return (pet as Fish).swim !== undefined;
    }

The return type `pet is Fish` tells TypeScript:
- “If this function returns true, then `pet` is definitely a `Fish`”

---

## 4. Using the Custom Type Guard
Now TypeScript correctly narrows the type in consuming functions.

    function getFood(pet: Fish | Bird) {
      if (isFish(pet)) {
        // pet is Fish here
        return "fish food";
      } else {
        // pet is Bird here
        return "bird food";
      }
    }

When hovering over `pet` inside each block:
- Inside `if` → `Fish`
- Inside `else` → `Bird`

This is **true type narrowing**, not just runtime checking.

---

## Summary
- `instanceof` is used for class-based objects
- Plain objects require custom type guards
- A function returning `pet is Fish` is called a **user-defined type guard**
- Type predicates allow TypeScript to narrow types accurately
- This enables correct IntelliSense, method access, and safer code

# 2. Discriminated Unions & `never` in TypeScript — Notes

## Discriminated Unions
A **discriminated union** is a type-narrowing pattern where we use a common literal property (usually called `kind`, `type`, or `id`) to distinguish between different object shapes.

This property acts as a **discriminator** that TypeScript can use to safely narrow types.

---

## Example: Discriminated Union

    interface Circle {
      kind: "circle";
      radius: number;
    }

    interface Square {
      kind: "square";
      side: number;
    }

    interface Rectangle {
      kind: "rectangle";
      length: number;
      breadth: number;
    }

    type Shape = Circle | Square;

---

## Narrowing Using the Discriminator
We can safely narrow the type by checking the `kind` property.

    function getTrueShape(shape: Shape) {
      if (shape.kind === "circle") {
        console.log("This is a circle");
        return Math.PI * shape.radius * shape.radius;
      } else {
        console.log("This is a square");
        return shape.side * shape.side;
      }
    }

---

## Using `switch` for Better Readability
Using `switch` with discriminated unions is often cleaner and more scalable.

    function getArea(shape: Shape) {
      switch (shape.kind) {
        case "circle":
          return Math.PI * shape.radius * shape.radius;
        case "square":
          return shape.side * shape.side;
      }
    }

---

## Problem When Adding New Types
If later we extend the union:

    type Shape = Circle | Square | Rectangle;

Our existing functions may silently miss handling `Rectangle`, which can cause logical bugs.

---

## Using `never` for Exhaustiveness Checking
To ensure **all cases are handled**, we add a `default` case with the `never` type.

    function getArea(shape: Shape) {
      switch (shape.kind) {
        case "circle":
          return Math.PI * shape.radius * shape.radius;
        case "square":
          return shape.side * shape.side;
        case "rectangle":
          return shape.length * shape.breadth;
        default:
          const _defaultForShape: never = shape;
          return _defaultForShape;
      }
    }

Here:
- If a new shape is added and not handled
- TypeScript throws an error at compile time
- This forces us to update the logic correctly

---

## Why `never` Is Important
- Ensures **exhaustive checks**
- Prevents silent logic errors
- Makes refactoring safer
- Forces the compiler to protect you

---

## Summary
- Discriminated unions use a common literal property to narrow types
- `switch` works very well with discriminated unions
- Adding `never` in the default case ensures all union members are handled
- This pattern is one of the safest ways to handle complex union logic in TypeScript
