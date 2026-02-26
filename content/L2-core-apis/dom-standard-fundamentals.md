# DOM Standard Fundamentals

- Level: L2
- Status: Stable
- Depth: core
- Specs:
  - DOM Standard
  - HTML Standard (integration points)
- Prerequisites: L1 - Runtime Model
- Next Topics: Event System

---

## 1. Official Term

DOM (Document Object Model)

## 2. Formal Definition

DOM adalah model objek terstruktur untuk dokumen,
yang mendefinisikan node tree, operasi manipulasi, traversal,
dan mekanisme event target pada dokumen web.

## 3. Mental Model

Dokumen HTML direpresentasikan sebagai pohon node.
Script membaca dan memodifikasi node tree ini melalui API DOM.

### Wireframe Ringkas

```text
Document
  -> html
      -> head
      -> body
          -> section
              -> h1
              -> p
```

## 4. Runtime Perspective

- Thread/process: operasi DOM utama berjalan di renderer main thread.
- Queue model: mutasi DOM terjadi dalam task berjalan; efek visual menunggu render opportunity.
- Scheduling: perubahan DOM disinkronkan ke pipeline style/layout/paint oleh host.
- Rendering interaction: DOM write/read pattern memengaruhi biaya layout.
- Dampak performa: mutasi besar tanpa batching dapat memicu jank.
- Dampak memori: node yang dilepas tapi masih direferensikan tetap retained.
- Dampak keamanan: DOM sink tertentu dapat membuka risiko XSS jika input tidak disanitasi.

## 5. Why This Exists

DOM memberi antarmuka standar lintas browser
agar dokumen dapat diinspeksi dan dimodifikasi secara terprogram.

## 6. Minimal Code Example

```js
const title = document.querySelector("h1");
title.textContent = "Updated";
```

## 7. Common Misconceptions

- "DOM adalah bagian ECMAScript"
  - Koreksi: DOM adalah Web Platform API, bukan language feature.
- "Perubahan DOM selalu langsung terlihat"
  - Koreksi: tampilan mengikuti render opportunity dan pipeline rendering.

## 8. Pitfalls and Best Practices

- Pitfall: read/write DOM bolak-balik memicu layout thrashing.
- Pitfall: menyimpan referensi node besar tanpa kebutuhan.
- Best practice: batch update DOM dan minimalkan sink berisiko.

## 9. Prerequisites

- [L1 - Runtime Model](../L1-runtime-model/index.md)

## 10. Next Topics

- [Event System](./event-system.md)
- [Timers](./timers.md)
