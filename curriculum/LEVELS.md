# Sistem Level Pembelajaran

Dokumen ini mendefinisikan level pembelajaran V2 dari fundamental sampai senior.
Setiap level berisi tujuan, capaian, fokus topik, dan syarat naik level.

---

## L0 - Platform Map

Tujuan Level:
Memahami peta besar Web Platform dan batas antar-layer.

Yang Harus Bisa Setelah Selesai:

- Membedakan ECMAScript vs Web Platform APIs
- Menjelaskan siapa mendefinisikan apa di landscape specification
- Menjelaskan bahwa event loop bukan bagian dari language spec

Topik Wajib:

- Web Platform Layering
- Specification Landscape
- Browser Architecture Overview

Syarat Sebelum Naik Level:

- Dapat menjelaskan 4 layer arsitektur tanpa tercampur

---

## L1 - Runtime Model

Tujuan Level:
Memahami cara browser menjalankan script dan menjadwalkan pekerjaan.

Yang Harus Bisa Setelah Selesai:

- Menjelaskan urutan task -> microtask -> rendering opportunity
- Menjelaskan run-to-completion
- Menjelaskan hubungan Promise jobs dengan host microtask checkpoint

Topik Wajib:

- Event Loop
- Tasks vs Microtasks
- Rendering Opportunity
- Document Lifecycle Basics
- Concurrency Model Basics
- Memory Lifetime Basics

Syarat Sebelum Naik Level:

- Bisa memprediksi urutan eksekusi contoh async sederhana secara benar

---

## L2 - Core APIs

Tujuan Level:
Memahami capability inti Web Platform pada level API.

Yang Harus Bisa Setelah Selesai:

- Menjelaskan kontrak dasar DOM, Event, Timers, Fetch, Storage, URL/History, Workers
- Menjelaskan interaksi API dengan model runtime L1

Topik Wajib:

- DOM
- Event System
- Timers
- Fetch
- URL and History
- Storage
- Web Workers

Syarat Sebelum Naik Level:

- Dapat memetakan tiap API ke spec utama dan implikasi runtime dasarnya

---

## L3 - Performance and Security

Tujuan Level:
Memahami constraint performa dan batas keamanan browser.

Yang Harus Bisa Setelah Selesai:

- Menganalisis penyebab jank dari sudut scheduling dan rendering
- Menjelaskan SOP, CORS, Secure Context, dan isolation boundaries

Topik Wajib:

- Rendering Pipeline
- Long Tasks
- PerformanceObserver
- Same-Origin Policy
- CORS
- Secure Context
- Cross-Origin Isolation

Syarat Sebelum Naik Level:

- Mampu menjelaskan tradeoff performa-keamanan pada satu studi kasus

---

## L4 - Advanced Deep Dive

Tujuan Level:
Memahami perilaku sistem browser yang lebih kompleks dan lintas komponen.

Yang Harus Bisa Setelah Selesai:

- Menjelaskan lifecycle lanjutan dan interaksi antar subsistem
- Menjelaskan dampak desain arsitektur browser terhadap perilaku aplikasi

Topik Wajib:

- Streams Deep Dive
- Service Worker Lifecycle
- Browser Process Model Deep Dive
- IndexedDB Transaction Model
- bfcache and Lifecycle Interaction

Syarat Sebelum Naik Level:

- Dapat menjelaskan minimal satu skenario kompleks end-to-end secara runtut

---

## L5 - Watchlist and Experimental

Tujuan Level:
Mengikuti fitur baru tanpa mencampur fitur stabil dan eksperimental.

Yang Harus Bisa Setelah Selesai:

- Membedakan stable vs experimental status
- Menilai readiness fitur sebelum adopsi

Topik Wajib:

- API proposal dan fitur experimental yang relevan

Syarat Sebelum Naik Level:

- Mampu menulis risk note adopsi fitur eksperimental

---

## L6 - Applied Systems

Tujuan Level:
Menerapkan konsep lintas level untuk debugging kasus nyata.

Yang Harus Bisa Setelah Selesai:

- Melacak bottleneck runtime lintas API
- Menyusun hipotesis akar masalah berbasis observasi

Topik Wajib:

- Cross-API debugging playbook
- Race condition diagnosis
- Scheduling and rendering bottleneck analysis

Syarat Sebelum Naik Level:

- Mampu menyelesaikan studi kasus debugging dengan evidence teknis

---

## L7 - Architecture Decisions

Tujuan Level:
Mengambil keputusan desain sistem berbasis tradeoff nyata.

Yang Harus Bisa Setelah Selesai:

- Memilih pola arsitektur yang sesuai konteks
- Menjelaskan konsekuensi keputusan terhadap performa, keamanan, dan maintainability

Topik Wajib:

- Worker vs Main Thread strategy
- Cache and invalidation architecture
- Security hardening decisions

Syarat Sebelum Naik Level:

- Dapat menulis decision record dengan alternatif dan justifikasi

---

## L8 - Spec Reading and Validation

Tujuan Level:
Mampu membaca specification primer dan memvalidasi asumsi implementasi.

Yang Harus Bisa Setelah Selesai:

- Menemukan bagian algoritma normatif yang relevan
- Memetakan teks specification ke perilaku runtime

Topik Wajib:

- Spec reading workflow
- Normative algorithm tracing
- Interop and conformance validation

Syarat Sebelum Naik Level:

- Mampu memvalidasi satu perilaku browser langsung dari specification

---

## L9 - Senior Engineering

Tujuan Level:
Mengembangkan kemampuan analisis dan komunikasi teknis level senior.

Yang Harus Bisa Setelah Selesai:

- Melakukan design review berbasis risiko
- Menyusun incident analysis yang actionable
- Menetapkan optimization plan berbasis data

Topik Wajib:

- Design review framework
- Incident analysis framework
- Performance and reliability planning

Syarat Sebelum Naik Level:

- Mampu menghasilkan review/analysis yang dapat dipakai tim lain

---

## L10 - Expert and Maintainer

Tujuan Level:
Menjadi penjaga kualitas sistem pengetahuan dan standar teknis.

Yang Harus Bisa Setelah Selesai:

- Menetapkan governance konten dan quality gate
- Mengkurasi roadmap pembelajaran lintas level
- Menjaga konsistensi terminologi dan akurasi spec-aligned

Topik Wajib:

- Knowledge governance
- Curriculum maintenance
- Review and mentoring standards

Syarat Kelulusan Akhir:

- Mampu menjaga mutu kurikulum end-to-end secara berkelanjutan
