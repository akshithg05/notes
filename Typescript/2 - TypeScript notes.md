
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
