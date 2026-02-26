# CORS

- Level: L3
- Status: Stable
- Depth: core
- Specs:
  - Fetch Standard (CORS protocol)
- Prerequisites: Same-Origin Policy
- Next Topics: Secure Context

---

## 1. Official Term

Cross-Origin Resource Sharing (CORS)

## 2. Formal Definition

CORS adalah mekanisme berbasis header HTTP
yang mengizinkan atau menolak akses script lintas origin
terhadap response resource tertentu.

## 3. Mental Model

Server menyatakan siapa yang boleh membaca response lintas origin.
Browser menegakkan keputusan itu sebelum mengekspos data ke script.

### Wireframe Ringkas

```text
Browser (Origin A) -> Request -> Server (Origin B)
Server response headers (Access-Control-*)
Browser validates policy -> expose or block response to JS
```

## 4. Runtime Perspective

- Thread/process: validation CORS terjadi pada subsistem network/security browser.
- Queue model: hasil fetch tetap masuk microtask saat resolved/rejected.
- Scheduling: pada request tertentu browser menjalankan preflight OPTIONS terlebih dahulu.
- Rendering interaction: error CORS dapat memutus alur data yang dibutuhkan UI.
- Dampak performa: preflight menambah round-trip latency.
- Dampak memori: tidak signifikan langsung, kecuali retry/logging berlebihan.
- Dampak keamanan: CORS mengontrol ekspos data lintas origin, bukan mekanisme autentikasi utama.

## 5. Why This Exists

CORS memungkinkan kolaborasi aman antar origin
tanpa menghilangkan boundary dasar SOP.

## 6. Minimal Code Example

```js
fetch("https://api.example.com/data", {
  method: "GET",
  credentials: "include"
});
```

Akses data di script akan berhasil jika policy CORS server sesuai.

## 7. Common Misconceptions

- "CORS adalah perlindungan server dari semua serangan"
  - Koreksi: CORS fokus pada kontrol akses response oleh browser script.
- "Jika request terkirim berarti CORS lolos"
  - Koreksi: request bisa terkirim tetapi response tetap diblok browser.

## 8. Pitfalls and Best Practices

- Pitfall: menggunakan `Access-Control-Allow-Origin: *` bersama kredensial.
- Pitfall: salah konfigurasi origin whitelist.
- Best practice: tetapkan origin yang diizinkan secara eksplisit dan minimal.

## 9. Prerequisites

- [Same-Origin Policy](./same-origin-policy.md)
- [Fetch API Fundamentals](../L2-core-apis/fetch-api-fundamentals.md)

## 10. Next Topics

- [Secure Context](./secure-context.md)
- [Cross-Origin Isolation](./cross-origin-isolation.md)
