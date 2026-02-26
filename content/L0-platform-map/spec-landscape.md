
---

# 📄 content/L0-platform-map/spec-landscape.md

```md
# Specification Landscape

- Level: L0
- Status: Stable
- Depth: core
- Specs:
  - WHATWG HTML Standard
  - DOM Standard
  - Fetch Standard
  - Streams Standard
  - Infra Standard
- Prerequisites: Web Platform Layering
- Next Topics: Browser Architecture Overview

---

## 1. Official Term

Living Standard

---

## 2. Formal Definition

Sebagian besar Web Platform didefinisikan dalam bentuk Living Standard,
yang terus diperbarui tanpa versi tetap.

---

## 3. Mental Model

Web Platform bukan satu dokumen.

Ia adalah kumpulan specification yang saling merujuk.

Contoh:

- Event Loop → HTML Standard
- DOM tree → DOM Standard
- Fetch algorithm → Fetch Standard
- Stream processing → Streams Standard

---

## 4. Runtime Perspective

Specification berisi algoritma normatif seperti:

> "User agent must..."

Browser implementation (Blink, Gecko, WebKit)
menerjemahkan algoritma ini menjadi kode C++/Rust.

---

## 5. Why This Exists

Agar semua browser memiliki perilaku konsisten.

Specification adalah kontrak perilaku.

---

## 6. Minimal Code Example

Tidak ada contoh kode.
Ini adalah konsep arsitektural.

---

## 7. Common Misconceptions

❌ "MDN adalah specification"

Koreksi:
MDN adalah dokumentasi.
Specification adalah dokumen normatif.

---

## 8. Pitfalls & Best Practices

Jika ada kebingungan,
selalu periksa specification sebelum artikel blog.

---

## 9. Prerequisites

Web Platform Layering

---

## 10. Next Topics

Browser Architecture Overview
