# Cross-Origin Isolation

- Level: L3
- Status: Stable
- Depth: core
- Specs:
  - HTML Standard (cross-origin isolation model)
  - COOP/COEP related policy headers
- Prerequisites: Secure Context
- Next Topics: L4 - Advanced Deep Dive

---

## 1. Official Term

Cross-Origin Isolation

## 2. Formal Definition

Cross-Origin Isolation adalah kondisi halaman
ketika policy seperti COOP dan COEP dikonfigurasi sesuai,
sehingga context mendapat isolasi lebih ketat dari cross-origin resources
untuk membuka capability tertentu (misalnya SharedArrayBuffer).

## 3. Mental Model

Halaman mengunci boundary lintas origin dengan policy header,
agar browser memberi fitur advanced yang butuh jaminan isolasi lebih tinggi.

### Wireframe Ringkas

```text
[Page]
  + COOP policy
  + COEP policy
      -> Cross-Origin Isolated = true
      -> advanced capabilities available
```

## 4. Runtime Perspective

- Thread/process: isolation memengaruhi cara browser mengelompokkan context dan resource sharing.
- Queue model: tidak mengubah task/microtask dasar, tetapi membatasi resource yang dapat dimuat/diakses.
- Scheduling: check policy terjadi saat navigasi/load resource.
- Rendering interaction: resource yang melanggar policy bisa diblok sehingga memengaruhi output UI.
- Dampak performa: ada tradeoff kompatibilitas resource pihak ketiga.
- Dampak memori: isolasi context dapat memengaruhi pola alokasi/proses secara tidak langsung.
- Dampak keamanan: meningkatkan mitigasi terhadap kelas serangan berbasis side-channel.

## 5. Why This Exists

Model ini ada untuk menyediakan baseline keamanan lebih kuat
sebelum browser mengaktifkan capability berisiko tinggi.

## 6. Minimal Code Example

```js
if (crossOriginIsolated) {
  console.log("isolated context aktif");
}
```

## 7. Common Misconceptions

- "COOP saja cukup untuk cross-origin isolation"
  - Koreksi: umumnya perlu kombinasi policy yang relevan (misalnya COOP + COEP).
- "Isolation hanya soal performa"
  - Koreksi: tujuan utama adalah boundary keamanan dan kesiapan capability tertentu.

## 8. Pitfalls and Best Practices

- Pitfall: mengaktifkan policy tanpa audit dependency resource pihak ketiga.
- Pitfall: gagal memonitor resource yang diblok karena header tidak kompatibel.
- Best practice: rollout bertahap dengan observability untuk resource failures.

## 9. Prerequisites

- [Secure Context](./secure-context.md)
- [Web Workers](../L2-core-apis/web-workers.md)

## 10. Next Topics

- L4 - Advanced Deep Dive
