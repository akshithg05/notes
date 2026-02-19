
![[namastedev.com_learn_namaste-frontend-system-design_color-contrast.png]]

Color contrast ensures that text and UI elements are clearly distinguishable from their background.

Proper contrast is essential for users with:
- Low vision
- Partial blindness
- Blurry vision
- Color blindness
- Light sensitivity

Good contrast improves readability for everyone.

---

## Why Color Contrast Matters

Poor contrast can make content:
- Hard to read
- Invisible in bright sunlight
- Difficult for aging users
- Unusable for visually impaired users

Accessibility standards define minimum contrast ratios to ensure readability.

---

## WCAG Contrast Ratio Standards

### Small Text (< 18px)
Minimum contrast ratio: 4.5:1

### Large Text (≥ 18px)
Minimum contrast ratio: 3:1

These ratios ensure readable content across various visual conditions.

---

## How to Check Contrast

Using Browser DevTools:
1. Inspect element
2. Go to Styles panel
3. Click on the color picker
4. View contrast ratio information

Tools:
- Lighthouse
- axe DevTools
- WebAIM Contrast Checker

---

## Font Size & Scalability

Applications must support:
- Adjustable font sizes
- Browser zoom
- Responsive layouts

Best Practices:
- Use rem or em instead of px for font sizing
- Avoid fixed-height containers
- Avoid clipping text

Content should remain usable up to **400% zoom level**.

---

## Dark Mode & Light Mode

Applications should support:
- Light mode
- Dark mode

Guidelines:
- Light mode → Dark text on light background
- Dark mode → Light text on dark background
- Avoid pure white (#FFFFFF) or pure black (#000000) for long text
- Use comfortable, eye-friendly color palettes

---

## CSS Media Queries for Preferences

Use user preference queries:

prefers-color-scheme:
- light
- dark

Example:
@media (prefers-color-scheme: dark) {
  body {
    background-color: #121212;
    color: #f5f5f5;
  }
}

prefers-contrast:
- more
- less

Example:
@media (prefers-contrast: more) {
  body {
    font-weight: bold;
  }
}

These respect user accessibility settings.

---

## Do Not Rely on Color Alone

Avoid:
- Red text alone to indicate error
- Green text alone to indicate success

Always combine color with:
- Icons
- Labels
- Text messages

Example:
Instead of only red border for error → Add "Error: Invalid input"

---

## Key Takeaway

Color contrast and scalable design ensure that content remains readable and usable across different lighting conditions, visual impairments, and device settings.

---

## One-Line Interview Summary

Color contrast ensures readable and accessible UI by following WCAG ratio standards, supporting zoom and theme preferences, and respecting user visual settings.
