# Event System

- Level: L2
- Status: Stable
- Depth: core
- Specs:
  - DOM Standard (events)
  - HTML Standard (event loop integration)
- Prerequisites: DOM Standard Fundamentals
- Next Topics: Timers

---

## 1. Official Term

DOM Event System

## 2. Formal Definition

Event system adalah mekanisme dispatch event pada target tree,
meliputi capturing, target, bubbling, serta default action dan cancelation behavior.

## 3. Mental Model

Event bergerak melalui jalur propagasi pada tree:

- turun (capture)
- kena target
- naik (bubble)

### Wireframe Ringkas

```text
Window
  -> Document
      -> Body
          -> Button (target)
Capture: Window -> ... -> Button
Bubble : Button -> ... -> Window
```

## 4. Runtime Perspective

- Thread/process: dispatch event UI umumnya diproses di main thread renderer.
- Queue model: input event masuk sebagai task, lalu handler dijalankan run-to-completion.
- Scheduling: host menentukan kapan event di-dispatch berdasar input/network/parser state.
- Rendering interaction: handler berat menunda frame dan respons input.
- Dampak performa: listener berlebihan pada node banyak menaikkan overhead.
- Dampak memori: listener tidak dicabut dapat menahan referensi objek/node.
- Dampak keamanan: event handling tidak aman dapat membuka jalur injeksi/logika bypass.

## 5. Why This Exists

Sistem event menyediakan mekanisme interaksi konsisten
untuk input pengguna, lifecycle dokumen, dan sinyal antar komponen UI.

## 6. Minimal Code Example

```js
document.body.addEventListener("click", (e) => {
  console.log("bubble", e.target.tagName);
});
```

## 7. Common Misconceptions

- "Event hanya bubble"
  - Koreksi: ada fase capture, target, dan bubble.
- "stopPropagation menghentikan default action"
  - Koreksi: default action dibatalkan dengan `preventDefault`, bukan `stopPropagation`.

## 8. Pitfalls and Best Practices

- Pitfall: memasang listener terlalu granular tanpa delegasi.
- Pitfall: mengandalkan urutan event antar API tanpa verifikasi.
- Best practice: gunakan event delegation dan cleanup listener yang jelas.

## 9. Prerequisites

- [DOM Standard Fundamentals](./dom-standard-fundamentals.md)
- [L1 - Runtime Model](../L1-runtime-model/index.md)

## 10. Next Topics

- [Timers](./timers.md)
