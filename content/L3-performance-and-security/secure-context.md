# Secure Context

- Level: L3
- Status: Stable
- Depth: core
- Specs:
  - Secure Contexts specification
  - HTML/Feature policy integration context
- Prerequisites: CORS
- Next Topics: Cross-Origin Isolation

---

## 1. Official Term

Secure Context

## 2. Formal Definition

Secure Context adalah environment eksekusi yang dianggap cukup aman
(umumnya HTTPS atau localhost)
untuk mengakses capability sensitif tertentu pada Web Platform.

## 3. Mental Model

Sebagian API berisiko tinggi hanya aktif
jika halaman berjalan pada konteks yang aman.

### Wireframe Ringkas

```text
[Context Check]
  HTTPS/localhost? -> yes -> sensitive APIs available
                     no  -> restricted/blocked
```

## 4. Runtime Perspective

- Thread/process: pemeriksaan secure context dilakukan browser saat capability diminta.
- Queue model: tidak mengubah queue model, tetapi memengaruhi hasil akses API.
- Scheduling: gating berlaku sebelum API sensitif dieksekusi penuh.
- Rendering interaction: dampak tidak langsung; memengaruhi fitur yang tersedia ke UI logic.
- Dampak performa: overhead check kecil.
- Dampak memori: tidak signifikan langsung.
- Dampak keamanan: mengurangi risiko ekspos fitur sensitif di koneksi tidak aman.

## 5. Why This Exists

Mekanisme ini ada untuk memastikan fitur sensitif
hanya tersedia pada konteks dengan jaminan transport/security baseline.

## 6. Minimal Code Example

```js
if (window.isSecureContext) {
  console.log("secure context");
}
```

## 7. Common Misconceptions

- "HTTPS hanya soal SEO/performa"
  - Koreksi: HTTPS juga syarat akses banyak API sensitif.
- "Semua API browser tetap tersedia di HTTP"
  - Koreksi: beberapa capability dibatasi pada secure context.

## 8. Pitfalls and Best Practices

- Pitfall: mengembangkan fitur sensitif tanpa fallback saat konteks tidak aman.
- Pitfall: deployment campuran konten aman dan tidak aman.
- Best practice: jadikan HTTPS default di seluruh environment produksi.

## 9. Prerequisites

- [Same-Origin Policy](./same-origin-policy.md)
- [CORS](./cors.md)

## 10. Next Topics

- [Cross-Origin Isolation](./cross-origin-isolation.md)
