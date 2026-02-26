# Concurrency Model

- Level: L1
- Status: Stable
- Depth: core
- Specs:
  - HTML Standard (event loop and workers integration)
  - Web Workers specification context
- Prerequisites: Memory Lifetime Model
- Next Topics: L2 - Core APIs

---

## 1. Official Term

Concurrency Model

## 2. Formal Definition

Concurrency model Web Platform mengatur bagaimana beberapa alur kerja
berjalan bersamaan secara terkoordinasi melalui event loop terpisah,
message passing, dan isolation antar execution context.

## 3. Mental Model

JavaScript pada dokumen utama bersifat single-threaded per context,
namun platform tetap concurrent dengan worker, network, dan subsistem lain.

### Wireframe Ringkas

```text
[Main Thread/Event Loop] <-> postMessage <-> [Worker Event Loop]
         |
         +-> UI/DOM (main only)
```

## 4. Runtime Perspective

- Thread/process: main thread menangani DOM; worker punya context dan event loop sendiri.
- Queue model: tiap context memiliki queue dan microtask checkpoint masing-masing.
- Scheduling: host mengatur eksekusi context berbeda dan komunikasi via message queue.
- Rendering interaction: kerja berat dipindah ke worker untuk mengurangi blocking main render path.
- Dampak performa: message passing dan structured clone punya biaya.
- Dampak memori: transfer data besar antar context bisa menggandakan pemakaian jika tidak memakai transferables.
- Dampak keamanan: isolation context membatasi akses langsung, termasuk larangan akses DOM dari worker.

## 5. Why This Exists

Model ini memungkinkan aplikasi web menangani kerja komputasi/network kompleks
sambil menjaga responsivitas UI dan boundary keamanan.

## 6. Minimal Code Example

```js
// main.js
const worker = new Worker("worker.js");
worker.postMessage({ type: "start" });
worker.onmessage = (e) => console.log(e.data);
```

```js
// worker.js
self.onmessage = () => {
  self.postMessage("done");
};
```

## 7. Common Misconceptions

- "JavaScript web selalu single-threaded mutlak"
  - Koreksi: main context single-threaded, tapi platform mendukung context concurrent lain.
- "Worker bisa akses DOM langsung"
  - Koreksi: worker tidak punya akses DOM dokumen utama.

## 8. Pitfalls and Best Practices

- Pitfall: memindah kerja ke worker tanpa memperhitungkan biaya serialisasi data.
- Pitfall: komunikasi terlalu chatty antar thread/context.
- Best practice: kirim payload seperlunya dan gunakan transferable untuk data biner besar.

## 9. Prerequisites

- Event Loop
- Tasks vs Microtasks
- Memory Lifetime Model

## 10. Next Topics

- [L2 - Core APIs](../L2-core-apis/index.md)
