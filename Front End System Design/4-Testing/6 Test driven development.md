
**Test-Driven Development (TDD)** is a development philosophy where **test cases are written before the actual code**.

---

## Why TDD?

According to TDD:
- Writing code first and tests later often results in tests written **just for the sake of testing**
- Such tests may not cover all edge cases or scenarios

By writing tests first, developers are forced to:
- Think through requirements clearly
- Identify edge cases early
- Define expected behavior before implementation

---

## TDD Workflow

TDD follows a simple cycle:

### 1. Write Tests (Red)
- Write test cases for the required functionality
- All tests fail initially because the code does not exist yet

### 2. Write Code (Green)
- Write the minimum amount of code needed to make the tests pass
- Focus only on satisfying the test cases

### 3. Refactor (Refactor)
- Improve code structure and readability
- Remove duplication
- Optimize logic without changing behavior

This cycle is commonly known as:

> **Red → Green → Refactor**

---

## Key Idea

> In TDD, tests define the behavior, and code is written only to satisfy those tests.

---

TDD is generally not asked in interviews, and most companies will not even do TDD, but it is good to know about it.

## Problems with TDD
- Takes a lot of time to build products (2X times).
- Even small functions and components takes a lot of time.
## Summary

- TDD emphasizes writing tests before code
- Ensures better test coverage
- Encourages cleaner, more maintainable code
- Uses the Red-Green-Refactor cycle

