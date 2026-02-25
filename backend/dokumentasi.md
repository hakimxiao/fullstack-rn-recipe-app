# 🌧️ Drizzle ORM — Panduan Setup

> ORM ringan & type-safe untuk database relasional di Node.js / TypeScript.

---

## 📋 Langkah-langkah Penggunaan

### 1. 📁 Buat Folder & File Schema

Buat struktur folder berikut di dalam project kamu:

```
src/
└── db/
    └── schema.js
```

---

### 2. 📦 Import dari Provider

Import Drizzle dari provider database yang kamu gunakan, lalu extract method yang dibutuhkan (lihat dokumentasi resmi untuk detail lengkap).

**Contoh untuk Neon (PostgreSQL):**

```js
import { drizzle } from "drizzle-orm/neon-http";
import * as schema from "../db/schema.js";
```

---

### 3. ⚙️ Buat File Konfigurasi DB

Setelah membuat instance database, ekspor koneksi `db` seperti berikut:

```js
export const db = drizzle(sql, { schema });
```

---

### 4. 🗂️ Buat `drizzle.config.js` di Root Project

Buat file `drizzle.config.js` di **root level** project kamu dengan isi berikut:

```js
export default {
  schema: "./src/db/schema.js", // Lokasi schema yang dibuat di langkah 1
  out: "./src/db/migrations", // Output hasil migrasi oleh Drizzle
  dialect: "postgresql", // Sesuaikan dengan provider yang dipakai
  dbCredentials: {
    url: ENV.DATABASE_URL, // Neon membutuhkan URL koneksi
  },
};
```

| Key                 | Keterangan                                       |
| ------------------- | ------------------------------------------------ |
| `schema`            | Path ke file schema yang dibuat di langkah 1     |
| `out`               | Folder output hasil generate migrasi             |
| `dialect`           | Jenis database (`postgresql`, `mysql`, `sqlite`) |
| `dbCredentials.url` | URL koneksi database (dari environment variable) |

---

### 5. 🚀 Jalankan Migrasi ke Cloud

Setelah model selesai dibuat di lokal, jalankan perintah berikut untuk memigrasikan schema ke database cloud:

```bash
npx drizzle-kit migrate
```

---

## 🔄 Alur Singkat

```
schema.js  →  drizzle.config.js  →  drizzle-kit migrate  →  ☁️ Database Cloud
```

---

> 💡 **Tips:** Pastikan `DATABASE_URL` sudah diset di file `.env` sebelum menjalankan migrasi.
