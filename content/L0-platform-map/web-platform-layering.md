# Web Platform Layering

- Level: L0
- Status: Stable
- Depth: core
- Specs:
  - ECMAScript specification
  - HTML Standard
  - DOM Standard
  - Fetch Standard
- Prerequisites: none
- Next Topics: Specification Landscape

---

## 1. Official Term

Web Platform

## 2. Formal Definition

Web Platform adalah kumpulan specification yang mendefinisikan API host,
processing model, dan perilaku runtime browser environment.

Web Platform bukan bagian dari ECMAScript language specification.

## 3. Mental Model

Layer arsitektur:

ECMAScript (language rules)
-> JavaScript engine (runtime bahasa)
-> Web Platform APIs (host environment)
-> Browser implementation (engine + process model + UI)

ECMAScript mendefinisikan semantik bahasa.
Web Platform mendefinisikan kemampuan host seperti DOM, Fetch, dan Timers.

## 4. Runtime Perspective

Ketika Anda menulis kode berikut:

```js
fetch("https://example.com").then(() => {
  console.log("done");
});
```

Yang terjadi secara konseptual:

- JavaScript engine mengeksekusi syntax dan Promise semantics (ECMAScript)
- Host API `fetch` disediakan oleh Web Platform (Fetch Standard)
- Penyelesaian Promise masuk ke microtask checkpoint pada event loop host
- Event loop dan scheduling berada di HTML processing model, bukan ECMAScript

Implikasi:

- Thread/queue/scheduling adalah tanggung jawab host browser
- Rendering tidak dilakukan oleh JavaScript language
- API availability ditentukan host, bukan spesifikasi bahasa

## 5. Why This Exists

Pemisahan layer ini ada agar:

- Bahasa dapat tetap portabel di banyak host
- Host dapat menambah capability tanpa mengubah inti bahasa
- Batas tanggung jawab spesifikasi tetap jelas

## 6. Minimal Code Example

```js
console.log(typeof Promise); // ECMAScript feature
console.log(typeof fetch); // Web Platform host API (di browser)
```

Contoh ini menunjukkan bahwa fitur bahasa dan fitur host berasal dari layer berbeda.

## 7. Common Misconceptions

- "JavaScript punya fetch"
  - Koreksi: `fetch` adalah Web Platform API.
- "Event loop adalah bagian JavaScript"
  - Koreksi: event loop adalah model di HTML Standard.
- "Kalau ada di browser, pasti dari ECMAScript"
  - Koreksi: banyak API browser berasal dari specification host.

## 8. Pitfalls and Best Practices

- Pitfall: mencampur language semantics dan host behavior
- Pitfall: asumsi API browser tersedia di semua host JavaScript
- Best practice: selalu sebut layer sumber fitur saat menjelaskan API
- Best practice: cek specification primer untuk batas tanggung jawab

## 9. Prerequisites

Tidak ada.

## 10. Next Topics

Specification Landscape
