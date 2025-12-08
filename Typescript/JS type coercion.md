In JavaScript, `NaN` stands for "Not-a-Number." It is a special value of the `Number` type that represents an undefined or unrepresentable result of a mathematical operation.

Key characteristics of `NaN`:
- Type is `number`: 
    Despite its name, `typeof NaN` returns `"number"`. This is a peculiarity of JavaScript, as `NaN` is a special numeric value according to the IEEE 754 standard for floating-point arithmetic.

- **Results from invalid operations**: 
    
    `NaN` typically arises when a mathematical operation cannot produce a valid numeric result. Common examples include:
    
    - Dividing zero by zero (`0 / 0`).
    
    - Attempting to parse a string that does not represent a valid number (e.g., `parseInt("hello")`).
    
    - Taking the square root of a negative number (`Math.sqrt(-1)`).
    

- **Does not equal itself**: 
    
    A crucial and unique characteristic of `NaN` is that it is the only value in JavaScript that is not equal to itself when compared using either loose (`==`) or strict (`===`) equality operators. For example, `NaN === NaN` evaluates to `false`.
    

- Checking for `NaN`: 
    
    Due to its unique comparison behavior, you cannot reliably check for `NaN` using `==` or `===`. Instead, use the global `isNaN()` function or the `Number.isNaN()` method. `Number.isNaN()` is generally preferred as it does not perform type coercion before the check, unlike the global `isNaN()`.



## 1. The "String Dominance" Rule (Concatenation)

The most important rule for the `+` operator is that if **either** operand is a `String`, the other operand will be converted to a `String`, and the operation becomes **string concatenation**.

This is why `1 + '1'` results in `'11'`. The number `1` is coerced into the string `'1'`, then concatenated with `'1'`.

## 2. Numeric Conversion (Addition)

If _neither_ operand is a string, JavaScript attempts to convert both operands into **numbers** and performs mathematical addition.

This is where values like `undefined`, `null`, and `boolean` are coerced into their numeric equivalents:
![[Pasted image 20251208215524.png]]

## 3. The Strict Numeric Rule

When you use subtraction or any other mathematical operator, JavaScript does not check for strings first. Instead, it aggressively coerces _both_ operands into numbers using the exact same numeric conversion rules discussed earlier: