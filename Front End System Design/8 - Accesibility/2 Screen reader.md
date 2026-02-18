
![[namastedev.com_learn_namaste-frontend-system-design_screen-reader (1).png]]


## Short cuts

![[namastedev.com_learn_namaste-frontend-system-design_screen-reader (1) 1.png]]


ARIA Example - 
![[namastedev.com_learn_namaste-frontend-system-design_screen-reader.png]]

# Screen Readers & ARIA (Deep Dive)

## What is a Screen Reader?

A screen reader is an Assistive Technology (AT) that:
- Converts UI content into speech or braille
- Enables keyboard-based navigation
- Reads content based on document structure and semantics

Screen readers depend heavily on semantic HTML.

---

## Examples of Screen Readers

### macOS
- VoiceOver (built-in)
- Shortcut: Cmd + F5

### Windows
- Narrator (built-in) – Ctrl + Win + Enter
- NVDA (free)
- JAWS (paid)

### Browser
- Chrome screen reader extensions

These tools interpret the accessibility tree, not just the visual UI.

---

# Accessibility Tree

Just like:
- DOM Tree
- CSSOM
- Render Tree

Browsers also create an **Accessibility Tree**.

The accessibility tree is generated based on:
- Semantic HTML
- ARIA attributes
- Element roles
- States and properties

Important:
What you visually see in the browser may differ from what a screen reader reads.

You can inspect this:
DevTools → Inspect Element → Accessibility panel

---

# HTML Best Practices for Screen Readers

## 1. Use Semantic HTML

Prefer:
- button instead of div
- nav, header, main, section
- form elements properly structured

Semantic HTML automatically improves accessibility.

---

## 2. Use Proper Headings

- h1 to h6
- Maintain logical hierarchy
- Do not skip heading levels

Screen readers use headings for navigation.

---

## 3. Use Lists Properly

- ul, ol
- li

Helps screen readers announce grouped content correctly.

---

## 4. Use Proper Links & Buttons

- Use <\a\> for navigation
- Use <\button\> for actions
- Avoid clickable divs

---

## 5. Forms

- Always use <\label\> with inputs
- Do not rely only on placeholder
- Use correct input types (email, number, password, etc.)

---

## 6. Tables

Use proper table structure:
- caption
- thead
- tbody
- th
- tr
- td

Screen readers interpret table structure for context.

---

## 7. Images

- Provide meaningful alt text
- Use aria-label when needed
- Use aria-hidden="true" for decorative images

For icon-only buttons:
- Add visually hidden text for screen readers

---

# ARIA (Accessible Rich Internet Applications)

ARIA helps enhance accessibility when semantic HTML is not enough.

Use ARIA:
- When building custom components
- When improving accessibility in legacy code
- When dynamic state changes need announcement

Rule:
Use semantic HTML first. Use ARIA only when required.

---

# ARIA is Governed by Three Concepts

## 1. Roles

Defines what an element represents.

Example:
role="button"

Used when a div behaves like a button.

---

## 2. Properties

Provide additional descriptive information.

Examples:
aria-describedby="id-ref"
aria-labelledby="id-ref"
aria-label="Close dialog"

---

## 3. States

Define dynamic conditions of elements.

Examples:
aria-pressed="true | false"
aria-expanded="true | false"
aria-checked="true | false"

States change as user interacts.

---

# Forms and ARIA

Useful ARIA attributes for forms:
- aria-label
- aria-labelledby
- aria-describedby

These improve context for screen readers.

---

# Hidden Content & Screen Readers

Important behavior:

display: none
→ Not visible on screen  
→ Not read by screen readers

For visually hidden but screen-reader-readable content:
Use a visually-hidden CSS class instead of display: none.

---

# Live Regions

Live regions allow dynamic content to be announced automatically.

aria-live values:
- assertive → announce immediately
- polite → announce when idle
- off → do not announce

Anything inside a live region is read automatically when it changes.

Example use cases:
- Form validation errors
- Success messages
- Notifications

---

# Key Takeaway

Screen readers rely on semantic HTML and ARIA attributes to construct an accessibility tree that converts UI into meaningful spoken output.

---

# One-Line Interview Summary

Screen readers interpret the accessibility tree built from semantic HTML and ARIA roles, states, and properties to provide voice-based navigation and interaction.
