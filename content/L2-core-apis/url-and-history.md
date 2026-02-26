# URL and History

- Level: L2
- Status: Stable
- Depth: core
- Specs:
  - URL Standard
  - HTML Standard (History API)
- Prerequisites: Fetch API Fundamentals
- Next Topics: Storage

---

## 1. Official Term

URL API and History API

## 2. Formal Definition

URL API menyediakan parsing dan manipulasi URL secara standar.
History API menyediakan kontrol state riwayat navigasi dokumen
melalui `pushState`, `replaceState`, dan event `popstate`.

## 3. Mental Model

URL API mengelola bentuk alamat.
History API mengelola tumpukan state navigasi pada tab.

### Wireframe Ringkas

```text
[History Stack]
  entry-1 -> entry-2 -> entry-3(current)
                 ^ popstate when user goes back/forward
```

## 4. Runtime Perspective

- Thread/process: manipulasi URL/history umumnya dipanggil dari main thread dokumen.
- Queue model: navigasi/back-forward memicu task event seperti `popstate`.
- Scheduling: update history state sinkron saat dipanggil; event terkait diproses via event loop.
- Rendering interaction: perubahan state dapat memicu rerender aplikasi SPA.
- Dampak performa: serialisasi state besar di history meningkatkan overhead.
- Dampak memori: state object besar di history menahan memori lebih lama.
- Dampak keamanan: origin boundary tetap berlaku; tidak bisa memanipulasi history tab origin lain.

## 5. Why This Exists

API ini memberi kontrol navigasi modern untuk aplikasi web,
terutama pola single-page navigation tanpa full reload.

## 6. Minimal Code Example

```js
const url = new URL(location.href);
url.searchParams.set("tab", "overview");
history.pushState({ tab: "overview" }, "", url);
```

## 7. Common Misconceptions

- "pushState memicu request network otomatis"
  - Koreksi: `pushState` hanya mengubah state URL/history pada dokumen saat ini.
- "History API bisa ubah domain bebas"
  - Koreksi: tetap terikat aturan origin/URL validity.

## 8. Pitfalls and Best Practices

- Pitfall: menyimpan state besar langsung ke history.
- Pitfall: lupa menangani `popstate` untuk sinkronisasi UI.
- Best practice: simpan state ringkas dan deterministik.

## 9. Prerequisites

- [Fetch API Fundamentals](./fetch-api-fundamentals.md)
- [Document Lifecycle](../L1-runtime-model/document-lifecycle.md)

## 10. Next Topics

- [Storage](./storage.md)
