![[namastedev.com_learn_namaste-frontend-system-design_accessibility-tools 2.png]]

Interview cheat sheet for accessibility
![[namastedev.com_learn_namaste-frontend-system-design_accessibility-tools 1.png]]

![[namastedev.com_learn_namaste-frontend-system-design_accessibility-tools 2.png]]

# Accessibility Tools, Techniques & Interview Cheat Sheet

Accessibility is not a one-time implementation.  
It requires continuous testing using automation and manual techniques.

---

# 1. Automation Tools

Automation helps detect accessibility issues early in development and CI/CD pipelines.

## AXE (Windows)
- Browser extension
- Detects WCAG violations
- Provides actionable suggestions

## Espresso (Android)
- UI testing framework
- Supports accessibility testing for Android apps

## eslint-plugin-jsx-a11y
- Linter for React projects
- Detects accessibility violations in JSX
- Enforces best practices

## Accessibility CI/CD Plugins
- Integrated in pipelines
- Prevents deployment if accessibility violations exceed threshold

## React Aria
- Library for building accessible React components
- Handles keyboard interaction and ARIA patterns correctly

Automation is fast, but does not catch everything.

---

# 2. Manual Testing Tools

Manual testing is critical for real accessibility validation.

## Lighthouse
- Built into Chrome DevTools
- Accessibility audit report
- Highlights contrast, labels, ARIA issues

## axe DevTools
- Browser extension
- Detailed accessibility issue breakdown

## Elements Tab (DevTools)
- Inspect accessibility tree
- Check roles, states, ARIA attributes

Manual testing catches real-world usability issues.

---

# 3. Out-of-the-Box Accessible UI Libraries

Using well-designed UI libraries reduces accessibility effort.

## Material UI
- Accessible components
- Built-in keyboard navigation
- ARIA-compliant patterns

## Fluent UI
- Microsoft’s UI framework
- Designed with accessibility in mind
- WCAG-aligned components

Using accessible component libraries speeds up development.

---

# Accessibility Interview Cheat Sheet

1. Use semantic HTML
2. Add labels to form elements
3. Use proper contrast ratios
4. Write descriptive link text (avoid "Click here")
5. Use ARIA only when semantic HTML is not sufficient
6. Keep pinch-to-zoom enabled
7. Provide text for non-text content (alt text)
8. Show visible focus indicators
9. Ensure content is understandable without relying on color
10. Provide captions for video and transcripts for audio

---

# Testing for Accessibility (Practical Checklist)

## 1. Zoom Test
Zoom the page to 400%
- Content should remain usable
- No clipping or overlap

## 2. Keyboard Test
- Navigate using only Tab and Shift+Tab
- No keyboard traps
- Logical focus order

## 3. Screen Reader Test
Turn off monitor and:
- Use screen reader
- Navigate headings
- Fill forms
- Trigger modals

If it works without vision, it is accessible.

## 4. Run Lighthouse Audit
- Fix reported accessibility issues
- Ensure contrast ratios pass

## 5. Disable CSS Test
Temporarily disable CSS:
- Structure should still make sense
- Headings should be logical
- Content should remain readable

---

# Key Takeaway

Accessibility requires a combination of automation, manual validation, accessible design systems, and continuous testing.

---

# One-Line Interview Summary

Accessibility testing combines automated tools, manual validation, accessible component libraries, and structured audits to ensure inclusive and WCAG-compliant web applications.
