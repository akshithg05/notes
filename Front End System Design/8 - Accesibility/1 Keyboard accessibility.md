
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
