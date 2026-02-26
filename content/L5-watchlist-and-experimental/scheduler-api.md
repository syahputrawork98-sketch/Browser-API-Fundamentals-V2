# Scheduler API

- Level: L5
- Status: Emerging
- Depth: watchlist
- Specs:
  - Prioritized Task Scheduling API context
- Prerequisites: Navigation API
- Next Topics: View Transitions API

---

## 1. Official Term

Scheduler API

## 2. Formal Definition

Scheduler API menyediakan primitive penjadwalan task dengan prioritas
agar aplikasi dapat bekerja lebih kooperatif terhadap event loop,
terutama untuk menjaga responsivitas UI.

## 3. Mental Model

Tidak semua task pentingnya sama.
Scheduler API membantu memprioritaskan task kritikal UI
lebih dulu dibanding kerja latar yang dapat ditunda.

### Wireframe Ringkas

```text
[Tasks]
  -> high priority (UI-critical)
  -> user-visible
  -> background
Scheduler selects by priority + host conditions
```

## 4. Runtime Perspective

- Thread/process: API dipanggil di context dokumen/worker yang mendukung.
- Queue model: task berprioritas dijadwalkan ke loop host dengan hint prioritas.
- Scheduling: host tetap otoritas akhir; prioritas adalah sinyal, bukan jaminan absolut.
- Rendering interaction: penjadwalan lebih baik dapat mengurangi blocking jalur render.
- Dampak performa: membantu mengurangi jank jika dipakai benar.
- Dampak memori: tidak besar langsung, tetapi bisa menurunkan antrean task menumpuk.
- Dampak keamanan: tidak mengubah boundary keamanan; fokusnya kontrol scheduling.

## 5. Why This Exists

Untuk memberi developer alat kooperatif
dalam mengatur beban kerja main thread dengan lebih granular.

## 6. Minimal Code Example

```js
if ("scheduler" in window && scheduler.postTask) {
  scheduler.postTask(() => {
    console.log("background task");
  }, { priority: "background" });
}
```

## 7. Common Misconceptions

- "Prioritas tinggi pasti langsung dijalankan"
  - Koreksi: host scheduler tetap mempertimbangkan kondisi runtime.
- "Scheduler API menggantikan semua pola async lama"
  - Koreksi: ini pelengkap, bukan pengganti total.

## 8. Pitfalls and Best Practices

- Pitfall: semua task diberi prioritas tinggi.
- Pitfall: tidak memisahkan kerja UI-critical vs background.
- Best practice: definisikan kebijakan prioritas yang konsisten di aplikasi.

## 9. Prerequisites

- [Tasks vs Microtasks](../L1-runtime-model/tasks-vs-microtasks.md)
- [Long Tasks](../L3-performance-and-security/long-tasks.md)

## 10. Next Topics

- [View Transitions API](./view-transitions-api.md)
