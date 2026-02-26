# Browser Process Model Deep Dive

- Level: L4
- Status: Stable
- Depth: advanced
- Specs:
  - HTML processing model context
  - Browser architecture implementation model
- Prerequisites: Service Worker Lifecycle
- Next Topics: IndexedDB Transaction Model

---

## 1. Official Term

Browser Process Model

## 2. Formal Definition

Browser process model menjelaskan pembagian tanggung jawab
antara browser process, renderer process, GPU process,
dan service/network process pada browser modern.

## 3. Mental Model

Aplikasi web tidak berjalan di satu proses tunggal.
Browser memecah komponen agar keamanan dan stabilitas meningkat.

### Wireframe Ringkas

```text
[Browser Process]
   +--> [Renderer Process A - Tab A]
   +--> [Renderer Process B - Tab B]
   +--> [GPU Process]
   +--> [Network/Service Process]
```

## 4. Runtime Perspective

- Thread/process: JavaScript halaman berjalan di renderer process masing-masing site/tab.
- Queue model: tiap renderer punya event loop sendiri; koordinasi lintas proses via IPC.
- Scheduling: OS scheduler + browser scheduler mengatur prioritas proses/thread.
- Rendering interaction: renderer menghasilkan frame/layer, GPU process melakukan compositing akhir.
- Dampak performa: isolasi proses menambah overhead IPC tetapi meningkatkan stabilitas keseluruhan.
- Dampak memori: multi-process menambah baseline memory per proses.
- Dampak keamanan: site isolation memperkecil dampak kompromi satu renderer terhadap origin lain.

## 5. Why This Exists

Model ini ada untuk mengisolasi kegagalan,
memperkuat boundary keamanan,
dan menjaga browser tetap responsif pada banyak tab.

## 6. Minimal Code Example

Tidak ada contoh kode langsung,
karena ini adalah model arsitektur internal browser.

## 7. Common Misconceptions

- "Semua tab pasti satu proses"
  - Koreksi: browser modern umumnya multi-process dengan kebijakan isolasi tertentu.
- "Lebih banyak proses selalu lebih buruk"
  - Koreksi: ada tradeoff memori vs isolasi/stabilitas/keamanan.

## 8. Pitfalls and Best Practices

- Pitfall: mendiagnosis bottleneck tanpa mempertimbangkan biaya IPC/proses lain.
- Pitfall: menyimpulkan perilaku runtime hanya dari perspektif satu thread JS.
- Best practice: analisis performa dengan konteks end-to-end (renderer, network, GPU).

## 9. Prerequisites

- [Browser Architecture Overview](../L0-platform-map/browser-architecture-overview.md)
- [Concurrency Model](../L1-runtime-model/concurrency-model.md)

## 10. Next Topics

- IndexedDB Transaction Model
- bfcache and Lifecycle Interaction
