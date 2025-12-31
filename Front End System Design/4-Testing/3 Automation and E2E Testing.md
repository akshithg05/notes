
- Testing makes product stable
- Many companies dont have testing teams, we have to write e2e and automation tests, it makes sure our app does not break when we add new code to it.
- Above is the main goal

## Why Testing Is Important

Testing makes a product **stable and reliable**.

- Many companies do not have dedicated testing teams.
- Developers are often responsible for writing **E2E and automation tests**.
- These tests ensure that the application **does not break when new code is added**.

**Main goal:**  
> Catch regressions early and maintain application stability.

---

## What Is Automation Testing?

Automation testing means:
- Writing **code** to test application behavior
- Eliminating or reducing **manual testing**
- Running tests repeatedly in a consistent way

---

## End-to-End (E2E) Testing

**E2E testing** validates the application from a **real user’s perspective**, covering the full flow.

Examples of E2E flows:
- Opening the browser
- Navigating to the application
- Logging in
- Performing user actions
- Verifying outcomes
- Closing the browser

All of this is done **automatically using code**, without human intervention.

---

## Puppeteer

- **Puppeteer** is a **Node.js library** used for browser automation.
- It controls browsers programmatically.
- By default, Puppeteer runs in **headless mode**.

---

## What Is Headless Browser?

A **headless browser**:
- Has all browser capabilities (DOM, JS execution, network, storage)
- Does **not** have a visible UI or screen
- Runs faster and is ideal for automation and CI environments

## Selectors (in Automation / E2E Testing)

A **selector** is a string that identifies a specific **DOM element** on a web page.

Selectors allow automation tools to **locate and interact with elements** based on:
- Tag name (e.g., `button`, `input`)
- ID (e.g., `#loginBtn`)
- Class (e.g., `.submit-btn`)
- Attributes (e.g., `[type="text"]`)
- Relationship to other elements in the DOM tree

Selectors work on the browser’s **tree-like DOM structure**, enabling precise targeting of elements for actions like:
- Clicking
- Typing
- Reading text
- Validating UI state

---

## Automation & E2E Testing Tools

Along with **Puppeteer**, there are other popular automation tools used today:

- **Cypress**
- **Selenium**
- **Playwright**

All these tools:
- Use selectors to identify DOM elements
- Automate user interactions
- Support E2E and automation testing workflows

---

## Key Takeaway

> Selectors are the foundation of automation testing — without accurate selectors, reliable E2E tests are not possible.

