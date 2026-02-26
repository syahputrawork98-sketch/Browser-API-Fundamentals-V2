# File System Access API

- Level: L5
- Status: Experimental
- Depth: watchlist
- Specs:
  - File System Access API context
- Prerequisites: Speculation Rules API
- Next Topics: WebGPU

---

## 1. Official Term

File System Access API

## 2. Formal Definition

File System Access API menyediakan akses baca/tulis file lokal
melalui permission model berbasis user gesture,
dengan handle file/directory yang dikelola browser.

## 3. Mental Model

Aplikasi web bisa bekerja lebih seperti aplikasi desktop,
namun akses file tetap dikunci oleh izin eksplisit pengguna.

### Wireframe Ringkas

```text
[User gesture]
   -> open/save picker
   -> permission grant
   -> file handle read/write
```

## 4. Runtime Perspective

- Thread/process: API dipanggil dari context dokumen (umumnya secure context).
- Queue model: operasi IO file bersifat async dan diselesaikan via promise.
- Scheduling: permission prompt dan operasi IO dikoordinasi host browser/OS bridge.
- Rendering interaction: operasi file besar yang diproses di main thread dapat mengganggu UI.
- Dampak performa: akses file besar perlu streaming/chunking untuk menjaga responsivitas.
- Dampak memori: membaca file penuh ke memori dapat menyebabkan spike.
- Dampak keamanan: izin granular + user gesture requirement menjadi boundary utama.

## 5. Why This Exists

Agar web app produktivitas dapat mengelola dokumen lokal
dengan pengalaman yang lebih natural namun tetap aman.

## 6. Minimal Code Example

```js
if (window.showOpenFilePicker) {
  const [handle] = await window.showOpenFilePicker();
  const file = await handle.getFile();
  console.log(file.name);
}
```

## 7. Common Misconceptions

- "Web app bisa akses semua file user tanpa batas"
  - Koreksi: akses dibatasi izin eksplisit, scope handle, dan policy browser.
- "Permission sekali berarti permanen di semua konteks"
  - Koreksi: perilaku izin tergantung browser/session/policy.

## 8. Pitfalls and Best Practices

- Pitfall: menyimpan asumsi permission selalu tersedia.
- Pitfall: memproses file besar sinkron di main thread.
- Best practice: gunakan async flow, validasi error/permission denial, dan fallback UX.

## 9. Prerequisites

- [Secure Context](../L3-performance-and-security/secure-context.md)
- [Storage](../L2-core-apis/storage.md)

## 10. Next Topics

- [WebGPU](./webgpu.md)
