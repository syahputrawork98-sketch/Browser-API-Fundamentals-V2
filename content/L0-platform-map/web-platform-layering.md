# Web Platform Layering

- Level: L0
- Status: Stable
- Depth: core
- Specs:
  - ECMAScript Specification
  - HTML Standard
  - DOM Standard
- Prerequisites: none
- Next Topics: Specification Landscape

---

## 1. Official Term

Web Platform

---

## 2. Formal Definition

Web Platform adalah kumpulan specification yang mendefinisikan
API dan perilaku lingkungan browser.

Web Platform bukan bagian dari ECMAScript.

---

## 3. Mental Model

Layer arsitektur:

ECMAScript (Language)
↓
JavaScript Engine
↓
Web Platform
↓
Browser Implementation

ECMAScript hanya mendefinisikan bahasa.
Web Platform mendefinisikan lingkungan tempat bahasa berjalan.

---

## 4. Runtime Perspective

Ketika Anda menulis:

```js
fetch("https://example.com")
