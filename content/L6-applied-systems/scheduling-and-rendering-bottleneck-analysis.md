# Scheduling and Rendering Bottleneck Analysis

- Level: L6
- Status: Stable
- Depth: applied
- Specs:
  - HTML event loop context
  - Performance Timeline context
  - Rendering pipeline context
- Prerequisites: Race Condition Diagnosis
- Next Topics: L7 - Architecture Decisions

---

## 1. Official Term

Scheduling and Rendering Bottleneck Analysis

## 2. Formal Definition

Analisis bottleneck scheduling dan rendering adalah proses
mengidentifikasi titik keterlambatan pada task/microtask flow
serta pipeline render yang menyebabkan jank, input delay, atau frame drop.

## 3. Mental Model

Gejala UI lambat bisa berasal dari dua sisi utama:

- antrian eksekusi (scheduling)
- biaya visualisasi (rendering)

### Wireframe Ringkas

```text
[Input/Event]
  -> Task queue delay?
  -> Long task?
  -> Microtask storm?
  -> Render pipeline cost?
  => identify primary bottleneck
```

## 4. Runtime Perspective

- Thread/process: fokus utama di renderer main thread + koordinasi GPU/network bila relevan.
- Queue model: lihat distribusi task vs microtask dan durasinya.
- Scheduling: cek starvation, prioritas task, dan blocking sync work.
- Rendering interaction: cek style/layout/paint/composite cost per frame.
- Dampak performa: bottleneck tunggal bisa mengkaskade ke INP/FPS buruk.
- Dampak memori: churn object/layer tinggi memperburuk stabilitas frame time.
- Dampak keamanan: instrumentation harus menjaga data sensitif saat profiling produksi.

## 5. Why This Exists

Agar optimasi performa berbasis data,
bukan asumsi, dan fokus pada bottleneck paling berdampak.

## 6. Minimal Code Example

```js
const obs = new PerformanceObserver((list) => {
  for (const e of list.getEntries()) {
    console.log(e.entryType, e.duration);
  }
});
obs.observe({ type: "longtask", buffered: true });
```

## 7. Common Misconceptions

- "Semua jank disebabkan CSS"
  - Koreksi: bisa dari JS scheduling, network callbacks, atau kombinasi.
- "Optimasi micro saja pasti cukup"
  - Koreksi: perlu lihat bottleneck dominan end-to-end.

## 8. Pitfalls and Best Practices

- Pitfall: optimasi komponen yang bukan bottleneck utama.
- Pitfall: profiling tanpa baseline dan tanpa skenario reproduksi konsisten.
- Best practice: tetapkan baseline metric, lakukan perubahan bertahap, verifikasi regresi.

## 9. Prerequisites

- [Rendering Pipeline](../L3-performance-and-security/rendering-pipeline.md)
- [Long Tasks](../L3-performance-and-security/long-tasks.md)
- [PerformanceObserver](../L3-performance-and-security/performanceobserver.md)

## 10. Next Topics

- L7 - Architecture Decisions
