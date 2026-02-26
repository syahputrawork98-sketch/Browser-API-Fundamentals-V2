# Tasks vs Microtasks

- Level: L1
- Status: Stable
- Depth: core
- Specs:
  - HTML Standard (tasks and microtask checkpoint)
  - ECMAScript Specification (Promise jobs)
- Prerequisites: Event Loop
- Next Topics: Rendering Opportunity

---

## 1. Official Term

Tasks and Microtasks

## 2. Formal Definition

Task adalah unit kerja yang dijadwalkan host event loop dari task source tertentu.
Microtask diproses pada microtask checkpoint, biasanya setelah task selesai
sebelum browser melanjutkan ke render opportunity atau task berikutnya.

## 3. Mental Model

Task adalah langkah besar per giliran.
Microtask adalah langkah kecil prioritas tinggi yang harus dikosongkan
sebelum loop bergerak ke fase berikutnya.

### Wireframe Ringkas

```text
Task #1 done
   -> flush microtasks (all)
   -> render opportunity
   -> Task #2
```

## 4. Runtime Perspective

- Thread/process: eksekusi callback tetap mengikuti context event loop dokumen.
- Queue model: task queue dan microtask queue diproses dengan prioritas berbeda.
- Scheduling: task dipilih host; microtask diflush sampai habis di checkpoint.
- Rendering interaction: microtask berantai dapat menunda rendering.
- Dampak performa: starvation bisa terjadi jika microtask terus menambah microtask.
- Dampak memori: closure pada microtask chain bisa memperpanjang referensi data.
- Dampak keamanan: tidak mengubah security boundary, tetapi memengaruhi timing observables.

## 5. Why This Exists

Pemisahan ini memungkinkan browser menjaga urutan operasi async dengan deterministik,
terutama untuk Promise reactions, tanpa menunggu task berikutnya.

## 6. Minimal Code Example

```js
setTimeout(() => console.log("task"), 0);
Promise.resolve()
  .then(() => console.log("microtask-1"))
  .then(() => console.log("microtask-2"));
console.log("sync");
```

Urutan umum: `sync`, `microtask-1`, `microtask-2`, `task`.

## 7. Common Misconceptions

- "Promise callback itu task"
  - Koreksi: Promise reaction diproses sebagai microtask.
- "Satu microtask saja per loop"
  - Koreksi: checkpoint memproses microtask sampai queue kosong.

## 8. Pitfalls and Best Practices

- Pitfall: recursive `queueMicrotask` tanpa batas.
- Pitfall: asumsi urutan callback lintas API tanpa memahami queue source.
- Best practice: gunakan microtask untuk sinkronisasi ringan, bukan kerja berat.

## 9. Prerequisites

- Event Loop

## 10. Next Topics

- [Rendering Opportunity](./rendering-opportunity.md)
