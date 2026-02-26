# Web Workers

- Level: L2
- Status: Stable
- Depth: core
- Specs:
  - HTML Standard (workers integration)
  - Web Workers specification context
- Prerequisites: Storage
- Next Topics: L3 - Performance and Security

---

## 1. Official Term

Web Workers

## 2. Formal Definition

Web Workers adalah mekanisme host untuk menjalankan script
pada execution context terpisah dari main thread,
dengan komunikasi melalui message passing.

## 3. Mental Model

Worker adalah "jalur kerja terpisah" untuk komputasi/background task,
sementara UI dan DOM tetap ditangani main thread.

### Wireframe Ringkas

```text
[Main Thread]
   | postMessage
   v
[Worker Thread/Event Loop]
   | postMessage
   v
[Main Thread]

DOM access: main only
```

## 4. Runtime Perspective

- Thread/process: worker berjalan pada context terpisah dari main thread dokumen.
- Queue model: tiap worker punya event loop, task queue, dan microtask checkpoint sendiri.
- Scheduling: komunikasi antar context terjadi via message queue (`postMessage`).
- Rendering interaction: pekerjaan berat di worker membantu menjaga render path main thread lebih responsif.
- Dampak performa: serialisasi data (structured clone) menambah biaya; payload besar perlu strategi transfer.
- Dampak memori: duplikasi data antar context bisa meningkatkan footprint jika tidak memakai transferable.
- Dampak keamanan: worker tidak dapat mengakses DOM dokumen langsung; tetap berada pada boundary origin/policy host.

## 5. Why This Exists

Web Workers ada agar aplikasi web bisa menjalankan komputasi
atau proses background tanpa memblokir interaksi UI di main thread.

## 6. Minimal Code Example

```js
// main.js
const worker = new Worker("worker.js");
worker.postMessage({ action: "start" });
worker.onmessage = (e) => console.log(e.data);
```

```js
// worker.js
self.onmessage = () => {
  const result = "done";
  self.postMessage(result);
};
```

## 7. Common Misconceptions

- "Worker bisa akses DOM"
  - Koreksi: worker tidak punya akses DOM dokumen utama.
- "Pindah ke worker selalu lebih cepat"
  - Koreksi: ada biaya komunikasi/serialisasi data yang harus dihitung.

## 8. Pitfalls and Best Practices

- Pitfall: mengirim payload terlalu besar terlalu sering.
- Pitfall: lifecycle worker tidak dikelola (worker dibiarkan hidup tanpa kebutuhan).
- Best practice: kirim data seperlunya, gunakan transferable untuk data biner besar, dan terminate worker saat selesai.

## 9. Prerequisites

- [Concurrency Model](../L1-runtime-model/concurrency-model.md)
- [Storage](./storage.md)

## 10. Next Topics

- L3 - Performance and Security
