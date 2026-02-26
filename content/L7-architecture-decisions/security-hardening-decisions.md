# Security Hardening Decisions

- Level: L7
- Status: Stable
- Depth: architecture
- Specs:
  - CSP, Trusted Types, COOP/COEP related policy context
  - SOP/CORS/Secure Context baseline
- Prerequisites: Cache and Invalidation Architecture
- Next Topics: L8 - Spec Reading and Validation

---

## 1. Official Term

Security Hardening Decisions

## 2. Formal Definition

Security hardening decisions adalah keputusan desain
untuk memperketat security posture aplikasi web
melalui kombinasi policy, boundary, dan safe defaults.

## 3. Mental Model

Hardening bukan satu fitur,
melainkan kumpulan kontrol yang saling melengkapi.

### Wireframe Ringkas

```text
[Threat Model]
   -> choose controls (CSP / Trusted Types / COOP-COEP / cookie policy)
   -> rollout + monitor
   -> iterate based on incidents
```

## 4. Runtime Perspective

- Thread/process: policy enforcement dilakukan browser di boundary request, parser, dan execution contexts.
- Queue model: enforcement tidak mengubah queue dasar, tetapi dapat memblokir operasi sebelum berjalan.
- Scheduling: pelanggaran policy tercatat sebagai signal observability.
- Rendering interaction: resource blocked by policy dapat mengubah hasil render.
- Dampak performa: beberapa policy menambah overhead kecil namun memberi tradeoff keamanan signifikan.
- Dampak memori: tidak dominan, kecuali logging/telemetry hardening yang berlebihan.
- Dampak keamanan: menurunkan attack surface dan memperkecil blast radius.

## 5. Why This Exists

Untuk mengurangi risiko eksploitasi pada sistem nyata
melalui keputusan arsitektur yang eksplisit dan dapat diaudit.

## 6. Minimal Code Example

```http
Content-Security-Policy: default-src 'self'; script-src 'self'
Cross-Origin-Opener-Policy: same-origin
Cross-Origin-Embedder-Policy: require-corp
```

## 7. Common Misconceptions

- "Hardening bisa ditunda sampai ada insiden"
  - Koreksi: hardening efektif justru dilakukan sebelum insiden.
- "Satu header keamanan sudah cukup"
  - Koreksi: perlu kombinasi kontrol sesuai threat model.

## 8. Pitfalls and Best Practices

- Pitfall: mengaktifkan policy ketat tanpa tahap observasi dan rollout.
- Pitfall: kebijakan berbeda antar lingkungan tanpa dokumentasi.
- Best practice: lakukan rollout bertahap, monitor violation reports, dan review berkala.

## 9. Prerequisites

- [Same-Origin Policy](../L3-performance-and-security/same-origin-policy.md)
- [CORS](../L3-performance-and-security/cors.md)
- [Cross-Origin Isolation](../L3-performance-and-security/cross-origin-isolation.md)

## 10. Next Topics

- L8 - Spec Reading and Validation
