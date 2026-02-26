# Panduan Wireframe

Dokumen ini memberi wireframe teks (ASCII) agar penjelasan lebih mudah dipahami sebelum masuk detail teknis.
Gunakan wireframe sebagai peta visual ringkas, bukan pengganti penjelasan formal.

---

## 1. Wireframe Kurikulum V2

```text
[README]
  |
  +--> [LEVELS L0-L10]
  |       |
  |       +--> Foundation:   L0 -> L1 -> L2 -> L3 -> L4 -> L5
  |       +--> Professional: L6 -> L7 -> L8
  |       +--> Senior:       L9 -> L10
  |
  +--> [PATHS]
          |
          +--> Jalur Wajib Fondasi
          +--> Jalur Professional Systems
          +--> Jalur Senior Track
```

Tujuan:

- Memperlihatkan arah belajar secara cepat
- Membantu menentukan posisi level saat ini

---

## 2. Wireframe Halaman Topik

```text
+--------------------------------------------------+
| Metadata: Level | Status | Specs | Prerequisites |
+--------------------------------------------------+
| 1. Official Term                                 |
| 2. Formal Definition                             |
| 3. Mental Model                                  |
|    - Wireframe Ringkas (ASCII)                  |
| 4. Runtime Perspective                           |
| 5. Why This Exists                               |
| 6. Minimal Code Example                          |
| 7. Common Misconceptions                         |
| 8. Pitfalls and Best Practices                   |
| 9. Prerequisites                                 |
|10. Next Topics                                   |
+--------------------------------------------------+
```

Tujuan:

- Menunjukkan struktur penjelasan topik secara konsisten
- Memudahkan pembaca memahami alur sebelum membaca detail

---

## 3. Aturan Pemakaian Wireframe

- Wireframe harus singkat dan fokus pada hubungan komponen.
- Gunakan ASCII agar kompatibel di markdown tanpa alat tambahan.
- Letakkan wireframe di bagian `Mental Model` pada subbagian `Wireframe Ringkas`.
- Hindari wireframe terlalu detail hingga menutupi tujuan pembelajaran.

---

## 4. Contoh Singkat (Event Loop)

```text
[Task Queue] -> (pick 1 task) -> [Run Script]
                               -> [Microtask Checkpoint]
                               -> [Render Opportunity]
                               -> (repeat)
```

Penjelasan satu baris:
Satu iterasi loop memproses task, mengosongkan microtask, lalu memberi peluang rendering.
