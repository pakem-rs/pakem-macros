# 🔮 Pakem Macros (`pakem_macros`)

> **"Look like Laravel, Run at Rust Speed."**  
> *Procedural macros powering Pakem Framework — Model ORM derivation, active record methods, declarative form validation, and routing.*

[![Crates.io](https://img.shields.io/crates/v/pakem_macros.svg)](https://crates.io/crates/pakem_macros)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Rust 2024](https://img.shields.io/badge/Rust-2024_Edition-orange.svg)](https://www.rust-lang.org)
[![Pakem Framework](https://img.shields.io/badge/ecosystem-Pakem%20Framework-purple.svg)](https://github.com/pakem-rs/framework)

---

## 🌟 Fitur Utama

`pakem_macros` menyediakan makro prosedural (*procedural macros*) yang membebaskan pengembang dari penulisan kode repetitif (*boilerplate*):

1. **`#[derive(PakemModel)]`**:
   - Membangkitkan implementasi trait `Model` secara otomatis.
   - Menyediakan fungsi CRUD statis dan instance: `find()`, `all()`, `create()`, `save()`, `delete()`, `paginate()`.
   - Menghubungkan model ke **Fluent Query Builder** (`User::query(db)`).
   - Mendukung kustomisasi tabel (`#[table("nama_tabel")]`), primary key kustom (`#[primary_key("id")]`), dan relasi deklaratif `has_many!`, `belongs_to!`, `belongs_to_many!`.

2. **`#[pakem_form]`**:
   - Validasi form deklaratif dengan sintaks yang ekspresif ala Laravel: `#[rule("required|email|min:3|max:50")]`.
   - Mengubah aturan teks secara otomatis menjadi validator bawaan tanpa konfigurasi manual yang berbelit-belit.

---

## 📦 Instalasi

Tambahkan dependensi ke berkas `Cargo.toml` Anda:

```toml
[dependencies]
pakem_macros = "1.0.5"
```

*(Catatan: Jika Anda menggunakan `pakem` atau `pakem-framework`, makro ini sudah diekspor ulang secara otomatis melalui `pakem::prelude::*`)*.

---

## 🚀 Panduan Penggunaan

### 1. Derive Model ORM (`#[derive(PakemModel)]`)

Cukup tambahkan derive pada struct entitas Anda:

```rust
use pakem::prelude::*;
use serde::{Deserialize, Serialize};
use sqlx::FromRow;

#[derive(Debug, Serialize, Deserialize, FromRow, Clone, Default, PakemModel)]
#[table("users")]
pub struct User {
    pub id: i64,
    pub name: String,
    pub email: String,
    pub created_at: Option<String>,
    pub updated_at: Option<String>,
}
```

Setelah didefinisikan, struct otomatis memiliki metode ekspresif:
```rust
// 1. Ambil data berdasarkan ID
let user = User::find(req.db(), 1).await?;

// 2. Query builder chaining
let active_users = User::query(req.db())
    .where_eq("email", "john@example.com")
    .order_by("name", "ASC")
    .get()
    .await?;

// 3. Paginasi otomatis
let paginator = User::paginate(req.db(), page, per_page).await?;
```

---

### 2. Validasi Form Deklaratif (`#[pakem_form]`)

Definisikan form input web atau REST API dengan aturan validasi deklaratif:

```rust
use pakem_macros::pakem_form;

#[pakem_form]
pub struct RegisterForm {
    #[rule("required|min:3|max:50")]
    pub name: String,

    #[rule("required|email")]
    pub email: String,

    #[rule("required|min:8")]
    pub password: String,
}
```

Aturan yang didukung:
- `required` — Field wajib diisi dan tidak boleh kosong.
- `email` — Format alamat surel yang valid.
- `url` — Format URL yang valid.
- `min:X` — Panjang karakter minimal `X`.
- `max:X` — Panjang karakter maksimal `X`.

---

## 🤝 Berkontribusi (Contributing)

Kontribusi dari komunitas sangat dinantikan!
1. Fork repositori ini.
2. Buat branch fitur (`git checkout -b feature/nama-fitur`).
3. Jalankan pengujian (`cargo check`).
4. Commit perubahan Anda (`git commit -m 'feat: tambah fitur macro baru'`).
5. Push ke branch Anda (`git push origin feature/nama-fitur`).
6. Buka **Pull Request**.

---

## 📜 Lisensi

Pakem Macros dirilis di bawah lisensi terbuka [MIT License](LICENSE).  
Dikelola oleh tim pengembang [Pakem Framework](https://github.com/pakem-rs/framework).
