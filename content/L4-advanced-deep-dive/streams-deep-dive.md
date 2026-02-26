# Streams Deep Dive

- Level: L4
- Status: Stable
- Depth: advanced
- Specs:
  - Streams Standard
  - Fetch Standard (body streams integration)
- Prerequisites: L3 - Performance and Security
- Next Topics: Service Worker Lifecycle

---

## 1. Official Term

Streams API

## 2. Formal Definition

Streams API adalah model pemrosesan data bertahap
melalui `ReadableStream`, `WritableStream`, dan `TransformStream`,
agar data besar dapat diproses incremental tanpa menunggu seluruh payload selesai.

## 3. Mental Model

Daripada memuat seluruh data sekaligus,
stream memecah data menjadi chunk yang diproses berurutan.

### Wireframe Ringkas

```text
[Source]
   -> chunk1 -> chunk2 -> chunk3
   -> [ReadableStream] -> [Transform] -> [WritableStream/Sink]
```

## 4. Runtime Perspective

- Thread/process: pemrosesan stream di context yang membuatnya (main thread atau worker).
- Queue model: operasi stream async menghasilkan promise/microtask transitions.
- Scheduling: producer-consumer diselaraskan via backpressure.
- Rendering interaction: pemrosesan chunk berat di main thread bisa mengganggu frame.
- Dampak performa: stream menurunkan peak memory dibanding buffer penuh.
- Dampak memori: backpressure membantu menghindari akumulasi data tak terkendali.
- Dampak keamanan: parsing data incremental tetap harus validasi konten tak tepercaya.

## 5. Why This Exists

Streams diperlukan untuk kasus payload besar atau aliran berkelanjutan,
agar aplikasi lebih responsif dan efisien memori.

## 6. Minimal Code Example

```js
const res = await fetch("/large-data");
const reader = res.body.getReader();
while (true) {
  const { done, value } = await reader.read();
  if (done) break;
  console.log("chunk", value.length);
}
```

## 7. Common Misconceptions

- "Fetch selalu harus tunggu body selesai total"
  - Koreksi: body dapat dibaca sebagai stream secara bertahap.
- "Stream otomatis lebih cepat di semua kasus"
  - Koreksi: stream membantu pola tertentu; overhead bisa ada pada payload kecil.

## 8. Pitfalls and Best Practices

- Pitfall: mengabaikan cancel/close pada stream.
- Pitfall: melakukan transform berat per chunk di main thread.
- Best practice: gunakan worker untuk transform berat dan hormati backpressure.

## 9. Prerequisites

- [Fetch API Fundamentals](../L2-core-apis/fetch-api-fundamentals.md)
- [Concurrency Model](../L1-runtime-model/concurrency-model.md)

## 10. Next Topics

- [Service Worker Lifecycle](./service-worker-lifecycle.md)
