# Worker vs Main Thread Strategy

- Level: L7
- Status: Stable
- Depth: architecture
- Specs:
  - HTML event loop and workers context
  - Web Workers API context
- Prerequisites: L6 - Applied Systems
- Next Topics: Cache and Invalidation Architecture

---

## 1. Official Term

Worker vs Main Thread Strategy

## 2. Formal Definition

Strategi ini adalah keputusan arsitektur
untuk membagi beban kerja antara main thread (UI-critical path)
dan worker context (background/compute path),
dengan mempertimbangkan biaya komunikasi dan kompleksitas sinkronisasi.

## 3. Mental Model

Main thread diprioritaskan untuk interaksi pengguna dan rendering.
Worker digunakan untuk kerja berat non-UI.

### Wireframe Ringkas

```text
[Main Thread]
  -> UI input/render (critical)
  -> light coordination
      <-> postMessage
[Worker]
  -> heavy compute/transform
```

## 4. Runtime Perspective

- Thread/process: main thread untuk DOM/render; worker untuk compute terpisah.
- Queue model: tiap context punya queue sendiri; komunikasi via message queue.
- Scheduling: host mengatur eksekusi antar context; IPC menambah latency tertentu.
- Rendering interaction: memindah kerja berat ke worker dapat menurunkan jank.
- Dampak performa: keuntungan worker bisa hilang jika payload besar terlalu sering dikirim.
- Dampak memori: duplikasi data antar context meningkatkan footprint.
- Dampak keamanan: worker membatasi akses DOM langsung, membantu boundary pemisahan tanggung jawab.

## 5. Why This Exists

Untuk menjaga responsivitas UI sambil tetap mampu menangani pekerjaan berat
pada aplikasi web kompleks.

## 6. Minimal Code Example

```js
const worker = new Worker("compute-worker.js");
worker.postMessage({ data: bigPayload });
worker.onmessage = (e) => updateUI(e.data);
```

## 7. Common Misconceptions

- "Semua kerja harus dipindah ke worker"
  - Koreksi: tugas ringan UI-adjacent sering lebih efisien di main thread.
- "Worker selalu lebih cepat"
  - Koreksi: biaya serialization/transfer bisa mahal.

## 8. Pitfalls and Best Practices

- Pitfall: mengirim payload besar terlalu sering tanpa transferable.
- Pitfall: membangun protokol message yang tidak versioned.
- Best practice: definisikan boundary kerja, kontrak pesan, dan budget latency.

## 9. Prerequisites

- [Web Workers](../L2-core-apis/web-workers.md)
- [Scheduling and Rendering Bottleneck Analysis](../L6-applied-systems/scheduling-and-rendering-bottleneck-analysis.md)

## 10. Next Topics

- [Cache and Invalidation Architecture](./cache-and-invalidation-architecture.md)
