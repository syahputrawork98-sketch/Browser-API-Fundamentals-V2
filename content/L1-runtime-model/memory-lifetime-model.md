# Memory Lifetime Model

- Level: L1
- Status: Stable
- Depth: core
- Specs:
  - ECMAScript Specification (reachability and GC model as host-integrated behavior)
  - HTML/DOM host object lifecycle behavior
- Prerequisites: Document Lifecycle
- Next Topics: Concurrency Model

---

## 1. Official Term

Memory Lifetime Model

## 2. Formal Definition

Memory lifetime model menjelaskan kapan objek tetap reachable,
kapan dapat dikoleksi garbage collector, dan bagaimana referensi lintas closure,
DOM, serta host objects memengaruhi retensi memori.

## 3. Mental Model

Objek tidak hilang saat "tidak dipakai secara logis", tetapi saat tidak lagi reachable.

### Wireframe Ringkas

```text
[Root References]
   -> [JS Objects]
   -> [Closures]
   -> [DOM Nodes]
If reachable from roots => retained
If unreachable          => eligible for GC
```

## 4. Runtime Perspective

- Thread/process: alokasi objek terjadi pada runtime engine di renderer context.
- Queue model: GC tidak dijadwalkan langsung oleh kode aplikasi per baris.
- Scheduling: engine menentukan kapan GC cycle berjalan berdasarkan heuristik.
- Rendering interaction: tekanan memori tinggi bisa memengaruhi responsivitas runtime.
- Dampak performa: retention berlebih meningkatkan GC pressure dan latency spike.
- Dampak memori: detached DOM, closure yang menahan data besar, dan cache tanpa batas sering jadi sumber kebocoran logis.
- Dampak keamanan: retensi data sensitif terlalu lama meningkatkan risiko paparan data di memori proses.

## 5. Why This Exists

Model ini diperlukan agar developer memahami bahwa manajemen memori web
adalah kombinasi antara reachability graph dan lifecycle host objects,
bukan hanya variabel lokal selesai scope.

## 6. Minimal Code Example

```js
let cache = [];
function storeLargeObject(obj) {
  cache.push(obj); // objek tetap reachable selama cache menahannya
}
```

## 7. Common Misconceptions

- "GC langsung membersihkan semua setelah function selesai"
  - Koreksi: objek dibersihkan jika tidak lagi reachable, waktunya tidak deterministik.
- "Remove element dari DOM pasti bebas memori"
  - Koreksi: jika masih direferensikan JS, node tetap retained.

## 8. Pitfalls and Best Practices

- Pitfall: global cache tanpa eviction policy.
- Pitfall: event listener tertinggal pada node yang sudah dilepas.
- Best practice: batasi retensi data, putus referensi saat tidak dibutuhkan.

## 9. Prerequisites

- Event Loop
- Document Lifecycle

## 10. Next Topics

- [Concurrency Model](./concurrency-model.md)
