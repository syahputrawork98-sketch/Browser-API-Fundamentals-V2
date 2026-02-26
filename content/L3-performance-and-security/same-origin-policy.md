# Same-Origin Policy

- Level: L3
- Status: Stable
- Depth: core
- Specs:
  - HTML Standard (origin model)
  - Fetch Standard (origin checks context)
- Prerequisites: L2 - Core APIs
- Next Topics: CORS

---

## 1. Official Term

Same-Origin Policy (SOP)

## 2. Formal Definition

Same-Origin Policy adalah model keamanan web
yang membatasi interaksi script antar resource berbeda origin
(protocol, host, port) kecuali diizinkan oleh mekanisme eksplisit.

## 3. Mental Model

Origin berbeda diperlakukan sebagai boundary keamanan.
Script satu origin tidak bebas membaca data origin lain.

### Wireframe Ringkas

```text
Origin A script
   -> Read Origin A data: allowed
   -> Read Origin B data: blocked (unless explicit policy)
```

## 4. Runtime Perspective

- Thread/process: check origin terjadi pada subsistem browser saat operasi lintas origin diminta.
- Queue model: permintaan tetap mengikuti task/microtask flow API asalnya.
- Scheduling: evaluasi policy dilakukan sebelum data sensitif diekspos ke script.
- Rendering interaction: tidak langsung memengaruhi render pipeline, tetapi memengaruhi alur data UI.
- Dampak performa: policy check relatif kecil dibanding biaya network.
- Dampak memori: boundary origin membantu membatasi paparan data antar context.
- Dampak keamanan: SOP adalah fondasi isolasi data antar situs.

## 5. Why This Exists

SOP ada untuk mencegah satu situs membaca data privat situs lain
hanya karena keduanya dibuka pada browser yang sama.

## 6. Minimal Code Example

```js
// Request lintas origin bisa dikirim,
// tetapi akses response oleh script tunduk SOP/CORS.
fetch("https://api.other-origin.example/data");
```

## 7. Common Misconceptions

- "SOP memblokir semua request lintas origin"
  - Koreksi: request bisa terkirim; yang dibatasi adalah akses data response oleh script.
- "SOP hanya berlaku untuk fetch"
  - Koreksi: SOP memengaruhi banyak interaksi lintas origin pada Web Platform.

## 8. Pitfalls and Best Practices

- Pitfall: menganggap data lintas origin otomatis aman karena request sukses di network tab.
- Pitfall: membuka policy terlalu longgar untuk kemudahan sementara.
- Best practice: rancang API dengan boundary origin dan prinsip least privilege.

## 9. Prerequisites

- [Fetch API Fundamentals](../L2-core-apis/fetch-api-fundamentals.md)
- [URL and History](../L2-core-apis/url-and-history.md)

## 10. Next Topics

- [CORS](./cors.md)
- [Secure Context](./secure-context.md)
