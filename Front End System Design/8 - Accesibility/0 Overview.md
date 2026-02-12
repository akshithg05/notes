![[namastedev.com_learn_namaste-frontend-system-design_accessibility-overview.png]]
# Accessibility
## Overview

Accessibility (a11y) ensures that the web applications we build are usable by **everyone**, including people with disabilities such as:

- Visual impairments (blindness, low vision, color blindness)
- Hearing impairments
- Motor impairments
- Cognitive disabilities

An inclusive web is a better web.

---

## What is Accessibility?

Accessibility means designing and building applications so that people using Assistive Technology (AT) can interact with them effectively.

Accessibility is not an optional feature — it is a core part of good system design.

---

## Why Accessibility is Important

- Inclusivity and equal access
- Legal compliance (many countries mandate accessibility standards)
- Better UX for all users
- Improves SEO
- Enhances overall design quality

---

## Assistive Technology (AT)

Assistive technologies help users interact with digital systems.

Examples:
- Screen readers
- Voice control software
- Keyboard navigation
- Braille displays
- Screen magnifiers

Our applications must be compatible with these tools.

---

## Accessibility Standards

### WCAG (Web Content Accessibility Guidelines)

Defines principles:
- Perceivable
- Operable
- Understandable
- Robust

Applications are rated:
- A
- AA (most common requirement)
- AAA

Following WCAG ensures structured and accessible experiences.

---

## ARIA (Accessible Rich Internet Applications)

ARIA provides additional attributes to improve accessibility for dynamic content.

Examples:
- aria-label
- aria-hidden
- aria-expanded
- role attributes

ARIA helps screen readers understand:
- Component purpose
- State changes
- Interactive elements

Important:
Use semantic HTML first. Use ARIA only when necessary.

---

## Screen Readers

Screen readers convert UI content into:
- Speech output
- Braille output

Examples:
- NVDA
- JAWS
- VoiceOver

Best practices:
- Proper heading hierarchy
- Meaningful alt text for images
- Labels for form inputs
- Avoid div-based buttons without proper roles

---

## Focus Management

Users navigating via keyboard rely on focus indicators.

Best practices:
- Logical tab order
- Visible focus states
- Avoid removing outline styles
- Use tabindex correctly
- Manage focus for modals and dialogs

Focus must never get trapped unintentionally.

---

## Contrast & Themes

Ensure proper visual accessibility.

### Color Contrast
- Maintain proper contrast ratio
- Avoid low contrast text
- Support users with color blindness

### Light/Dark Mode
- Provide theme flexibility
- Ensure contrast remains accessible in both modes

Do not rely on color alone to convey meaning.

---

## Tooling for Accessibility Testing

Automated Tools:
- Lighthouse
- axe DevTools
- WAVE

Manual Testing:
- Keyboard-only navigation
- Screen reader testing
- Contrast checking tools

Accessibility requires both automated and manual validation.

---

## Practical Examples

Good:
- button for buttons
- label for form inputs
- alt text for images
- Proper heading structure (h1 → h2 → h3)

Bad:
- Clickable divs without role
- Missing alt attributes
- No focus states
- Placeholder used instead of label

---

## Key Takeaway

Accessibility ensures that applications are inclusive, usable, and compliant by supporting assistive technologies, proper semantics, and inclusive design principles.

---

## One-Line Interview Summary

Accessibility is the practice of building inclusive web applications that support assistive technologies, follow accessibility standards, and ensure usability for all users.
