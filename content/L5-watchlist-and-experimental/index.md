# L5 - Watchlist and Experimental

Level ini berisi API baru atau eksperimental yang perlu dipantau
sebelum diadopsi luas pada sistem produksi.

---

## Status

Batch 1 dan batch 2 tersedia.
Konten ini bersifat evolving dan perlu evaluasi berkala.

---

## Topik Batch 1

- [Navigation API](./navigation-api.md)
- [Scheduler API](./scheduler-api.md)
- [View Transitions API](./view-transitions-api.md)

## Topik Batch 2

- [Speculation Rules API](./speculation-rules-api.md)
- [File System Access API](./file-system-access-api.md)
- [WebGPU](./webgpu.md)

---

## Adoption Matrix

| API | Status | Browser Support | Risk | When to Use |
|---|---|---|---|---|
| Navigation API | Experimental | Partial/bervariasi | Medium-High | SPA modern yang butuh interception navigasi terstruktur |
| Scheduler API | Emerging | Partial/bervariasi | Medium | Menjadwalkan prioritas task agar UI lebih responsif |
| View Transitions API | Emerging | Partial/bervariasi | Medium | Transisi antar state UI/page dengan kontrol animasi native |
| Speculation Rules API | Experimental | Partial/bervariasi | Medium-High | Optimasi navigasi prediktif dengan prefetch/prerender terarah |
| File System Access API | Experimental | Partial/bervariasi | High | Aplikasi web produktivitas yang butuh interaksi file lokal |
| WebGPU | Emerging | Partial/bervariasi | High | Rendering/compute workload intensif dengan kebutuhan performa tinggi |

---

## Jalur Baca Disarankan

1. Navigation API
2. Scheduler API
3. View Transitions API
4. Speculation Rules API
5. File System Access API
6. WebGPU

---

## Prerequisites

- [L4 - Advanced Deep Dive](../L4-advanced-deep-dive/index.md)

---

## Next Level

L6 - Applied Systems
