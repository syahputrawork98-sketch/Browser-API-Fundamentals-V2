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
  - Web IDL
- Prerequisites: Web Platform Layering
- Next Topics: Browser Architecture Overview

---

## 1. Official Term

Living Standard

## 2. Formal Definition

Sebagian besar spesifikasi Web Platform dikelola sebagai living standards,
yaitu dokumen normatif yang terus diperbarui tanpa versi rilis mayor tetap.

## 3. Mental Model

Web Platform bukan satu dokumen tunggal.
Ia adalah jaringan spesifikasi yang saling merujuk.

Contoh pemetaan:

- Event loop -> HTML Standard
- DOM tree dan event dispatch -> DOM Standard
- Fetch algorithm -> Fetch Standard
- Stream abstraction -> Streams Standard

## 4. Runtime Perspective

Spesifikasi tidak mengeksekusi kode secara langsung.
Spesifikasi mendefinisikan algoritma normatif seperti "user agent must ...".

Implementasi browser (Blink, Gecko, WebKit) menerjemahkan algoritma ini
menjadi kode engine, scheduler, networking stack, dan rendering pipeline.

Dampak praktis:

- Perilaku runtime dibentuk oleh kontrak specification
- Kompatibilitas lintas browser bergantung pada kepatuhan implementasi

## 5. Why This Exists

Landscape ini ada agar web memiliki perilaku yang konsisten,
interoperable, dan dapat diuji lintas implementasi browser.

## 6. Minimal Code Example

Tidak ada contoh kode untuk topik ini,
karena ini adalah peta arsitektur specification.

## 7. Common Misconceptions

- "MDN adalah specification"
  - Koreksi: MDN adalah dokumentasi sekunder. Sumber normatif adalah specification.
- "Semua API web didefinisikan HTML"
  - Koreksi: HTML hanya salah satu spesifikasi utama, bukan satu-satunya.

## 8. Pitfalls and Best Practices

- Pitfall: mengambil kesimpulan dari artikel tanpa mengecek sumber normatif
- Best practice: validasi istilah dan perilaku ke specification primer
- Best practice: bedakan dokumentasi edukasi vs dokumen normatif

## 9. Prerequisites

Web Platform Layering

## 10. Next Topics

Browser Architecture Overview
