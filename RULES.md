# Aturan Kontribusi V2

Dokumen ini adalah kontrak kualitas untuk seluruh konten di V2.
Tujuan utama V2 adalah memberi jalur belajar bertingkat dari dasar sampai level advanced/senior.

---

## 1. Tujuan dan Cakupan

V2 harus membantu pembaca bergerak bertahap dari:

- pemahaman konsep dasar Web Platform
- ke kemampuan analisis runtime nyata
- ke pengambilan keputusan arsitektur level senior

Konten wajib berorientasi:

- spec-aligned
- runtime-aware
- sistematis
- bisa divalidasi

---

## 2. Batas Arsitektur (Wajib)

Setiap topik wajib membedakan secara eksplisit:

- ECMAScript (spesifikasi bahasa)
- JavaScript Engine (mesin eksekusi)
- Web Platform APIs (host APIs)
- Browser Implementation (engine/process model)

Dilarang menyebut Web APIs sebagai bagian dari JavaScript language.

---

## 3. Kanon Terminologi

Istilah ambigu wajib dikoreksi secara eksplisit:

- "JavaScript event loop" -> Event Loop (HTML Standard)
- "JavaScript fetch" -> Fetch API (Fetch Standard)
- "JavaScript timer" -> Timers (HTML Standard)

Jika ada konflik istilah, ikuti istilah resmi specification.

---

## 4. Roadmap Level Pembelajaran (L0-L10)

### Foundation

- L0: Platform Map
- L1: Runtime Model
- L2: Core APIs
- L3: Performance and Security
- L4: Advanced Deep Dive
- L5: Watchlist and Experimental

### Professional

- L6: Applied Systems (debugging kasus nyata lintas API)
- L7: Architecture Decisions (tradeoff dan keputusan desain)
- L8: Spec Reading and Validation (membaca algoritma spec langsung)

### Senior Track

- L9: Senior Engineering (design review, incident analysis, optimization plan)
- L10: Expert and Maintainer (quality governance, standardisasi kurikulum)

Setiap level wajib punya:

- Tujuan Level
- Yang Harus Bisa Setelah Selesai
- Topik Wajib
- Syarat Sebelum Naik Level

---

## 5. Kontrak Struktur Topik (Wajib)

Setiap topik wajib mengikuti 10 bagian berikut:

1. Official Term
2. Formal Definition
3. Mental Model
4. Runtime Perspective
5. Why This Exists
6. Minimal Code Example
7. Common Misconceptions
8. Pitfalls and Best Practices
9. Prerequisites
10. Next Topics

Tambahan metadata wajib di bagian atas file:

- Level
- Status
- Depth
- Specs
- Prerequisites
- Next Topics

---

## 6. Runtime Coverage Minimum

Bagian Runtime Perspective wajib mencakup:

- Thread/process tempat eksekusi utama
- Queue model (task, microtask, atau model lain yang relevan)
- Scheduling mechanism
- Rendering interaction
- Dampak performa
- Dampak memori
- Dampak keamanan

---

## 7. Quality Gate Naik Level

Topik dinyatakan lulus hanya jika:

- semua 10 bagian terisi
- terminologi tidak melanggar batas arsitektur
- minimal satu miskonsepsi dikoreksi jelas
- ada penjelasan dampak runtime yang konkret
- `Prerequisites` dan `Next Topics` konsisten dengan level

Naik ke level berikutnya hanya setelah seluruh topik wajib level saat ini lulus quality gate.

---

## 8. Larangan Konten

Dilarang menulis:

- oversimplification yang merusak akurasi
- framework-first explanation
- Node.js specific APIs (kecuali disebut sebagai pembanding, bukan fokus)
- analogi menyesatkan
- copy-paste definisi tanpa pemahaman runtime

---

## 9. Sumber Kebenaran

Referensi primer yang wajib diprioritaskan:

- HTML Standard
- DOM Standard
- Fetch Standard
- Streams Standard
- Infra Standard
- Web IDL
- ECMAScript Specification

Dokumentasi sekunder (misalnya MDN, blog) boleh dipakai untuk konteks,
namun tidak boleh menggantikan specification sebagai sumber normatif.

---

## 10. Definisi Selesai (Definition of Done)

Satu topik dianggap selesai jika:

- lolos struktur 10 bagian
- lolos runtime coverage minimum
- lolos quality gate level
- istilah konsisten dengan kanon terminologi
- referensi specification tercantum

Jika salah satu poin gagal, topik tetap berstatus draft.
