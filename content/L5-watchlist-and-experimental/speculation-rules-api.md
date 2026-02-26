# Speculation Rules API

- Level: L5
- Status: Experimental
- Depth: watchlist
- Specs:
  - Speculation Rules API context
- Prerequisites: View Transitions API
- Next Topics: File System Access API

---

## 1. Official Term

Speculation Rules API

## 2. Formal Definition

Speculation Rules API memungkinkan halaman mendeklarasikan
kandidat URL untuk prefetch atau prerender
melalui aturan terstruktur berbasis JSON.

## 3. Mental Model

Aplikasi memberi "petunjuk prediksi navigasi" ke browser,
agar browser menyiapkan resource lebih awal untuk transisi lebih cepat.

### Wireframe Ringkas

```text
[Current Page]
   -> speculation rules
   -> prefetch/prerender candidates
   -> faster future navigation (if prediction hits)
```

## 4. Runtime Perspective

- Thread/process: evaluasi aturan dilakukan oleh subsistem navigasi/network browser.
- Queue model: aktivitas prefetch/prerender berjalan async di luar alur interaksi utama.
- Scheduling: browser memutuskan kapan mengeksekusi spekulasi berdasarkan resource budget.
- Rendering interaction: prerender yang berhasil dapat mengurangi waktu render saat navigasi aktual.
- Dampak performa: hit rate tinggi mempercepat navigasi; hit rate rendah menambah biaya network.
- Dampak memori: prerender dapat menambah konsumsi memori sementara.
- Dampak keamanan: browser menerapkan batas policy agar spekulasi tetap aman dan terkontrol.

## 5. Why This Exists

Agar aplikasi bisa mengoptimalkan navigasi antarpages
secara proaktif dengan sinyal terstruktur ke browser.

## 6. Minimal Code Example

```html
<script type="speculationrules">
{
  "prefetch": [{ "source": "list", "urls": ["/next-page"] }]
}
</script>
```

## 7. Common Misconceptions

- "Semua prefetch pasti dipakai"
  - Koreksi: spekulasi bersifat probabilistik, bisa tidak terpakai.
- "Prerender selalu aman untuk semua halaman"
  - Koreksi: ada syarat kompatibilitas dan policy yang harus dipenuhi.

## 8. Pitfalls and Best Practices

- Pitfall: menambahkan terlalu banyak kandidat tanpa prioritas.
- Pitfall: tidak memonitor hit/miss terhadap biaya network.
- Best practice: mulai dari kandidat bernilai tinggi dan ukur dampaknya.

## 9. Prerequisites

- [Navigation API](./navigation-api.md)
- [URL and History](../L2-core-apis/url-and-history.md)

## 10. Next Topics

- [File System Access API](./file-system-access-api.md)
