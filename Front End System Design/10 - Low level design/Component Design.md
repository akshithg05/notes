## Core Idea

Everything in UI design (React / Angular) is a **component**.

A component is a normal JavaScript function which returns JSX.  
JSX returns a **React element**, which ultimately renders a **UI element**.

Everything visible in a React application is a component:
- A small button
- A navbar
- A card
- An entire page
- The entire application

All of these are components of different sizes.

---
## Component Composition

A web application is built by combining many smaller components together.
This process is called **Component Composition**.
Large components are composed of smaller components, which may themselves contain smaller components.

Example:

- App
    - Header    
        - Logo
        - Navbar
    - Body
        - Containers
        - Cards
        - Sections

The entire UI is built by **composing many small reusable components**.

---
## Important Principle

Never start writing code directly.
First perform **Component Design**.

Steps:

1. Understand the UI mock given by the designer.
2. Break the UI into components.
3. Define the component hierarchy.
4. Then start writing code.

Benefits:

- Avoid unnecessary divs
- Avoid rewriting code
- Clear structure before implementation
- Easier maintenance

---
# Steps for Component Design

1. The designer provides a **UI mock**.
2. From the mock we identify the UI structure.

In most basic websites we typically see:

- Header
- Logo
- Navbar
- Body
- Content sections
- Cards
- Containers

Every small part should be treated as an **individual component**.

Example:
- Header → Component
- Logo → Component
- Navbar → Component
- Menu container → Component

---
## Component Composition Example

Header can be broken into smaller components.
Header
- LeftSection
    - Logo
- RightSection
    - Menu

The header is composed of two inner components.
These components can be **further nested**.

---
## Important Note

There is **no single correct way** to break down components.
There are **many ways to design the same UI**.

However, a good approach is:
**Start from the top-level component and progressively break it down into smaller components.**

This makes the UI structure easier to understand and implement.

---
## Example UI Breakdown

This example represents a typical application layout.

Pseudo structure:

AppComponent  
 Header  
  LeftSection  
   Logo  
    img

  RightSection  
   Menu  
    Tabs

 Body  
  MultipleScrollableRows  
   Card  
   Card  
   Card

AppComponent is the **root component**.  
Everything in the application exists inside this component.

---
# What Interviewers Expect

In frontend system design interviews, you should **first explain the component breakdown** before writing code.

Even simple looking UIs contain **hidden design challenges and edge cases**.

---

# Example: YouTube Sidebar Problem

Consider a YouTube-like UI.

There is a **hamburger icon in the header**.

When clicked:

- A **left side collapsible navigation panel** opens.
- The panel **expands and collapses smoothly**.

At first glance this looks easy, but there are design considerations.

---
## Code Design Goals

A good design should ensure the code is:
1. Modular
2. Reusable
3. Readable
4. Testable
---
## Key Observation

In the UI:
- The **hamburger icon is inside the Header**
- The **navigation panel is part of the Body**

When collapsed:
- Only a few options appear
When expanded:
- Many options appear
---
## Common Mistake

Many developers place the **sidebar inside the Header component**.
This is not technically wrong, but it often leads to:

- Complex CSS
- Difficult layout management
- Poor readability
---
## Better Design Approach

Place the sidebar inside the **Body component**.
Structure:

Body  
 LeftNavigationContainer

Inside this container create two components:
- CollapsedMenu
- ExpandedMenu

---
## Why This Works Better

Advantages:
- Clear separation of concerns
- Easier debugging
- Better modularity
- Cleaner code

---
## Conditional Rendering

Use a **state variable** to decide which component to render.
Example logic:
If menu is collapsed → render CollapsedMenu  
If menu is expanded → render ExpandedMenu

---

## Why Two Separate Components

The collapsed and expanded menus contain:
- Different layouts
- Different number of items
- Different UI elements

Keeping them as **separate components** improves:
- Modularity
- Maintainability
- Code clarity

This is a good way to do things. When we start writing code we will know how hard it is.