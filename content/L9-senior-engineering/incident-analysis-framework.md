# Incident Analysis Framework

- Level: L9
- Status: Stable
- Depth: senior
- Specs:
  - Runtime behavior and reliability analysis context
- Prerequisites: Design Review Framework
- Next Topics: Performance and Reliability Planning

---

## 1. Official Term

Incident Analysis Framework

## 2. Formal Definition

Incident analysis framework adalah metode terstruktur
untuk menganalisis gangguan produksi,
menentukan root cause, contributing factors,
dan corrective actions yang terukur.

## 3. Mental Model

Insiden bukan hanya "apa yang rusak",
tetapi "mengapa sistem memungkinkan itu terjadi".

### Wireframe Ringkas

```text
[Incident signal]
  -> timeline reconstruction
  -> root cause + contributing factors
  -> corrective/preventive actions
  -> ownership + due dates
```

## 4. Runtime Perspective

- Thread/process: rekonstruksi insiden harus memetakan context eksekusi yang terlibat.
- Queue model: cek interleaving async yang memicu failure.
- Scheduling: identifikasi starvation, timeout, retry storm, atau priority inversion.
- Rendering interaction: jika insiden UI, hubungkan ke long tasks/frame drops.
- Dampak performa: ukur blast radius melalui SLI/SLO terpengaruh.
- Dampak memori: identifikasi memory leak/churn patterns sebagai faktor.
- Dampak keamanan: klasifikasikan apakah ada implikasi data exposure/policy bypass.

## 5. Why This Exists

Agar organisasi belajar dari kegagalan secara sistematis
bukan sekadar menutup gejala.

## 6. Minimal Code Example

```text
Struktur post-incident note:
1) Impact
2) Timeline (UTC)
3) Root cause
4) Contributing factors
5) Corrective actions
6) Verification plan
```

## 7. Common Misconceptions

- "Cukup fix bug, analisis mendalam tidak perlu"
  - Koreksi: tanpa analisis, faktor sistemik sering terulang.
- "Satu akar penyebab selalu cukup"
  - Koreksi: insiden nyata biasanya multi-faktor.

## 8. Pitfalls and Best Practices

- Pitfall: blame individual, bukan sistem.
- Pitfall: corrective action tanpa owner/deadline.
- Best practice: gunakan data objektif + action yang dapat diverifikasi.

## 9. Prerequisites

- [Cross-API Debugging Playbook](../L6-applied-systems/cross-api-debugging-playbook.md)
- [Race Condition Diagnosis](../L6-applied-systems/race-condition-diagnosis.md)

## 10. Next Topics

- [Performance and Reliability Planning](./performance-and-reliability-planning.md)
