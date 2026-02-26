# Normative Algorithm Tracing

- Level: L8
- Status: Stable
- Depth: professional
- Specs:
  - HTML/DOM/Fetch algorithms (contextual)
- Prerequisites: Spec Reading Workflow
- Next Topics: Interop and Conformance Validation

---

## 1. Official Term

Normative Algorithm Tracing

## 2. Formal Definition

Normative algorithm tracing adalah proses menelusuri langkah-langkah algoritma
berkata kunci normatif (misalnya "must", "queue a task", "fire an event")
untuk memahami perilaku implementasi yang diwajibkan specification.

## 3. Mental Model

Setiap langkah algoritma adalah kontrak perilaku.
Tracing berarti mengikuti alur cabang algoritma hingga outcome final.

### Wireframe Ringkas

```text
[Algorithm step 1]
   -> condition A? yes -> branch A steps
   -> condition A? no  -> branch B steps
   -> side effects (queue task / fire event / update state)
```

## 4. Runtime Perspective

- Thread/process: langkah seperti "queue a task" harus dipetakan ke event loop context.
- Queue model: bedakan tindakan sinkron vs enqueue behavior.
- Scheduling: cabang algoritma menentukan kapan callback/event dijalankan.
- Rendering interaction: cek langkah yang memengaruhi style/layout/update rendering.
- Dampak performa: branch tertentu bisa memicu kerja ekstra (mis. preflight, reflow trigger path).
- Dampak memori: tracing menunjukkan kapan objek disimpan/dilepas dalam lifecycle spec.
- Dampak keamanan: cabang policy enforcement sering menentukan blocked vs allowed path.

## 5. Why This Exists

Untuk menghindari interpretasi keliru,
terutama pada kasus edge dan condition branch kompleks.

## 6. Minimal Code Example

```text
Contoh tracing ringkas:
- Locate: "queue a task to fire an event"
- Identify: task source + trigger condition
- Infer: callback tidak sinkron, akan dieksekusi pada giliran loop berikutnya
```

## 7. Common Misconceptions

- "Semua kata di spec punya bobot sama"
  - Koreksi: langkah normatif dan catatan non-normatif berbeda bobot.
- "Kalau satu browser berbeda, spec pasti salah"
  - Koreksi: bisa jadi bug implementasi atau interpretasi tracing yang keliru.

## 8. Pitfalls and Best Practices

- Pitfall: melewati cross-reference ke definisi istilah lain.
- Pitfall: tidak mencatat branch condition saat menyimpulkan behavior.
- Best practice: tulis trace log langkah per langkah saat analisis.

## 9. Prerequisites

- [Spec Reading Workflow](./spec-reading-workflow.md)
- [Tasks vs Microtasks](../L1-runtime-model/tasks-vs-microtasks.md)

## 10. Next Topics

- [Interop and Conformance Validation](./interop-and-conformance-validation.md)
