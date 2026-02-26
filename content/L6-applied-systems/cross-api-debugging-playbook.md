# Cross-API Debugging Playbook

- Level: L6
- Status: Stable
- Depth: applied
- Specs:
  - HTML Standard (event loop and lifecycle context)
  - Performance Timeline context
  - API-specific standards sesuai kasus
- Prerequisites: L5 - Watchlist and Experimental
- Next Topics: Race Condition Diagnosis

---

## 1. Official Term

Cross-API Debugging Playbook

## 2. Formal Definition

Cross-API debugging playbook adalah pendekatan sistematis
untuk mendiagnosis masalah runtime yang melibatkan lebih dari satu API,
misalnya interaksi Fetch + DOM + Timers + Storage + Worker.

## 3. Mental Model

Masalah produksi jarang berasal dari satu API tunggal.
Debugging efektif butuh jejak sebab-akibat lintas subsistem.

### Wireframe Ringkas

```text
[Symptom]
  -> [Trace timeline]
  -> [Map involved APIs]
  -> [Form hypothesis]
  -> [Validate with instrumentation]
  -> [Fix + regressions check]
```

## 4. Runtime Perspective

- Thread/process: identifikasi context eksekusi tiap gejala (main, worker, network, GPU).
- Queue model: petakan task/microtask/event source yang relevan.
- Scheduling: cari titik starvation, long task, atau delay di boundary async.
- Rendering interaction: hubungkan delay data dengan dampak frame/input.
- Dampak performa: instrumentation berlebihan bisa memengaruhi hasil jika tidak terkontrol.
- Dampak memori: logging/data capture berlebih dapat menambah pressure.
- Dampak keamanan: debugging data produksi harus menjaga privasi dan boundary akses.

## 5. Why This Exists

Karena bottleneck nyata sering muncul dari interaksi antar API,
bukan dari bug isolated pada satu komponen.

## 6. Minimal Code Example

```js
performance.mark("before-fetch");
const res = await fetch("/api/data");
performance.mark("after-fetch");
performance.measure("fetch-latency", "before-fetch", "after-fetch");
```

## 7. Common Misconceptions

- "Kalau gejala di UI, bug pasti di DOM"
  - Koreksi: akar masalah bisa di network, scheduling, atau storage.
- "Satu log sudah cukup membuktikan akar masalah"
  - Koreksi: perlu korelasi lintas sinyal runtime.

## 8. Pitfalls and Best Practices

- Pitfall: langsung patch tanpa hipotesis yang dapat diuji.
- Pitfall: mengabaikan reproduksi deterministik.
- Best practice: gunakan workflow observe -> hypothesize -> validate -> fix -> verify.

## 9. Prerequisites

- [L1 - Runtime Model](../L1-runtime-model/index.md)
- [L2 - Core APIs](../L2-core-apis/index.md)
- [L3 - Performance and Security](../L3-performance-and-security/index.md)

## 10. Next Topics

- [Race Condition Diagnosis](./race-condition-diagnosis.md)
