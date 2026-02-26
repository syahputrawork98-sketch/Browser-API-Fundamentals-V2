# IndexedDB Transaction Model

- Level: L4
- Status: Stable
- Depth: advanced
- Specs:
  - Indexed Database API specification
- Prerequisites: Browser Process Model Deep Dive
- Next Topics: bfcache and Lifecycle Interaction

---

## 1. Official Term

IndexedDB Transaction Model

## 2. Formal Definition

IndexedDB menggunakan model transaksi untuk menjamin konsistensi operasi
pada object store dalam scope tertentu,
dengan mode utama seperti `readonly` dan `readwrite`.

Transaksi memiliki lifecycle (active, committing, finished/aborted)
yang diproses asinkron oleh event loop.

## 3. Mental Model

Operasi database terjadi dalam "sesi transaksi" terikat scope store.
Jika transaksi gagal, perubahan dalam scope transaksi tidak dipersist.

### Wireframe Ringkas

```text
open DB
  -> create transaction(scope, mode)
      -> enqueue requests (get/put/delete)
      -> auto-commit if successful
      -> abort on error
```

## 4. Runtime Perspective

- Thread/process: API dipanggil dari main thread/worker context; backend storage ditangani subsistem browser.
- Queue model: request IndexedDB asinkron mengembalikan hasil via event/task.
- Scheduling: transaksi memproses operasi berurutan sesuai aturan transaction scope.
- Rendering interaction: operasi besar yang memicu callback berat di main thread dapat mengganggu respons UI.
- Dampak performa: transaksi terlalu besar atau contention antar transaksi menambah latency.
- Dampak memori: object payload besar saat serialisasi/deserialisasi menambah pressure.
- Dampak keamanan: data terikat origin; tetap perlu threat model terhadap XSS pada origin yang sama.

## 5. Why This Exists

Model transaksi dibutuhkan untuk menjaga integritas data lokal
saat aplikasi melakukan operasi asinkron dan concurrent pada penyimpanan terstruktur.

## 6. Minimal Code Example

```js
const tx = db.transaction(["users"], "readwrite");
const store = tx.objectStore("users");
store.put({ id: 1, name: "Ada" });
tx.oncomplete = () => console.log("commit");
```

## 7. Common Misconceptions

- "IndexedDB itu sinkron seperti localStorage"
  - Koreksi: IndexedDB bersifat asinkron dengan model event/transaction.
- "Setiap request langsung permanen"
  - Koreksi: perubahan dipastikan saat transaksi commit.

## 8. Pitfalls and Best Practices

- Pitfall: transaction scope terlalu lebar sehingga contention tinggi.
- Pitfall: mengabaikan error/abort handling.
- Best practice: pecah operasi ke transaksi yang fokus dan tangani failure path eksplisit.

## 9. Prerequisites

- [Storage](../L2-core-apis/storage.md)
- [Concurrency Model](../L1-runtime-model/concurrency-model.md)

## 10. Next Topics

- [bfcache and Lifecycle Interaction](./bfcache-and-lifecycle-interaction.md)
