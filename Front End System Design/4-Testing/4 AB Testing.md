# A/B Testing (Split Testing / Bucket Testing)

**A/B Testing**, also called **Split Testing** or **Bucket Testing**, is primarily driven by **product and business decisions**.  
It is not always a developer’s day-to-day task, but it is **important for senior engineers** to understand how it works and why it is used.

A/B testing helps teams make **data-driven decisions** instead of relying on assumptions.

---

## Why A/B Testing Is Used

Product managers often use A/B testing to answer questions like:
- Which button text works better?
- Which UI layout increases engagement?
- Which thumbnail attracts more clicks?

Instead of guessing, real user data is used to decide.

---

## Example: CTA (Call-To-Action) Button

Suppose a website has multiple options for naming a button (CTA).

Steps:
1. Create **two versions** of the button (Version A and Version B)
2. Show:
   - Version A to one group of users
   - Version B to another group
3. Measure engagement:
   - Number of clicks
   - Conversion rate
4. Choose the version with **better performance**

This testing is done on a **large pool of users** to ensure reliable results.

---

## Variations in A/B Testing

- You can test **2 or 3 versions** (A/B or A/B/C testing)
- Avoid testing too many variations at once
- Fewer variants = clearer results

Example:
- YouTube testing different thumbnails for the same video

---

## Data-Driven Decisions

Decisions based on A/B testing are called **data-driven decisions**.

Benefits:
- Removes guesswork
- Improves user engagement
- Helps companies scale to a large user base
- Aligns product changes with real user behavior

---

## A/B Testing Tools

Some commonly used A/B testing tools:
- **Wasabi (by Intuit)**
- **Google Optimize**
- **AB Tasty**

These tools can:
- Show different versions for mobile vs desktop
- Collect analytics
- Generate dashboards and reports

---

## Technical Perspective

From a technical point of view:
- When a user makes an API call, the A/B testing tool:
  - Randomly assigns the user to a version
  - Serves the corresponding UI or feature
  - Tracks user interactions
- The tool handles:
  - User bucketing
  - Analytics
  - Reporting

Developers mainly integrate the tool; **experiment logic is handled by the platform**.

---

## Summary

- A/B testing compares multiple versions of a feature
- Decisions are based on real user data
- Commonly driven by product teams
- Helps in scaling products efficiently
- Widely used for UI, UX, and conversion optimization

