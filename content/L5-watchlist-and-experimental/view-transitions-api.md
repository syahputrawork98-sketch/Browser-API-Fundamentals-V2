# View Transitions API

- Level: L5
- Status: Emerging
- Depth: watchlist
- Specs:
  - View Transitions API context
- Prerequisites: Scheduler API
- Next Topics: L6 - Applied Systems

---

## 1. Official Term

View Transitions API

## 2. Formal Definition

View Transitions API menyediakan mekanisme transisi visual terintegrasi platform
untuk perpindahan state UI atau navigasi,
dengan model snapshot before/after dan animasi transisi.

## 3. Mental Model

Browser menangkap view sebelum dan sesudah perubahan,
lalu menginterpolasi transisi antar keduanya.

### Wireframe Ringkas

```text
[Before State Snapshot]
      -> apply DOM/state update
[After State Snapshot]
      -> transition animation
      -> final state displayed
```

## 4. Runtime Perspective

- Thread/process: koordinasi transisi terjadi pada jalur rendering dokumen.
- Queue model: update state dan transisi terkait mengikuti scheduling event loop/render loop.
- Scheduling: browser mengeksekusi transisi pada momen yang sinkron dengan pipeline rendering.
- Rendering interaction: API ini langsung terkait frame rendering dan compositing.
- Dampak performa: transisi kompleks dapat meningkatkan biaya paint/composite.
- Dampak memori: snapshot visual menambah penggunaan memori sementara.
- Dampak keamanan: tidak mengubah boundary origin; fokus pada presentasi visual.

## 5. Why This Exists

Untuk menghadirkan transisi UI yang lebih halus dan konsisten
dengan integrasi native ke pipeline rendering browser.

## 6. Minimal Code Example

```js
if (document.startViewTransition) {
  document.startViewTransition(() => {
    document.body.classList.toggle("alt-state");
  });
}
```

## 7. Common Misconceptions

- "View transitions otomatis gratis tanpa biaya render"
  - Koreksi: tetap ada biaya tergantung kompleksitas UI.
- "API ini wajib untuk semua animasi"
  - Koreksi: gunakan saat transisi state/navigation memang butuh continuity visual.

## 8. Pitfalls and Best Practices

- Pitfall: transisi besar tanpa batas pada halaman kompleks.
- Pitfall: tidak menyediakan fallback saat API tidak tersedia.
- Best practice: mulai dari transisi sederhana dan ukur dampak performanya.

## 9. Prerequisites

- [Rendering Pipeline](../L3-performance-and-security/rendering-pipeline.md)
- [PerformanceObserver](../L3-performance-and-security/performanceobserver.md)

## 10. Next Topics

- L6 - Applied Systems
