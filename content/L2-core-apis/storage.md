# Storage

- Level: L2
- Status: Stable
- Depth: core
- Specs:
  - HTML Standard (Web Storage)
  - IndexedDB specification context
  - Storage Standard (quota/partition context)
- Prerequisites: URL and History
- Next Topics: Web Workers

---

## 1. Official Term

Web Storage and Client-Side Storage Model

## 2. Formal Definition

Storage API pada web menyediakan mekanisme persistensi data klien
seperti `localStorage`, `sessionStorage`, dan penyimpanan terstruktur (IndexedDB),
dengan batas quota dan kebijakan origin.

## 3. Mental Model

Setiap origin memiliki "ruang simpan" sendiri.
Jenis storage berbeda pada kapasitas, sinkron/asinkron, dan use case.

### Wireframe Ringkas

```text
[Origin Storage Bucket]
  -> localStorage (sync, kecil)
  -> sessionStorage (sync, per-tab-session)
  -> IndexedDB (async, besar/terstruktur)
```

## 4. Runtime Perspective

- Thread/process: Web Storage API sync di main thread; IndexedDB async via subsistem database browser.
- Queue model: operasi async (IndexedDB) menghasilkan callback/event melalui event loop.
- Scheduling: akses sync blocking lebih berisiko untuk respons UI.
- Rendering interaction: operasi sync berulang pada jalur render dapat menambah jank.
- Dampak performa: serialisasi besar di storage sync mahal.
- Dampak memori: cache + storage tanpa kebijakan invalidasi meningkatkan footprint.
- Dampak keamanan: storage terikat origin, tetapi data sensitif tetap perlu enkripsi/mitigasi XSS.

## 5. Why This Exists

Aplikasi web membutuhkan persistensi lokal
untuk offline capability, state continuity, dan caching data.

## 6. Minimal Code Example

```js
localStorage.setItem("theme", "dark");
const theme = localStorage.getItem("theme");
```

## 7. Common Misconceptions

- "localStorage cocok untuk data besar"
  - Koreksi: localStorage terbatas dan sinkron; data besar lebih cocok IndexedDB.
- "Data di storage aman dari XSS"
  - Koreksi: script berbahaya pada origin yang sama bisa mengakses storage.

## 8. Pitfalls and Best Practices

- Pitfall: menyimpan token sensitif tanpa pertimbangan threat model.
- Pitfall: menyimpan objek besar berulang di localStorage.
- Best practice: pilih storage sesuai karakter data dan akses pattern.

## 9. Prerequisites

- [URL and History](./url-and-history.md)
- [Memory Lifetime Model](../L1-runtime-model/memory-lifetime-model.md)

## 10. Next Topics

- Web Workers
