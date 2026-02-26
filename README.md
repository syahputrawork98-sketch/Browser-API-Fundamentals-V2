# Browser API Fundamentals V2

Repository ini adalah referensi arsitektural Web Platform dan Browser APIs
untuk pembelajaran bertingkat dari fundamental sampai senior.

Ini bukan tutorial JavaScript.
Ini bukan panduan framework.
Ini bukan kumpulan snippet.

---

## 1. Tujuan

Memahami secara mendalam:

- bagaimana event loop bekerja
- bagaimana task dan microtask dijadwalkan
- kapan rendering terjadi
- bagaimana fetch diproses browser
- bagaimana security boundary membatasi akses
- bagaimana concurrency dimodelkan
- bagaimana object lifecycle dan memory retention terjadi

---

## 2. Layer Arsitektur

Model layer:

ECMAScript (Language)
-> JavaScript Engine (V8 / SpiderMonkey / JavaScriptCore)
-> Web Platform (HTML, DOM, Fetch, Streams, dan lain-lain)
-> Browser Implementation (Blink / WebKit / Gecko)

Fokus repository ini adalah layer Web Platform.

---

## 3. Struktur Level (L0-L10)

### Foundation

- L0: Platform Map
- L1: Runtime Model
- L2: Core APIs
- L3: Performance and Security
- L4: Advanced Deep Dive
- L5: Watchlist and Experimental

### Professional

- L6: Applied Systems
- L7: Architecture Decisions
- L8: Spec Reading and Validation

### Senior Track

- L9: Senior Engineering
- L10: Expert and Maintainer

---

## 4. Navigasi Cepat

- Aturan kontribusi dan quality gate: `RULES.md`
- Definisi level pembelajaran: `curriculum/LEVELS.md`
- Jalur belajar lintas level: `curriculum/PATHS.md`
- Panduan wireframe pembelajaran: `curriculum/WIREFRAMES.md`
- Sumber spesifikasi primer: `specs/SOURCES.md`
- Catatan perubahan versi: `CHANGELOG.md`
- Konten awal L0: `content/L0-platform-map/`

---

## 5. Cara Mulai Belajar

Urutan rekomendasi:

1. Baca `curriculum/LEVELS.md` untuk memahami target tiap level.
2. Baca `curriculum/PATHS.md` untuk memilih jalur progres.
3. Baca `curriculum/WIREFRAMES.md` agar punya peta visual sebelum detail teknis.
4. Mulai dari konten L0 di `content/L0-platform-map/`.
5. Gunakan `RULES.md` sebagai checklist saat menulis atau mereview topik.

---

## 6. Prinsip Penulisan

Setiap topik wajib:

- spec-aligned
- runtime-aware
- menggunakan terminologi resmi specification
- memisahkan jelas: ECMAScript vs Web APIs vs browser implementation
- menyertakan wireframe ringkas di bagian Mental Model

Standar lengkap ada di `RULES.md`.

---

## 7. Pertanyaan Inti Tiap Topik

Setiap topik harus menjawab:

- berjalan di thread atau process mana
- masuk queue apa
- siapa yang menjadwalkan
- kapan rendering dapat terjadi
- apa dampaknya ke performa
- apa dampaknya ke memori
- apa dampaknya ke keamanan

---

## 8. Status Saat Ini

V2 sedang dibangun sebagai struktur utama pembelajaran bertingkat.
Konten L0-L4 sudah tersedia penuh untuk cakupan inti saat ini.
