# Rendering Opportunity

- Level: L1
- Status: Stable
- Depth: core
- Specs:
  - HTML Standard (update the rendering)
  - CSSOM View / rendering pipeline behavior (implementation-dependent)
- Prerequisites: Tasks vs Microtasks
- Next Topics: L2 - Core APIs

---

## 1. Official Term

Rendering Opportunity

## 2. Formal Definition

Rendering opportunity adalah momen ketika user agent dapat melakukan update rendering
setelah task selesai dan microtask checkpoint tidak lagi pending.

## 3. Mental Model

Browser hanya bisa merender di batas tertentu,
bukan di setiap baris JavaScript yang dieksekusi.

### Wireframe Ringkas

```text
[Run Task] -> [Flush Microtasks] -> [Can Render? yes] -> [Style/Layout/Paint] -> [Next Task]
```

## 4. Runtime Perspective

- Thread/process: di banyak kasus style/layout berjalan di renderer main thread.
- Queue model: render menunggu task dan microtask yang relevan selesai.
- Scheduling: browser menentukan kapan frame diproduksi berdasarkan budget dan state.
- Rendering interaction: DOM write/read pattern dapat memicu biaya layout tambahan.
- Dampak performa: long task atau microtask storm menyebabkan frame drop/jank.
- Dampak memori: DOM mutation berlebihan meningkatkan tekanan memori sementara.
- Dampak keamanan: tidak mengubah policy security, tetapi memengaruhi UX/perceived responsiveness.

## 5. Why This Exists

Agar browser bisa menyeimbangkan konsistensi state script dengan kebutuhan UI update
secara efisien tanpa merender di setiap operasi kecil.

## 6. Minimal Code Example

```js
const box = document.getElementById("box");
box.style.width = "200px";
box.style.height = "200px";
// perubahan ini umumnya akan terlihat pada render opportunity berikutnya
```

## 7. Common Misconceptions

- "DOM berubah berarti langsung repaint saat itu juga"
  - Koreksi: update visual biasanya menunggu render opportunity.
- "requestAnimationFrame sama dengan render"
  - Koreksi: `requestAnimationFrame` memberi callback sebelum fase render berikutnya.

## 8. Pitfalls and Best Practices

- Pitfall: layout thrashing karena read/write DOM bolak-balik.
- Pitfall: manipulasi DOM besar dalam satu tick tanpa batching.
- Best practice: batch DOM updates dan gunakan pola scheduling yang kooperatif.

## 9. Prerequisites

- Event Loop
- Tasks vs Microtasks

## 10. Next Topics

- [L2 - Core APIs](../L2-core-apis/index.md)
