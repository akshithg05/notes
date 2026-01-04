
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
