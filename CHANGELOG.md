# 📝 Changelog — `pakem-macros`

Semua perubahan penting pada procedural macro suite **Pakem Macros** (`pakem-macros`) didokumentasikan di dalam berkas ini.

Format pencatatan mengacu pada [Keep a Changelog](https://keepachangelog.com/en/1.0.0/) dan mengikuti standar [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [1.0.5] - 2026-11-27

### 🦀 Rust 2024 Edition Compatibility & Package Rename
- Penggantian nama package crates.io dari `pakem_macros` menjadi `pakem-macros` agar konsisten menggunakan tanda hubung (`-`) seperti crate ekosistem Pakem lainnya (`pakem-blade`, `pakem-live`, `indonesian-script`).
- Migrasi manifest ke Rust 2024 Edition (`edition = "2024"`).
- Pembaruan dependensi `syn` (v2/v3), `quote`, dan `proc-macro2`.
- Dukungan macro derive `PakemModel` untuk integrasi ORM mutakhir.
