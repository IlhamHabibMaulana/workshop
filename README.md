# Workshop: Pengembangan Aplikasi To-Do List Berbasis Web
Repositori ini berisi seluruh dokumen spesifikasi teknis, rancangan UI/UX, aturan keamanan, skrip database Supabase, dan implementasi kode Single Page Application (SPA) berbasis **Tailwind CSS** dan **Supabase**.

---

## 📁 Struktur Berkas Repositori

```text
├── PRD.md                 # Product Requirements Document (Identitas, CRUD, Skema Data & Kontrak QA)
├── STITCH_PROMPT.md       # Prompt Desain UI/UX Siap Pakai untuk Google Stitch
├── DESIGN.md              # Design System, Palet Warna Tailwind & Pedoman Komponen
├── RULES.md               # AI Coding & Security Guardrails (Anti-XSS & Kredensial)
├── supabase_schema.sql    # Skrip PostgreSQL Supabase (Tabel tasks, RLS, CHECK & Dummy Data)
├── index.html             # Implementasi Lengkap Web Application (Tailwind + Supabase JS)
└── README.md              # Dokumentasi & Petunjuk Penggunaan
```

---

## 🚀 Panduan Memulai Cepat

### 1. Setup Skema Database di Supabase
1. Buka [Supabase Dashboard](https://supabase.com/dashboard).
2. Buat proyek baru atau pilih proyek yang sudah ada.
3. Masuk ke menu **SQL Editor**, buka berkus [`supabase_schema.sql`](supabase_schema.sql), lalu salin seluruh kodenya dan klik **Run**.
4. Skrip ini akan membuat:
   - Tabel `public.tasks` dengan validasi constraint `CHECK`.
   - Mengaktifkan Row Level Security (RLS) dengan policy publik untuk demo.
   - Mengisi 3 data tugas awal secara otomatis.

### 2. Konfigurasi Kredensial Frontend
Buka file [`index.html`](index.html), cari baris konfigurasi Supabase (sekitar baris 250):
```javascript
const SUPABASE_URL = "https://your-project-id.supabase.co";
const SUPABASE_ANON_KEY = "your-public-anon-key";
```
*Ganti dengan URL dan Anon Key publik dari menu Project Settings > API di Supabase.*
*(Catatan: Aplikasi tetap dapat berjalan dalam mode demo interaktif lokal / localStorage jika URL dikosongkan).*

### 3. Menjalankan Aplikasi
Cukup buka berkas `index.html` langsung menggunakan web browser apa pun (Google Chrome, Edge, Safari, Firefox), atau gunakan ekstensi **Live Server** di VS Code.

---

## 🛡️ Kepatuhan Standar Uji & Keamanan (Modul 5 SKPL)
* **TC-01 (Toggle Status Tugas):** Klik checkbox pada baris tabel mengubah status `Pending` ↔ `Completed` seketika.
* **TC-02 (Validasi Form Kosong):** Menolak penyimpanan saat field Judul kosong dan memunculkan peringatan *"Judul tugas tidak boleh kosong!"*.
* **SEC-01 (Anti-XSS Protection):** Seluruh input dirender aman menggunakan `.textContent` / sanitasi entitas HTML (`escapeHtml`).
* **SEC-02 (Credential Audit):** Tidak ada secret service key yang terekspos di sisi klien.
