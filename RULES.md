# Repository Rules

## 1. Scope Boundary

This repository documents Web Platform APIs in the browser environment.

Not included:
- Node.js APIs
- Framework abstractions (React, Next.js, etc.)
- Build tools / bundlers

---

## 2. Terminology Discipline

All terminology must align with:
- HTML Standard
- DOM Standard
- Fetch Standard
- Streams Standard
- ECMAScript Specification

Incorrect terms must be corrected explicitly.

---

## 3. Topic Admission Rule

A new topic must include:

- Level (L0–L5)
- Status (Draft / Stable)
- Spec reference
- Prerequisites
- Next topics

If the API is unstable or experimental → place in L5.

---

## 4. Architectural Consistency

Every topic must follow the 10-section structure:

1. Official Term
2. Formal Definition
3. Mental Model
4. Runtime Perspective
5. Why It Exists
6. Minimal Code Example
7. Misconceptions
8. Pitfalls
9. Prerequisites
10. Next Topics

---

## 5. No Scope Explosion

Advanced topics cannot be added before core runtime topics are stable.
