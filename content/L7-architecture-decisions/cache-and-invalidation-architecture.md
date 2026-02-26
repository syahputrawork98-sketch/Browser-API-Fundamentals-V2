# Cache and Invalidation Architecture

- Level: L7
- Status: Stable
- Depth: architecture
- Specs:
  - HTTP caching model context
  - Cache Storage and Service Worker context
- Prerequisites: Worker vs Main Thread Strategy
- Next Topics: Security Hardening Decisions

---

## 1. Official Term

Cache and Invalidation Architecture

## 2. Formal Definition

Ini adalah desain kebijakan cache lintas lapisan
(HTTP cache, Cache Storage, in-memory cache, data cache aplikasi)
serta strategi invalidasi agar data tetap konsisten dan efisien.

## 3. Mental Model

Cache mempercepat akses data,
tetapi setiap cache menambah risiko stale data jika invalidasi buruk.

### Wireframe Ringkas

```text
[Origin Data]
  -> HTTP Cache
  -> Service Worker Cache
  -> App Memory Cache
Invalidate policy keeps layers consistent
```

## 4. Runtime Perspective

- Thread/process: keputusan cache bisa dieksekusi di main thread, service worker, dan network stack.
- Queue model: fetch/cached response flow mengikuti task/microtask sesuai API yang dipakai.
- Scheduling: revalidation/background refresh menambah workload async tambahan.
- Rendering interaction: cache hit mempercepat data-to-UI path; stale data memicu UI mismatch.
- Dampak performa: cache tepat menurunkan latency dan bandwidth.
- Dampak memori: cache berlapis tanpa budget dapat menyebabkan storage/memory bloat.
- Dampak keamanan: cache data sensitif harus memperhatikan scope, lifetime, dan leakage risk.

## 5. Why This Exists

Agar arsitektur data tetap cepat namun benar,
terutama pada aplikasi offline-capable atau high-traffic.

## 6. Minimal Code Example

```js
const cache = await caches.open("app-v1");
await cache.put("/api/config", new Response(JSON.stringify({ v: 1 })));
```

## 7. Common Misconceptions

- "Tambah cache selalu mempercepat"
  - Koreksi: tanpa invalidasi tepat, cache bisa merusak konsistensi dan UX.
- "Satu strategi cache cukup untuk semua data"
  - Koreksi: data immutable dan mutable butuh kebijakan berbeda.

## 8. Pitfalls and Best Practices

- Pitfall: tidak ada versioning cache key.
- Pitfall: invalidasi massal tanpa rollout plan.
- Best practice: definisikan TTL/version/revalidation per kategori data.

## 9. Prerequisites

- [Service Worker Lifecycle](../L4-advanced-deep-dive/service-worker-lifecycle.md)
- [Storage](../L2-core-apis/storage.md)

## 10. Next Topics

- [Security Hardening Decisions](./security-hardening-decisions.md)
