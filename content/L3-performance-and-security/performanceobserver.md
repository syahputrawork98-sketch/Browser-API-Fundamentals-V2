# PerformanceObserver

- Level: L3
- Status: Stable
- Depth: core
- Specs:
  - Performance Timeline
  - PerformanceObserver API
- Prerequisites: Long Tasks
- Next Topics: L4 - Advanced Deep Dive

---

## 1. Official Term

PerformanceObserver

## 2. Formal Definition

PerformanceObserver adalah API untuk berlangganan entry pada Performance Timeline
secara asinkron, seperti `longtask`, `mark`, `measure`, dan entry type lain yang didukung.

## 3. Mental Model

Alih-alih polling performa manual,
aplikasi mendaftar observer dan menerima entry ketika browser merekam metrik.

### Wireframe Ringkas

```text
[Runtime events]
    -> [Performance Timeline]
    -> [PerformanceObserver callback]
    -> [App diagnostics/logging]
```

## 4. Runtime Perspective

- Thread/process: observer callback dijalankan pada context dokumen tempat observer dibuat.
- Queue model: delivery entry terjadi asinkron melalui scheduling host.
- Scheduling: browser mengirim batch entry ke callback observer.
- Rendering interaction: observer ringan aman; callback berat bisa menjadi beban baru di main thread.
- Dampak performa: memberi visibilitas bottleneck nyata tanpa instrumentasi invasif.
- Dampak memori: buffer entry perlu dikonsumsi/disaring agar tidak membesar.
- Dampak keamanan: beberapa metrik dibatasi oleh policy/precision untuk mitigasi abuse timing.

## 5. Why This Exists

API ini ada agar developer dapat memonitor performa runtime
secara terstruktur dan berbasis data dari timeline browser.

## 6. Minimal Code Example

```js
const observer = new PerformanceObserver((list) => {
  for (const entry of list.getEntries()) {
    console.log(entry.entryType, entry.duration);
  }
});

observer.observe({ type: "longtask", buffered: true });
```

## 7. Common Misconceptions

- "PerformanceObserver hanya untuk lab tooling"
  - Koreksi: bisa dipakai juga untuk runtime diagnostics aplikasi.
- "Semua entry type selalu tersedia"
  - Koreksi: ketersediaan tergantung dukungan browser dan konteks.

## 8. Pitfalls and Best Practices

- Pitfall: callback observer melakukan kerja berat atau logging berlebihan.
- Pitfall: tidak memfilter entry type sesuai tujuan.
- Best practice: observasi metrik yang relevan dan minimalkan overhead callback.

## 9. Prerequisites

- [Long Tasks](./long-tasks.md)
- [L1 - Runtime Model](../L1-runtime-model/index.md)

## 10. Next Topics

- L4 - Advanced Deep Dive
