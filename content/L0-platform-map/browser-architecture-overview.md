# Browser Architecture Overview

- Level: L0
- Status: Stable
- Depth: core
- Specs:
  - HTML Standard (processing model context)
- Prerequisites: Specification Landscape
- Next Topics: L1 - Runtime Model

---

## 1. Official Term

Browser Process Model

## 2. Formal Definition

Browser modern menggunakan multi-process architecture
untuk keamanan, isolasi, dan stabilitas.

## 3. Mental Model

Komponen utama:

- Browser Process
- Renderer Process
- GPU Process
- Network Service/Process

JavaScript dokumen web umumnya berjalan di Renderer Process.

### Wireframe Ringkas

```text
[Browser Process]
   |-- manages tabs/windows
   |-- coordinates navigation
   |
   +--> [Renderer Process] -> DOM, style, JS execution
   +--> [Network Service]  -> request/response pipeline
   +--> [GPU Process]      -> compositing/raster tasks
```

## 4. Runtime Perspective

Saat tab dibuka:

- Browser process menyiapkan renderer untuk dokumen
- DOM dan JavaScript dieksekusi di renderer
- Networking ditangani oleh network service/process
- Hasil render dikomposisikan melalui GPU pipeline

Implikasi:

- Isolasi proses membatasi dampak crash antar tab
- Site isolation memperketat boundary antar origin
- Komunikasi lintas proses menambah biaya koordinasi tertentu

## 5. Why This Exists

Model ini ada untuk:

- meningkatkan keamanan (isolation)
- meningkatkan stabilitas (fault containment)
- menjaga performa sistem pada skala multi-tab

## 6. Minimal Code Example

Tidak ada contoh kode langsung,
karena ini adalah konsep arsitektur sistem browser.

## 7. Common Misconceptions

- "Semua tab berjalan dalam satu proses"
  - Koreksi: browser modern menggunakan multi-process model.
- "JavaScript mengontrol seluruh pipeline render sendiri"
  - Koreksi: JavaScript hanya salah satu komponen di renderer; render final melibatkan subsistem lain.

## 8. Pitfalls and Best Practices

- Pitfall: mengasumsikan semua operasi terjadi pada satu thread/proses
- Pitfall: mengabaikan biaya komunikasi lintas proses pada fitur kompleks
- Best practice: rancang aplikasi dengan asumsi isolation boundary nyata

## 9. Prerequisites

Specification Landscape

## 10. Next Topics

L1 - Runtime Model
