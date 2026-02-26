# Service Worker Lifecycle

- Level: L4
- Status: Stable
- Depth: advanced
- Specs:
  - Service Workers specification
  - Cache Storage integration context
- Prerequisites: Streams Deep Dive
- Next Topics: Browser Process Model Deep Dive

---

## 1. Official Term

Service Worker Lifecycle

## 2. Formal Definition

Service Worker lifecycle adalah rangkaian fase worker background khusus
mulai dari `install`, `activate`, hingga menangani event seperti `fetch`,
dengan model update/versioning yang berbeda dari script halaman biasa.

## 3. Mental Model

Service worker adalah perantara programmable antara aplikasi web dan network/cache,
bukan script halaman yang selalu aktif.

### Wireframe Ringkas

```text
register()
  -> install
  -> waiting
  -> activate
  -> fetch/message events
  -> update check (new worker version)
```

## 4. Runtime Perspective

- Thread/process: service worker berjalan di worker context terpisah dari halaman.
- Queue model: event (`install`, `activate`, `fetch`) diproses sebagai task pada event loop worker.
- Scheduling: browser dapat menghentikan/menjalankan kembali worker sesuai kebutuhan.
- Rendering interaction: tidak merender UI langsung, tapi memengaruhi data/resource yang sampai ke halaman.
- Dampak performa: strategi cache tepat meningkatkan latency; strategi buruk bisa menambah stale data.
- Dampak memori: cache berlebih tanpa invalidasi menambah storage pressure.
- Dampak keamanan: service worker hanya tersedia di secure context dan scope terkontrol.

## 5. Why This Exists

Service worker memungkinkan offline support,
cache strategy yang bisa diprogram,
dan kontrol request lebih fleksibel untuk aplikasi web modern.

## 6. Minimal Code Example

```js
self.addEventListener("install", (event) => {
  event.waitUntil(caches.open("v1"));
});

self.addEventListener("fetch", (event) => {
  event.respondWith(fetch(event.request));
});
```

## 7. Common Misconceptions

- "Service worker selalu aktif terus"
  - Koreksi: lifecycle-nya event-driven dan bisa dihentikan browser.
- "Update service worker langsung mengganti versi aktif"
  - Koreksi: ada fase waiting/activation flow.

## 8. Pitfalls and Best Practices

- Pitfall: strategi cache tanpa invalidasi versi.
- Pitfall: tidak mengelola transisi versi worker dengan aman.
- Best practice: desain versioning cache dan rollout update yang eksplisit.

## 9. Prerequisites

- [Fetch API Fundamentals](../L2-core-apis/fetch-api-fundamentals.md)
- [Storage](../L2-core-apis/storage.md)
- [Web Workers](../L2-core-apis/web-workers.md)

## 10. Next Topics

- [Browser Process Model Deep Dive](./browser-process-model-deep-dive.md)
