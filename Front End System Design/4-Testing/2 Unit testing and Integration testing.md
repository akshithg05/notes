
## What Is Unit Testing?

**Unit testing** means testing a **small, isolated unit of code** in a larger codebase.  
A unit can be:
- A single function
- A utility
- A component (in frontend apps)

The goal is to ensure that the unit works **independently and correctly**.

---

## Jest for Unit Testing

**Jest** is a popular JavaScript testing framework.

Why Jest?
- Works very well with **JavaScript**
- Excellent support for **React**
- Supports assertions, mocks, spies, and snapshots
- Easy setup and fast execution

Jest is commonly used with frameworks like:
- React
- Angular
- Vanilla JavaScript projects

---

## Example: Unit Testing a Function

### Application Code (`app.js`)

```js
const users = [
  { name: "Akshith", age: 24 },
  { name: "Anushka", age: 18 },
  { name: "Virat", age: 37 },
  { name: "Kylian", age: 27 },
];

// Small unit of code
function sortingByAge(data) {
  return data.sort((a, b) => a.age - b.age);
}

module.exports = { sortingByAge };
```

This function is a **unit**, and we will write test cases only for this function.

---

### Test File (`app.test.js` / `app.spec.js` / __tests__ folder)

```js
const { sortingByAge } = require("./app");

test("Check if the function sorts users by age", () => {
  const users = [
    { name: "Akshith", age: 24 },
    { name: "Anushka", age: 18 },
    { name: "Virat", age: 37 },
    { name: "Kylian", age: 27 },
  ];

  const sortedData = sortingByAge(users);

  expect(sortedData[0]?.name).toBe("Anushka");
  expect(sortedData[sortedData.length - 1]?.name).toBe("Virat");
});

test("Sorted data should not be undefined", () => {
  const users = [
    { name: "Akshith", age: 24 },
    { name: "Anushka", age: 18 },
  ];

  const sortedData = sortingByAge(users);

  expect(sortedData).not.toBe(undefined);
});
```

These test cases validate:
- Correct sorting logic
- Valid return value

---

## Interview Tip

> Try to write **2–3 meaningful unit test cases** during machine coding interviews.

This shows:
- Logical thinking
- Test coverage awareness
- Code reliability mindset

---

## React Testing Library (RTL) & Testing Library

- **Testing Library** is a **superset** that provides tools for testing UI applications.
- **React Testing Library (RTL)** is a part of Testing Library, specifically for React.

Key idea:
> Test the application the way **users interact with it**, not implementation details.

---

## JSDOM

- **JSDOM** is a JavaScript-based DOM implementation.
- Jest uses JSDOM internally to simulate a browser environment.
- Allows DOM APIs like `document`, `window`, and events to work during tests.

This makes frontend unit and component testing possible **without a real browser**.

---

## Component Testing

**Component testing** is a type of **unit testing** where:
- We test **individual React components**
- Ensure a component renders and behaves correctly in isolation

---

## Integration Testing

**Integration testing** checks how **multiple components work together**.

Example:
- A form component + button + API call
- Multiple components forming a feature

When we test the interaction between components, it becomes **integration testing**.

---

## Summary

- Unit testing → test small, isolated units
- Jest → popular JS testing framework
- Component testing → unit testing for UI components
- Integration testing → multiple components working together
- RTL + JSDOM → essential for React testing

