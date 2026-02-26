# Browser API Fundamentals V2

Repository ini adalah referensi arsitektural Web Platform dan Browser APIs.

Ini bukan tutorial JavaScript.
Ini bukan panduan framework.
Ini bukan kumpulan snippet.

Repository ini berfokus pada pemahaman layer Web Platform secara sistematis dan spec-aligned.

---

## 🎯 Tujuan

Memahami secara mendalam:

- Bagaimana Event Loop bekerja
- Bagaimana Task dan Microtask dijadwalkan
- Kapan rendering terjadi
- Bagaimana Fetch diproses oleh browser
- Bagaimana Security boundary membatasi akses
- Bagaimana concurrency dimodelkan
- Bagaimana object lifecycle dan memory retention terjadi

---

## 🧱 Layer Arsitektur

ECMAScript (Language)
↓
JavaScript Engine (V8 / SpiderMonkey / JavaScriptCore)
↓
Web Platform (HTML Standard, DOM Standard, Fetch Standard, Streams Standard, dll)
↓
Browser Implementation (Blink / WebKit / Gecko)

Repository ini fokus pada layer **Web Platform**.

---

## 📚 Struktur Level

Konten dibagi menjadi beberapa level:

- L0 — Platform Map
- L1 — Runtime Model
- L2 — Core APIs
- L3 — Performance & Security
- L4 — Advanced Deep Dive
- L5 — Watchlist / Experimental

Lihat detail di `curriculum/LEVELS.md`.

---

## 🧭 Filosofi

- Menggunakan terminologi resmi dari specification.
- Penjelasan menggunakan Bahasa Indonesia.
- Berorientasi runtime model.
- Tidak mencampur framework abstraction.
- Tidak membahas Node.js APIs.

---

## 📌 Prinsip Utama

Setiap topik harus menjawab:

- Berjalan di thread mana?
- Masuk queue apa?
- Siapa yang menjadwalkan?
- Kapan rendering bisa terjadi?
- Apa dampaknya ke performa?
- Apa dampaknya ke keamanan?
