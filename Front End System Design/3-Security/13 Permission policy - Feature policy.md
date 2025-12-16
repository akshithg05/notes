
![[Pasted image 20251216063752.png]]

The **Permissions-Policy** HTTP header allows a website to **control which browser features can be used** by:

- The main document
- Any embedded **iframe** (including cross-domain iframes)

This is important because third-party iframes or scripts may try to access sensitive browser capabilities **on behalf of your application**.

---

## Why Permissions Policy Is Needed

If your application embeds:
- Third-party iframes
- Cross-domain iframes
- External scripts

they may try to access browser features like:
- Geolocation
- Camera
- Microphone
- Screen capture

Without restrictions, this could lead to **data misuse or privacy issues**.

Permissions Policy acts as a **safeguard**.

---

## Common Browser Features Controlled

Examples of features that can be restricted:

- `geolocation`
- `camera`
- `microphone`
- `autoplay`
- `display-capture`
- `picture-in-picture`

---

## Allow List Rules

Permissions Policy uses an **allow list** model.

### Empty Allow List
```
geolocation=()
```
- Feature is **disabled for all origins**
- No iframe or external source can access it

---

### Allow All
```
geolocation=*
```
- Feature is allowed for **all origins**
- Not recommended for sensitive permissions

---

### Allow Self + Trusted Origins
```
geolocation=(self "https://trusted-site.example")
```
- Allowed only for:
  - Your own site
  - Explicitly trusted domains

---

## Example: Express Middleware Using Permissions Policy

```js
app.use((req, res, next) => {
  res.setHeader(
    "Permissions-Policy",
    "geolocation=(self), camera=(), microphone=(), autoplay=(self)"
  );
  next();
});
```

### What This Does:
- `geolocation` → allowed only for your own site
- `camera` → blocked everywhere
- `microphone` → blocked everywhere
- `autoplay` → allowed only for your site

---

## Key Idea

Permissions Policy:
- Prevents misuse of browser capabilities
- Protects users from third-party iframe abuse
- Restricts what embedded content can do
- Adds another layer of client-side security

---

## Summary

- Permissions Policy controls browser feature access
- Applies to both main document and iframes
- Uses allow lists (`self`, specific domains, `*`, or empty)
- Helps protect user privacy and application security


## Summary
![[Pasted image 20251216063959.png]]