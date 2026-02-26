# Long Tasks

- Level: L3
- Status: Stable
- Depth: core
- Specs:
  - Long Tasks API
  - Performance Timeline integration
- Prerequisites: Rendering Pipeline
- Next Topics: PerformanceObserver

---

## 1. Official Term

Long Task

## 2. Formal Definition

Long task adalah unit pekerjaan pada main thread
yang berjalan cukup lama (secara umum >50ms)
sehingga menghambat respons input dan update frame.

## 3. Mental Model

Saat satu task terlalu panjang,
browser tidak punya kesempatan melayani input atau merender frame tepat waktu.

### Wireframe Ringkas

```text
[Task A: 120ms] ------------------------------
No input handling / No render during this span
```

## 4. Runtime Perspective

- Thread/process: long task biasanya terjadi di main thread renderer.
- Queue model: selama long task berjalan, task lain menunggu.
- Scheduling: event loop tetap run-to-completion, tidak memotong task sinkron.
- Rendering interaction: frame budget terlewati sehingga jank meningkat.
- Dampak performa: meningkatkan input delay dan menurunkan perceived responsiveness.
- Dampak memori: operasi sinkron besar sering berkorelasi dengan alokasi objek besar sementara.
- Dampak keamanan: UI freeze dapat memperburuk UX pada flow sensitif (konfirmasi, autentikasi, dsb).

## 5. Why This Exists

Konsep long task penting untuk diagnosis responsivitas,
agar bottleneck main thread bisa diukur dan dipecah.

## 6. Minimal Code Example

```js
const start = performance.now();
while (performance.now() - start < 120) {
  // simulasi kerja sinkron berat
}
```

## 7. Common Misconceptions

- "CPU cepat berarti long task tidak relevan"
  - Koreksi: long task tetap relevan pada device/latar beban berbeda.
- "Async otomatis bebas long task"
  - Koreksi: callback async tetap bisa berisi kerja sinkron berat.

## 8. Pitfalls and Best Practices

- Pitfall: memproses dataset besar dalam satu tick.
- Pitfall: parsing/transform sinkron berat di jalur interaksi user.
- Best practice: pecah kerja menjadi chunk atau pindahkan ke worker.

## 9. Prerequisites

- [Event Loop](../L1-runtime-model/event-loop.md)
- [Rendering Pipeline](./rendering-pipeline.md)

## 10. Next Topics

- [PerformanceObserver](./performanceobserver.md)
