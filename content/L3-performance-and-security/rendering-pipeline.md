# Rendering Pipeline

- Level: L3
- Status: Stable
- Depth: core
- Specs:
  - HTML Standard (rendering opportunity context)
  - CSS rendering model context
- Prerequisites: L2 - Core APIs
- Next Topics: Long Tasks

---

## 1. Official Term

Rendering Pipeline

## 2. Formal Definition

Rendering pipeline adalah rangkaian tahapan internal browser
untuk mengubah DOM/CSSOM menjadi frame visual,
umumnya meliputi style calculation, layout, paint, dan compositing.

## 3. Mental Model

Perubahan UI tidak langsung digambar per baris JavaScript.
Browser mengakumulasi perubahan lalu memproses pipeline frame.

### Wireframe Ringkas

```text
DOM/CSS changes
   -> Style Calculation
   -> Layout
   -> Paint
   -> Composite
   -> Frame on screen
```

## 4. Runtime Perspective

- Thread/process: style/layout sering terjadi di renderer main thread; compositing melibatkan subsistem GPU.
- Queue model: pipeline berjalan setelah task/microtask yang relevan selesai, saat render opportunity.
- Scheduling: browser menyeimbangkan frame budget dengan beban script/layout/paint.
- Rendering interaction: DOM read/write pattern dapat memicu forced synchronous layout.
- Dampak performa: layout thrashing menyebabkan jank dan frame drop.
- Dampak memori: layer berlebih dan paint cache meningkatkan penggunaan memori grafis.
- Dampak keamanan: tidak mengubah policy origin, tetapi memengaruhi quality of service UI.

## 5. Why This Exists

Pipeline ini diperlukan untuk memisahkan tahap perhitungan style/geometri
hingga output visual agar rendering tetap terstruktur dan efisien.

## 6. Minimal Code Example

```js
const box = document.getElementById("box");
box.style.width = "300px";
box.style.transform = "translateX(20px)";
```

Perubahan ini akan diproses pada tahap pipeline render berikutnya.

## 7. Common Misconceptions

- "Render terjadi di setiap statement JS"
  - Koreksi: render terjadi pada kesempatan tertentu setelah scheduling host.
- "Semua properti CSS biayanya sama"
  - Koreksi: properti tertentu memicu layout/paint lebih mahal dibanding transform/composite-only.

## 8. Pitfalls and Best Practices

- Pitfall: read layout metric setelah write style berulang.
- Pitfall: mutasi DOM besar tanpa batching.
- Best practice: batch perubahan dan pilih properti yang ramah compositing jika memungkinkan.

## 9. Prerequisites

- [Rendering Opportunity](../L1-runtime-model/rendering-opportunity.md)
- [DOM Standard Fundamentals](../L2-core-apis/dom-standard-fundamentals.md)

## 10. Next Topics

- [Long Tasks](./long-tasks.md)
- [PerformanceObserver](./performanceobserver.md)
