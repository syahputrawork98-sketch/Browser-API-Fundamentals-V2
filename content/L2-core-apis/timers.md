# Timers

- Level: L2
- Status: Stable
- Depth: core
- Specs:
  - HTML Standard (timers)
- Prerequisites: Event System
- Next Topics: Fetch

---

## 1. Official Term

Timers (`setTimeout`, `setInterval`)

## 2. Formal Definition

Timers adalah mekanisme host untuk menjadwalkan callback
setelah delay minimum tertentu atau secara periodik,
melalui task queue pada event loop.

## 3. Mental Model

Timer tidak mengeksekusi callback "tepat saat delay habis".
Timer hanya menjadwalkan callback agar masuk antrean task saat eligible.

### Wireframe Ringkas

```text
setTimeout(fn, 100)
   -> wait minimum delay
   -> enqueue timer task
   -> run when event loop picks the task
```

## 4. Runtime Perspective

- Thread/process: callback timer pada dokumen dieksekusi di main thread event loop dokumen.
- Queue model: callback timer masuk task queue, bukan microtask queue.
- Scheduling: delay minimum dipengaruhi clamping, tab visibility, dan beban thread.
- Rendering interaction: callback timer berat dapat mengganggu frame cadence.
- Dampak performa: interval terlalu rapat meningkatkan contention main thread.
- Dampak memori: interval yang tidak dihentikan menahan closure/state lebih lama.
- Dampak keamanan: timing behavior dapat dipengaruhi mitigasi precision pada environment tertentu.

## 5. Why This Exists

Timers memberi mekanisme penjadwalan dasar
untuk pekerjaan tertunda, polling ringan, dan task chunking.

## 6. Minimal Code Example

```js
const id = setInterval(() => {
  console.log("tick");
}, 1000);

setTimeout(() => clearInterval(id), 5000);
```

## 7. Common Misconceptions

- "setTimeout(0) langsung jalan"
  - Koreksi: callback tetap menunggu giliran task queue.
- "Delay timer selalu presisi"
  - Koreksi: delay adalah minimum delay, bukan jaminan waktu eksekusi absolut.

## 8. Pitfalls and Best Practices

- Pitfall: menggunakan interval untuk kerja berat kontinu.
- Pitfall: lupa `clearInterval` saat komponen/halaman tidak lagi butuh.
- Best practice: gunakan timer secukupnya dan ukur dampak terhadap responsivitas.

## 9. Prerequisites

- [Event Loop](../L1-runtime-model/event-loop.md)
- [Tasks vs Microtasks](../L1-runtime-model/tasks-vs-microtasks.md)

## 10. Next Topics

- Fetch
- URL and History
