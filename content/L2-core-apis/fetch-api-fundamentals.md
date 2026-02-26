# Fetch API Fundamentals

- Level: L2
- Status: Stable
- Depth: core
- Specs:
  - Fetch Standard
  - HTML Standard (event loop integration)
- Prerequisites: Timers
- Next Topics: URL and History

---

## 1. Official Term

Fetch API

## 2. Formal Definition

Fetch API adalah antarmuka host untuk melakukan request network
berbasis algoritma Fetch Standard, dengan model Promise,
request/response objects, mode, credentials, dan policy terkait origin.

## 3. Mental Model

`fetch()` memulai pipeline request secara asinkron.
Hasilnya tidak langsung data final, tetapi Promise untuk response.

### Wireframe Ringkas

```text
fetch(request)
   -> network pipeline
   -> response headers received
   -> Promise resolved (Response)
   -> body consumed (json/text/stream)
```

## 4. Runtime Perspective

- Thread/process: pemanggilan API dari main thread; network ditangani subsistem browser.
- Queue model: resolution Promise masuk microtask checkpoint.
- Scheduling: completion callback mengikuti event loop host setelah response siap.
- Rendering interaction: callback parsing berat bisa mengganggu frame jika di main thread.
- Dampak performa: request berlebihan/parsing besar menambah latency UI.
- Dampak memori: menyimpan response besar tanpa streaming meningkatkan memory pressure.
- Dampak keamanan: tunduk pada SOP, CORS, mixed content, dan credentials policy.

## 5. Why This Exists

Fetch menyatukan model network modern berbasis Promise
dan menyediakan kontrol request/response yang konsisten lintas browser.

## 6. Minimal Code Example

```js
async function loadUser() {
  const res = await fetch("/api/user", { credentials: "include" });
  if (!res.ok) throw new Error("request failed");
  return res.json();
}
```

## 7. Common Misconceptions

- "Fetch reject kalau status 404"
  - Koreksi: Promise fetch reject untuk network error; status HTTP non-2xx tetap resolve.
- "Fetch adalah fitur JavaScript language"
  - Koreksi: Fetch adalah Web Platform API.

## 8. Pitfalls and Best Practices

- Pitfall: tidak cek `response.ok`.
- Pitfall: mengabaikan cancellation (`AbortController`) pada request yang tidak relevan lagi.
- Best practice: validasi status, batasi payload, dan kelola lifecycle request.

## 9. Prerequisites

- [Timers](./timers.md)
- [Concurrency Model](../L1-runtime-model/concurrency-model.md)

## 10. Next Topics

- [URL and History](./url-and-history.md)
- [Storage](./storage.md)
