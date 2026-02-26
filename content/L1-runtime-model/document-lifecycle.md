# Document Lifecycle

- Level: L1
- Status: Stable
- Depth: core
- Specs:
  - HTML Standard (document readiness and lifecycle events)
  - Page Lifecycle guidance (implementation behavior)
- Prerequisites: Rendering Opportunity
- Next Topics: Memory Lifetime Model

---

## 1. Official Term

Document Lifecycle

## 2. Formal Definition

Document lifecycle adalah rangkaian fase keadaan dokumen dari loading,
interactive, complete, hingga transisi visibility atau termination.

Fase ini memengaruhi kapan script dijalankan dan kapan event lifecycle dipicu.

## 3. Mental Model

Dokumen web bergerak melalui status kesiapan dan event transisi,
bukan sekadar "halaman terbuka lalu selesai".

### Wireframe Ringkas

```text
[Navigation Start]
      -> [loading]
      -> [DOMContentLoaded]
      -> [complete/load]
      -> [visibilitychange]
      -> [pagehide/unload (kondisional)]
```

## 4. Runtime Perspective

- Thread/process: event lifecycle utama diproses pada renderer main thread.
- Queue model: dispatch event lifecycle terjadi sebagai task dari lifecycle-related sources.
- Scheduling: timing event dipengaruhi parser, network completion, dan state dokumen.
- Rendering interaction: readiness state memengaruhi kapan UI dianggap siap interaktif.
- Dampak performa: handler lifecycle yang berat dapat menambah load delay.
- Dampak memori: listener global yang tidak dibersihkan dapat menahan referensi.
- Dampak keamanan: lifecycle event dapat berinteraksi dengan policy bfcache dan navigation isolation.

## 5. Why This Exists

Lifecycle memberi kontrak waktu bagi aplikasi untuk inisialisasi,
menangani suspend/resume, dan mengelola resource saat halaman berubah status.

## 6. Minimal Code Example

```js
document.addEventListener("DOMContentLoaded", () => {
  console.log("DOM siap dipakai");
});

window.addEventListener("load", () => {
  console.log("resource utama selesai dimuat");
});
```

## 7. Common Misconceptions

- "DOMContentLoaded sama dengan load"
  - Koreksi: `DOMContentLoaded` fokus pada parsing DOM, `load` menunggu resource terkait selesai.
- "Halaman hidden berarti script berhenti total"
  - Koreksi: ada throttling/penyesuaian, bukan selalu berhenti total.

## 8. Pitfalls and Best Practices

- Pitfall: inisialisasi berat di event awal tanpa batching.
- Pitfall: mengandalkan `unload` untuk cleanup kritikal.
- Best practice: gunakan event lifecycle sesuai tujuan (`DOMContentLoaded`, `visibilitychange`, `pagehide`).

## 9. Prerequisites

- Event Loop
- Rendering Opportunity

## 10. Next Topics

- [Memory Lifetime Model](./memory-lifetime-model.md)
- [Concurrency Model](./concurrency-model.md)
