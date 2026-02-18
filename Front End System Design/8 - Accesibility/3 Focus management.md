![[namastedev.com_learn_namaste-frontend-system-design_focus-management.png]]

# Focus Management (Accessibility Deep Dive)

Focus management ensures that keyboard users and screen reader users can navigate the application in a predictable and logical way.

Proper focus handling is critical for accessibility, especially in SPAs and dynamic UI components.

We will discuss 6 key techniques.

---

## 1. Tab Navigation

Pressing Tab moves focus forward.  
Pressing Shift + Tab moves focus backward.

By default, HTML5 provides tabbing functionality for:
``` html
- <a>
- <button>
- <input>
- <textarea>
- <iframe>
- <select>
```

No fancy JavaScript is required when using semantic HTML correctly.

---

### tabindex

If using custom elements like div:

tabindex values:
- tabindex="0" → focusable in DOM order
- tabindex="-1" → not tabbable but focusable via JS
- tabindex="1,2,3..." → manual order (avoid this)

Best Practice:
- Avoid manual tab ordering (1,2,3...)
- Prefer semantic HTML
- Use tabindex="0" only when necessary

When tabindex="0" is used, focus follows DOM order.

---

## 2. Keyboard Shortcuts

Keyboard shortcuts improve accessibility and productivity.

Example:
document.addEventListener("keydown", function(e) {
  if (e.key === "k" && e.ctrlKey) {
    console.log("Search shortcut triggered");
  }
});

Guidelines:
- Avoid overriding common browser shortcuts
- Make shortcuts discoverable
- Ensure shortcuts are accessible to screen readers

---

## 3. Skip Links

When a page loads, tabbing starts from the top (usually navigation).

To avoid tabbing through many header links, use a "Skip to main content" link.

Example:

<a href="#main-content" class="skip-link">
  Skip to main content
</a>

```html
<main id="main-content">
  ...
</main>
```

This allows keyboard users to jump directly to the main content.

Common in accessible websites.

---

## 4. Active Element (Focus Return)

When opening a modal from a button, focus must return to the same button after closing the modal.

Example:

``` js
const openBtn = document.getElementById("openModal");
const modal = document.getElementById("modal");

openBtn.addEventListener("click", () => {
  modal.style.display = "block";
  modal.focus();
});

function closeModal() {
  modal.style.display = "none";
  openBtn.focus();   // Return focus to triggering element
}
```

This preserves logical navigation flow.

---

## 5. Tab Trapping

When inside a modal, focus should remain inside the modal while tabbing.

Focus must not move outside the modal.

Example (basic concept):

``` js
modal.addEventListener("keydown", function(e) {
  if (e.key === "Tab") {
    e.preventDefault();
    modal.focus();
  }
});
```

In real implementations:
- Identify first and last focusable elements
- Cycle focus between them
- Prevent focus escape

Tab trapping ensures accessible modal behavior.

---

## 6. Page Navigation (SPA Focus Management)

In Single Page Applications (React, Angular, Vue):

Page changes do not reload the document.

Therefore:
- Screen readers may not detect page changes automatically
- Focus must be manually managed

Best Practices:

1. Use skip links
2. Move focus to main content on route change

Example:

const contentElement = document.getElementById("main-content");
contentElement.focus();

3. Use aria-live to announce page changes

Example:

<div aria-live="polite">
  Page updated
</div>

This informs screen readers that content has changed.

---

# Key Takeaway

Focus management ensures predictable keyboard navigation, proper modal behavior, and correct screen reader announcements, especially in dynamic applications.

---

# One-Line Interview Summary

Focus management ensures logical keyboard navigation and screen reader compatibility by controlling tab order, restoring focus, trapping focus in modals, and handling SPA navigation correctly.
