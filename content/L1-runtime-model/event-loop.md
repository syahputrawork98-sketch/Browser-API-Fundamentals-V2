# Event Loop

- Level: L1
- Status: Stable
- Depth: core
- Specs:
  - HTML Standard (event loop)
  - ECMAScript Specification (jobs and job queues)
- Prerequisites: Web Platform Layering
- Next Topics: Tasks vs Microtasks

---

## 1. Official Term

Event Loop

## 2. Formal Definition

Event loop adalah mekanisme pemrosesan pekerjaan pada host browser
yang mengatur task selection, microtask checkpoint, dan render opportunity.

Event loop adalah bagian dari HTML Standard, bukan ECMAScript language specification.

## 3. Mental Model

Setiap iterasi event loop secara konseptual:

- mengambil satu task
- menjalankan task hingga stack kosong
- menjalankan microtask checkpoint
- memberi peluang rendering

### Wireframe Ringkas

```text
[Pick Task] -> [Run Task] -> [Microtask Checkpoint] -> [Render Opportunity] -> (repeat)
```

## 4. Runtime Perspective

- Thread/process: pada dokumen biasa, eksekusi script terjadi di renderer main thread.
- Queue model: task queue untuk event/timer/network handoff; microtask queue untuk Promise reactions dan `queueMicrotask`.
- Scheduling: host scheduler memilih task yang diproses pada tiap iterasi.
- Rendering interaction: rendering tidak terjadi di tengah task sinkron panjang.
- Dampak performa: long task menunda input dan frame.
- Dampak memori: callback yang menahan referensi besar memperpanjang lifetime objek.
- Dampak keamanan: scheduling tetap berada dalam boundary proses/origin sesuai isolation model browser.

## 5. Why This Exists

Model ini memberi eksekusi deterministik dan aman untuk state UI bersama,
sekaligus menggabungkan input, network, timer, dan rendering dalam satu orkestrasi runtime.

## 6. Minimal Code Example

```js
console.log("A");
setTimeout(() => console.log("D"), 0);
Promise.resolve().then(() => console.log("C"));
console.log("B");
```

Urutan umum output: `A`, `B`, `C`, `D`.

## 7. Common Misconceptions

- "Event loop milik JavaScript"
  - Koreksi: event loop adalah model host pada HTML Standard.
- "setTimeout(0) langsung jalan"
  - Koreksi: callback timer tetap menunggu giliran task queue.

## 8. Pitfalls and Best Practices

- Pitfall: long synchronous task pada main thread.
- Pitfall: microtask chain tanpa batas.
- Best practice: pecah kerja berat dan beri kesempatan browser merender.

## 9. Prerequisites

- Web Platform Layering
- Specification Landscape

## 10. Next Topics

- [Tasks vs Microtasks](./tasks-vs-microtasks.md)
- [Rendering Opportunity](./rendering-opportunity.md)
