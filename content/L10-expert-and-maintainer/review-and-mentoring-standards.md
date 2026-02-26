# Review and Mentoring Standards

- Level: L10
- Status: Stable
- Depth: expert
- Specs:
  - Technical review and mentoring quality standards context
- Prerequisites: Curriculum Maintenance
- Next Topics: Continuous L0-L10 Quality Stewardship

---

## 1. Official Term

Review and Mentoring Standards

## 2. Formal Definition

Review and mentoring standards adalah standar operasional
untuk memastikan proses review teknis dan pembinaan penulis
konsisten, adil, evidence-based, dan menghasilkan peningkatan kompetensi.

## 3. Mental Model

Review menjaga kualitas artefak.
Mentoring meningkatkan kualitas pembuat artefak.
Keduanya harus berjalan sebagai loop berkelanjutan.

### Wireframe Ringkas

```text
[Draft topic]
  -> technical review (spec/runtime checks)
  -> actionable feedback
  -> mentoring follow-up
  -> revised draft
  -> approval + learning notes
```

## 4. Runtime Perspective

- Thread/process: reviewer wajib menilai apakah narasi eksekusi (main thread/worker/process) tepat dan tidak tercampur.
- Queue model: mentoring menekankan akurasi model queue agar debugging mindset penulis tetap benar.
- Scheduling: standar review memeriksa klaim scheduling terhadap perilaku host yang normatif.
- Rendering interaction: reviewer memvalidasi bahwa dampak rendering dibahas saat topik menyentuh UI responsiveness.
- Dampak performa: feedback harus mengarahkan ke metrik dan budget, bukan opini umum.
- Dampak memori: penulis dibimbing untuk mengaitkan desain API dengan memory lifetime nyata.
- Dampak keamanan: reviewer memaksa explicit boundary analysis pada konten security-sensitive.

## 5. Why This Exists

Untuk menjaga transfer knowledge tetap berkualitas tinggi
sekaligus membangun kapasitas reviewer/author generasi berikutnya.

## 6. Minimal Code Example

```text
Contoh rubric review:
- Akurasi spec: 0-2
- Kejelasan runtime: 0-2
- Kedalaman tradeoff: 0-2
- Kualitas wireframe: 0-2
- Actionability feedback: 0-2
Lulus jika total >= 8 dan tidak ada skor 0 di akurasi spec.
```

## 7. Common Misconceptions

- "Mentoring sama dengan proofreading"
  - Koreksi: mentoring mencakup reasoning teknis, bukan hanya gaya bahasa.
- "Reviewer harus selalu memberi solusi final"
  - Koreksi: reviewer memberi arah dan constraint; author tetap bertanggung jawab atas desain akhir.

## 8. Pitfalls and Best Practices

- Pitfall: feedback umum tanpa contoh perbaikan konkret.
- Pitfall: standar review berubah-ubah antar reviewer.
- Best practice: gunakan rubric stabil, contoh good/bad patterns, dan sesi retrospektif mentor.

## 9. Prerequisites

- [Curriculum Maintenance](./curriculum-maintenance.md)
- [Incident Analysis Framework](../L9-senior-engineering/incident-analysis-framework.md)

## 10. Next Topics

- [L10 - Expert and Maintainer](./index.md) sebagai anchor continuous L0-L10 quality stewardship.
