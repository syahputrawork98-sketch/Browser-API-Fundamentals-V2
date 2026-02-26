# Race Condition Diagnosis

- Level: L6
- Status: Stable
- Depth: applied
- Specs:
  - HTML event loop model
  - API concurrency behavior context
- Prerequisites: Cross-API Debugging Playbook
- Next Topics: Scheduling and Rendering Bottleneck Analysis

---

## 1. Official Term

Race Condition

## 2. Formal Definition

Race condition adalah kondisi ketika hasil akhir sistem
bergantung pada urutan timing eksekusi async yang tidak dijamin,
sehingga aplikasi menghasilkan state yang tidak konsisten.

## 3. Mental Model

Dua atau lebih alur async "berlomba" menulis state.
Siapa selesai terakhir bisa menimpa hasil yang seharusnya tidak berlaku lagi.

### Wireframe Ringkas

```text
Request A start -----> finish (slow)
Request B start -> finish (fast)
State update order mismatch => stale overwrite risk
```

## 4. Runtime Perspective

- Thread/process: race bisa terjadi meski single-threaded, karena interleaving async completion.
- Queue model: completion callback dari source berbeda masuk event loop pada waktu berbeda.
- Scheduling: latensi network/IO/user input membuat urutan completion tidak deterministik.
- Rendering interaction: UI bisa menampilkan state lama/berkedip jika race tidak ditangani.
- Dampak performa: retry/polling tanpa kontrol dapat memperparah race.
- Dampak memori: state snapshot berlebih untuk mitigasi race dapat menambah overhead.
- Dampak keamanan: race pada flow auth/permission bisa menimbulkan state boundary yang salah.

## 5. Why This Exists

Diagnosis race penting agar aplikasi tetap deterministik
meski bekerja dengan banyak operasi async paralel.

## 6. Minimal Code Example

```js
let latestRequestId = 0;
async function loadData(query) {
  const id = ++latestRequestId;
  const res = await fetch(`/search?q=${encodeURIComponent(query)}`);
  const data = await res.json();
  if (id !== latestRequestId) return; // abaikan hasil stale
  render(data);
}
```

## 7. Common Misconceptions

- "Race cuma ada di multi-thread"
  - Koreksi: event-loop async interleaving juga bisa memicu race.
- "Urutan pemanggilan sama dengan urutan selesai"
  - Koreksi: completion order bisa berbeda.

## 8. Pitfalls and Best Practices

- Pitfall: update state tanpa token/version check.
- Pitfall: tidak membatalkan request lama saat intent user berubah.
- Best practice: gunakan idempotent state transitions, cancellation, dan guard versi.

## 9. Prerequisites

- [Tasks vs Microtasks](../L1-runtime-model/tasks-vs-microtasks.md)
- [Concurrency Model](../L1-runtime-model/concurrency-model.md)

## 10. Next Topics

- [Scheduling and Rendering Bottleneck Analysis](./scheduling-and-rendering-bottleneck-analysis.md)
