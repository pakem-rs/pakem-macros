# 📝 Changelog — `pakem-macros`

Semua perubahan penting pada procedural macro suite **Pakem Macros** (`pakem-macros`) didokumentasikan di dalam berkas ini.

Format pencatatan mengacu pada [Keep a Changelog](https://keepachangelog.com/en/1.0.0/) dan mengikuti standar [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [1.0.5] - 2026-11-27

### 🐛 Perbaikan Bug & Keandalan Macro
- **Akurasi `Model::delete()` & `destroy()`**: Mengembalikan `Ok(res.rows_affected() > 0)` alih-alih selalu `Ok(true)` saat baris tidak ditemukan.
- **Tanpa Pemotongan Teks (`LEFT(..., 16383)`)**: Menghapus pemotongan otomatis 16.383 karakter pada kolom teks panjang (`content`, `body`, `description`, `message`, dsb.) agar data utuh.

### 🦀 Rust 2024 Edition Compatibility & Package Rename
- **Konsistensi Nama Crate (`pakem-derive`)**: Mengganti nama package crates.io menjadi `pakem-derive` agar seluruh ekosistem konsisten memakai tanda hubung (`-`).
- Migrasi manifest ke Rust 2024 Edition (`edition = "2024"`).
- Pembaruan dependensi `syn` (v2/v3), `quote`, dan `proc-macro2`.
- Dukungan macro derive `PakemModel` untuk integrasi ORM mutakhir.
