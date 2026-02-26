# Browser Architecture Overview

- Level: L0
- Status: Draft
- Depth: core
- Specs:
  - HTML Standard (processing model)
- Prerequisites: Specification Landscape
- Next Topics: L1 — Runtime Model

---

## 1. Official Term

Browser Process Model

---

## 2. Formal Definition

Browser modern menggunakan multi-process architecture
untuk keamanan dan isolasi.

---

## 3. Mental Model

Komponen utama:

- Browser Process
- Renderer Process
- GPU Process
- Network Process

JavaScript berjalan di Renderer Process.

---

## 4. Runtime Perspective

Ketika Anda membuka tab:

- Browser membuat Renderer Process.
- DOM dan JavaScript berjalan di dalamnya.
- Networking bisa diproses di network service.
- Rendering akhir dikirim ke GPU process.

Isolasi ini memungkinkan Site Isolation.

---

## 5. Why This Exists

- Keamanan
- Stabilitas
- Performance

Jika satu tab crash,
tidak menjatuhkan seluruh browser.

---

## 6. Minimal Code Example

Tidak ada contoh kode.
Ini adalah arsitektur sistem.

---

## 7. Common Misconceptions

❌ "Semua tab berjalan dalam satu proses"

Koreksi:
Browser modern menggunakan multi-process model.

---

## 8. Pitfalls & Best Practices

Jangan berasumsi bahwa semua komunikasi terjadi dalam satu thread.

---

## 9. Prerequisites

Specification Landscape

---

## 10. Next Topics

L1 — Runtime Model
