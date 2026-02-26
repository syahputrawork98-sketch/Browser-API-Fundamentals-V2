# Changelog Archives

Folder ini menyimpan arsip changelog lama agar `CHANGELOG.md` utama tetap ringkas.

## Aturan Rotasi

- `CHANGELOG.md` utama menyimpan versi terbaru (rolling window).
- Jika baris melebihi sekitar 120-150 baris, pindahkan versi paling lama ke arsip baru.
- Nama file arsip mengikuti rentang versi, contoh:
  - `CHANGELOG-archive-v0.1.0-to-v0.3.1.md`
  - `CHANGELOG-archive-v0.4.0-to-v0.6.0.md`
- Isi historis tidak diubah, hanya dipindahkan.

## Arsip Tersedia

- [v0.1.0 to v0.3.1](./CHANGELOG-archive-v0.1.0-to-v0.3.1.md)
- [v0.4.0 to v0.6.0](./CHANGELOG-archive-v0.4.0-to-v0.6.0.md)
