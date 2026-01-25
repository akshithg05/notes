## Normalization (State Management & API Caching)

### What is Normalization?
Normalization is the process of flattening complex or nested data by storing entities separately and linking them using unique IDs instead of deeply nesting objects.

Instead of duplicating related data, we store it once and reference it.

---

### Simple Concept Example

Unnormalized (nested data):

```js
student = {
  name: "Akshith",
  city: "Bengaluru",
  college: {
    id: "clg1",
    name: "BMS"
  }
}
```

Problem:
If thousands of students belong to the same college, the college object is duplicated for every student.

Normalized approach:

```js
student = {
  name: "Akshith",
  city: "Bengaluru",
  collegeId: "clg1"
}

college = {
  id: "clg1",
  name: "BMS"
}
```

Now the same collegeId can be referenced by many students.

---

### Why We Normalize Data
- Removes redundancy – data is stored once and reused via references
- Improves efficiency – faster lookups (O(1) instead of O(n))
- Simplifies updates – update data in one place instead of deep nesting
- Enhances caching – entities can be cached independently
- Improves scalability – works well for large and growing datasets

---

### Example: Unnormalized State

```js
state = {
  users: [
    {
      id: 1,
      name: "Alice",
      posts: [
        { id: 101, title: "Post 1" },
        { id: 102, title: "Post 2" }
      ]
    },
    {
      id: 2,
      name: "Bob",
      posts: [
        { id: 103, title: "Post 3" }
      ]
    }
  ]
}
```

Problem:
To find a post, we must iterate through users and their posts → O(n) time.

---

### Example: Normalized State

```json
state = {
  users: {
    byId: {
      1: { id: 1, name: "Alice", postIds: [101, 102] },
      2: { id: 2, name: "Bob", postIds: [103] }
    },
    allIds: [1, 2]
  },

  posts: {
    byId: {
      101: { id: 101, title: "Post 1", userId: 1 },
      102: { id: 102, title: "Post 2", userId: 1 },
      103: { id: 103, title: "Post 3", userId: 2 }
    },
    allIds: [101, 102, 103]
  }
}
```

Benefits:
- Direct access to any entity → O(1)
- Clear relationships between data
- Easier updates and better cache control

---

### Where Normalization Is Commonly Used
- State management (Redux, Zustand, RTK Query)
- API response caching
- Large frontend applications
- Relational data (users, posts, comments, tags)

---

### One-Line Interview Summary
Normalization flattens nested data by storing entities separately using IDs, improving performance, scalability, and cache efficiency.
