
![[namastedev.com_learn_namaste-frontend-system-design_keyboard-accessibility.png]]
## Important Note

Web applications are accessible by default.

It is often developers who accidentally make them inaccessible by:
- Replacing semantic HTML with divs
- Removing focus styles
- Ignoring keyboard navigation
- Not adding proper labels or alt text

HTML5 provides highly accessible built-in elements such as:
- button
- input
- label
- form
- nav
- header
- main

Good system design preserves and enhances this built-in accessibility.

---

## Types of Disabilities to Consider

### 1. Visual Disabilities
- Blindness
- Low vision
- Color blindness
- Light sensitivity

Requirements:
- Screen reader compatibility
- High contrast
- Proper alt text
- Scalable text

---

### 2. Hearing Disabilities
- Partial hearing loss
- Complete deafness

Requirements:
- Captions for videos
- Transcripts for audio
- Visual indicators instead of sound-only alerts

---

### 3. Motor Disabilities
- Limited hand movement
- Tremors
- Paralysis

Requirements:
- Full keyboard navigation
- Large clickable areas
- No time-sensitive interactions
- Avoid complex gestures

---

### 4. Neurological / Cognitive Disabilities
- ADHD
- Dyslexia
- Memory impairments
- Seizure disorders

Requirements:
- Clear layouts
- Simple language
- Avoid flashing content
- Consistent navigation

---

### 5. Speech Disabilities
- Difficulty speaking

Requirements:
- Avoid voice-only interaction requirements
- Provide text alternatives

---

## Temporary & Situational Disabilities

Accessibility is not only for a small fraction of people.

Everyone can experience temporary or situational limitations.

### Temporary
- Broken arm
- Eye infection
- Temporary hearing loss

### Situational
- Bright sunlight affecting visibility
- Noisy environment affecting hearing
- Holding a baby while browsing
- Low bandwidth network

Accessibility benefits everyone.

---
![[namastedev.com_learn_namaste-frontend-system-design_keyboard-accessibility 1.png]]


[[2026-02-14]]

Web accessibility
![[namastedev.com_learn_namaste-frontend-system-design_keyboard-accessibility.png]]
## Assistive Technology (AT)

Assistive Technology helps users with disabilities interact with web applications.  
Our applications must work seamlessly with these technologies.

---

### 1. Keyboard-Only Navigation

Some users cannot use a mouse and rely entirely on a keyboard.

Requirements:
- Logical tab order
- Visible focus indicators
- All interactive elements reachable via Tab
- Avoid keyboard traps
- Use proper semantic HTML elements

Important:
Never remove the default focus outline unless you replace it with an accessible alternative.

---

### 2. Screen Readers

Screen readers convert UI content into speech or braille.

Examples:
- NVDA
- JAWS
- VoiceOver

Best Practices:
- Use semantic HTML (button, label, nav, header)
- Provide meaningful alt text for images
- Use proper heading hierarchy
- Avoid empty or unclear ARIA labels

Screen readers depend heavily on structure and semantics.

---

### 3. Mouse & Pointer Devices

Some users rely on specialized pointer devices.

Requirements:
- Large clickable areas
- Avoid tiny buttons
- Do not rely only on hover interactions
- Provide click alternatives for drag-and-drop

---

### 4. Touchscreen Gestures

Users on mobile devices use touch gestures.

Requirements:
- Avoid gesture-only interactions
- Provide visible controls
- Ensure adequate spacing between elements
- Avoid precision-dependent gestures

Accessibility must work across devices.

---

### 5. Screen Magnifiers

Used by users with low vision.

Requirements:
- Responsive layouts
- Scalable text
- No content cutoff when zoomed
- Avoid fixed-height containers that clip content

Your layout must support zoom up to 200% or more.

---

# Accessibility Standards

## WCAG – Web Content Accessibility Guidelines

WCAG defines global accessibility standards.

### Levels of Compliance

Level A – Basic  
Minimum accessibility requirements.

Level AA – Intermediate (Most Recommended)  
Industry standard for most modern applications.

Level AAA – Advanced  
Highest level, often difficult to fully achieve.

Most production applications target Level AA.

---

## WCAG Principles (WebAIM Summary)

Accessibility is built on four core principles:

### 1. Perceivable
Users must be able to perceive information.

Examples:
- Alt text for images
- Captions for videos
- Sufficient color contrast

---

### 2. Operable
Users must be able to operate the interface.

Examples:
- Keyboard navigation
- No keyboard traps
- Accessible buttons and forms

---

### 3. Understandable
Users must be able to understand content and UI behavior.

Examples:
- Clear instructions
- Predictable navigation
- Consistent layouts

---

### 4. Robust
Content must work with various assistive technologies.

Examples:
- Proper HTML structure
- Standards-compliant markup
- ARIA used correctly

---

## Key Takeaway

Assistive technologies rely on well-structured, semantic, and standards-compliant applications.  
Following WCAG principles ensures inclusive, usable, and future-proof system design.

---

## One-Line Interview Summary

Accessibility standards like WCAG ensure applications are perceivable, operable, understandable, and robust across assistive technologies such as screen readers and keyboard navigation.
