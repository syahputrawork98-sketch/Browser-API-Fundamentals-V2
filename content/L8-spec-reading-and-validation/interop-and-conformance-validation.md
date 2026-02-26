# Interop and Conformance Validation

- Level: L8
- Status: Stable
- Depth: professional
- Specs:
  - Web Platform Tests (WPT) ecosystem context
  - Specification conformance principles
- Prerequisites: Normative Algorithm Tracing
- Next Topics: L9 - Senior Engineering

---

## 1. Official Term

Interoperability and Conformance Validation

## 2. Formal Definition

Interop and conformance validation adalah proses memverifikasi
apakah perilaku implementasi lintas browser selaras dengan specification,
serta mengidentifikasi deviasi melalui pengujian dan evidence yang dapat direproduksi.

## 3. Mental Model

Tujuan utama bukan sekadar "jalan di browser saya",
melainkan konsistensi behavior lintas implementasi.

### Wireframe Ringkas

```text
[Expected behavior from spec]
   -> [Run cross-browser checks]
   -> [Collect divergences]
   -> [Classify: app bug / browser bug / spec gap]
```

## 4. Runtime Perspective

- Thread/process: validasi perlu mempertimbangkan perbedaan scheduling antar engine.
- Queue model: verifikasi urutan task/microtask/event untuk kasus sensitif timing.
- Scheduling: perbedaan edge timing bisa menjadi sumber interop issue.
- Rendering interaction: cek perbedaan visual lifecycle (layout/paint timing) pada skenario sama.
- Dampak performa: pengujian lintas browser mencegah optimasi yang hanya valid di satu engine.
- Dampak memori: perilaku GC/memory bisa berbeda implementasi, perlu baseline per browser.
- Dampak keamanan: pastikan policy enforcement konsisten (SOP/CORS/secure context behavior).

## 5. Why This Exists

Agar aplikasi dan keputusan arsitektur
tetap robust pada ekosistem browser nyata,
bukan hanya pada satu implementasi.

## 6. Minimal Code Example

```text
Checklist validasi:
1) Definisikan expected behavior dari spec.
2) Uji pada minimal 2-3 browser.
3) Catat output aktual dan perbedaan.
4) Klasifikasikan penyebab dan tindak lanjut.
```

## 7. Common Misconceptions

- "Jika lulus di Chromium berarti standar sudah aman"
  - Koreksi: interop menuntut validasi lintas engine.
- "Perbedaan kecil bisa diabaikan"
  - Koreksi: deviasi kecil bisa jadi bug latent pada skala produksi.

## 8. Pitfalls and Best Practices

- Pitfall: tidak mendefinisikan expected behavior sebelum testing.
- Pitfall: menguji tanpa skenario reproducible.
- Best practice: pakai matriks interop, simpan evidence, dan track regression.

## 9. Prerequisites

- [Normative Algorithm Tracing](./normative-algorithm-tracing.md)
- [Cross-API Debugging Playbook](../L6-applied-systems/cross-api-debugging-playbook.md)

## 10. Next Topics

- L9 - Senior Engineering
