# Cross-Level Review Rubric

- Level: L10
- Status: Stable
- Depth: expert
- Specs:
  - Quality gate scoring and review standardization context
- Prerequisites: Maintainer Operations Playbook
- Next Topics: Audit Cadence Blueprint

---

## 1. Official Term

Cross-Level Review Rubric

## 2. Formal Definition

Cross-level review rubric adalah kerangka penilaian terstandardisasi
untuk mengevaluasi kualitas topik lintas level L0-L10
secara objektif, konsisten, dan dapat diaudit.

## 3. Mental Model

Rubric menyamakan quality bar antar reviewer:
setiap topik dinilai dengan kriteria dan skor yang sama
agar keputusan lulus/tidak tidak bergantung opini personal.

### Wireframe Ringkas

```text
[Topic draft]
  -> score by criteria
  -> detect critical gaps
  -> assign pass/fix-required
  -> track score trend per level
```

## 4. Runtime Perspective

- Thread/process: rubric mewajibkan kejelasan mapping eksekusi (main thread/worker/process) untuk tiap topik teknis.
- Queue model: penilaian menolak konten yang ambigu pada task vs microtask vs host queue lainnya.
- Scheduling: skor runtime turun jika scheduling path tidak dijelaskan dengan benar.
- Rendering interaction: topik terkait UI harus menjelaskan interaksi terhadap rendering pipeline.
- Dampak performa: rubric memberi bobot pada keberadaan budget/metric/performance implication.
- Dampak memori: scoring memeriksa coverage memory lifetime dan retention risk.
- Dampak keamanan: topik dinilai gagal jika boundary keamanan disebut tanpa mekanisme teknis.

## 5. Why This Exists

Untuk meminimalkan variasi kualitas hasil review
dan menyediakan dasar keputusan yang dapat dipertanggungjawabkan.

## 6. Minimal Code Example

```text
Contoh bobot rubric:
- Terminologi spec: 20%
- Akurasi runtime: 25%
- Kejelasan mental model + wireframe: 15%
- Tradeoff performa/memori/keamanan: 25%
- Navigasi prerequisite/next topic: 15%
Pass jika skor total >= 85 dan tidak ada critical fail.
```

## 7. Common Misconceptions

- "Rubric membuat review kaku"
  - Koreksi: rubric menstandardisasi minimum quality bar, bukan melarang judgment profesional.
- "Skor tinggi otomatis berarti topik siap publish"
  - Koreksi: tetap perlu sanity check konteks batch dan dampak lintas dokumen.

## 8. Pitfalls and Best Practices

- Pitfall: kriteria terlalu abstrak sehingga reviewer menafsirkan berbeda.
- Pitfall: tidak mendefinisikan kondisi critical fail.
- Best practice: tetapkan definisi skor per level dan contoh artefak pass/fail.

## 9. Prerequisites

- [Maintainer Operations Playbook](./maintainer-operations-playbook.md)
- [Curriculum Maintenance](./curriculum-maintenance.md)

## 10. Next Topics

- [Audit Cadence Blueprint](./audit-cadence-blueprint.md)
