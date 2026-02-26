# Navigation API

- Level: L5
- Status: Experimental
- Depth: watchlist
- Specs:
  - Navigation API draft/living specification context
- Prerequisites: L4 - Advanced Deep Dive
- Next Topics: Scheduler API

---

## 1. Official Term

Navigation API

## 2. Formal Definition

Navigation API menyediakan antarmuka modern untuk mengamati,
menangani, dan mengintersepsi navigasi dokumen secara lebih terstruktur
dibanding pola historis berbasis `popstate` saja.

## 3. Mental Model

API ini memberi "kontrol lapisan navigasi" yang lebih eksplisit
untuk transisi route pada aplikasi web modern.

### Wireframe Ringkas

```text
[User/App navigation intent]
    -> Navigation API event
    -> optional interception
    -> commit navigation state
```

## 4. Runtime Perspective

- Thread/process: event navigasi diproses pada context dokumen (main thread).
- Queue model: callback navigasi mengikuti task/event loop host.
- Scheduling: browser mengoordinasikan lifecycle navigasi dan history state.
- Rendering interaction: interception memengaruhi kapan UI transisi dirender.
- Dampak performa: handler navigasi berat menambah latency transisi.
- Dampak memori: state navigasi kompleks perlu lifecycle management yang ketat.
- Dampak keamanan: tetap tunduk pada origin boundary dan policy navigasi browser.

## 5. Why This Exists

Agar pengelolaan navigasi SPA menjadi lebih konsisten,
lebih mudah diobservasi, dan lebih terintegrasi dengan model platform modern.

## 6. Minimal Code Example

```js
if ("navigation" in window) {
  navigation.addEventListener("navigate", (event) => {
    console.log("navigate to", event.destination?.url);
  });
}
```

## 7. Common Misconceptions

- "Navigation API sudah baseline di semua browser"
  - Koreksi: dukungan masih bervariasi.
- "API ini menggantikan semua pola routing saat ini"
  - Koreksi: adopsi bertahap dan fallback tetap diperlukan.

## 8. Pitfalls and Best Practices

- Pitfall: mengandalkan API tanpa feature detection.
- Pitfall: tidak menyediakan fallback ke History API.
- Best practice: gunakan progressive enhancement dan guard capability.

## 9. Prerequisites

- [URL and History](../L2-core-apis/url-and-history.md)
- [Document Lifecycle](../L1-runtime-model/document-lifecycle.md)

## 10. Next Topics

- [Scheduler API](./scheduler-api.md)
