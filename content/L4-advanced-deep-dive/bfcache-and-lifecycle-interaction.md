# bfcache and Lifecycle Interaction

- Level: L4
- Status: Stable
- Depth: advanced
- Specs:
  - HTML Standard (session history and bfcache related behavior)
  - Page lifecycle behavior context
- Prerequisites: IndexedDB Transaction Model
- Next Topics: L5 - Watchlist and Experimental

---

## 1. Official Term

Back-Forward Cache (bfcache)

## 2. Formal Definition

bfcache adalah mekanisme browser untuk menyimpan snapshot halaman
saat navigasi history (back/forward),
agar halaman bisa dipulihkan cepat tanpa reload penuh.

Interaksi lifecycle mencakup event seperti `pagehide`, `pageshow`,
dan kondisi yang menentukan apakah halaman eligible masuk cache.

## 3. Mental Model

Saat user pindah halaman, browser bisa "membekukan" state halaman lama.
Saat kembali, halaman dipulihkan hampir instan jika lolos syarat bfcache.

### Wireframe Ringkas

```text
[Page A active]
  -> navigate to Page B
  -> Page A stored in bfcache? (eligible)
  -> back to Page A
  -> pageshow (restored, no full reload)
```

## 4. Runtime Perspective

- Thread/process: state halaman disimpan/dipulihkan oleh subsistem navigasi browser.
- Queue model: lifecycle events terkait navigasi diproses sebagai task pada event loop.
- Scheduling: eligibility bfcache dievaluasi saat transisi navigasi.
- Rendering interaction: restore dari bfcache menghindari biaya full reparse/reload.
- Dampak performa: meningkatkan kecepatan back/forward navigation secara signifikan.
- Dampak memori: menyimpan snapshot halaman menambah penggunaan memori sementara.
- Dampak keamanan: browser menerapkan aturan ketat agar restore tetap aman dan konsisten.

## 5. Why This Exists

bfcache ada untuk meningkatkan pengalaman navigasi history
dengan waktu kembali halaman yang lebih cepat dan hemat resource.

## 6. Minimal Code Example

```js
window.addEventListener("pageshow", (event) => {
  if (event.persisted) {
    console.log("restored from bfcache");
  }
});
```

## 7. Common Misconceptions

- "Back selalu reload halaman dari awal"
  - Koreksi: bisa restore dari bfcache jika eligible.
- "bfcache sama dengan HTTP cache"
  - Koreksi: bfcache menyimpan state halaman aktif, bukan hanya resource response.

## 8. Pitfalls and Best Practices

- Pitfall: menggunakan pola yang membuat halaman tidak eligible bfcache.
- Pitfall: tidak menangani re-initialization ringan saat `pageshow` persisted.
- Best practice: desain lifecycle handler yang kompatibel dengan restore flow.

## 9. Prerequisites

- [Document Lifecycle](../L1-runtime-model/document-lifecycle.md)
- [Service Worker Lifecycle](./service-worker-lifecycle.md)

## 10. Next Topics

- L5 - Watchlist and Experimental
