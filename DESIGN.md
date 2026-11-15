# DESIGN SYSTEM & UI GUIDELINES
## TaskFlow — Pengelola Tugas (Dark Palette — Sesuai Desain Figma)

Dokumen ini mendokumentasikan sistem desain, token visual, palet warna, tipografi, dan panduan komponen yang diekstrak langsung dari desain resmi Figma **TaskFlow** (`UbROgniYvDs6tJnkwEC93E`).

---

### 1. Palet Warna (TaskFlow Dark Theme Tokens)

Desain menggunakan tema gelap modern (*Deep Slate & Navy*) dengan aksen *Warm Amber / Gold* dan *Emerald Green* yang kontras dan nyaman di mata:

| Token Desain | Kode Hex / Nilai | Penerapan pada Antarmuka |
| :--- | :--- | :--- |
| **Canvas Background** | `#0D1320` (`bg-[#0d1320]`) | Latar belakang seluruh halaman web utama. |
| **Sidebar Surface** | `#161B29` (`bg-[#161b29]`) | Latar belakang panel navigasi samping (aside). |
| **Card / Bento Surface** | `#1A1F2D` (`bg-[#1a1f2d]`) | Kontainer 4 kartu metrik (KPI), kartu tugas, dan tombol filter. |
| **Input / Outer Bar** | `#242A38` (`bg-[#242a38]`) | Bar pembungkus *quick add task*, border subtil, dan badge tag default. |
| **Input Inner Surface** | `rgba(8,14,27,0.8)` | Kolom isian teks judul tugas pada form cepat. |
| **Primary Brand / Amber** | `#F59E0B` (`bg-[#f59e0b]`) | Tombol aksi utama (+TAMBAH), checkbox aktif, dan tombol header. |
| **Amber Text / Highlight** | `#FFC174` (`text-[#ffc174]`) | Teks heading logo, counter pending, dan aksen progress bar. |
| **Amber Button Text** | `#472A00` (`text-[#472a00]`) | Teks kontras tinggi di atas tombol amber `#F59E0B`. |
| **Text Primary** | `#DDE2F5` (`text-[#dde2f5]`) | Judul halaman "Daftar Tugas Saya", angka KPI total, dan teks judul aktif. |
| **Text Secondary / Muted** | `#D8C3AD` (`text-[#d8c3ad]`) | Label uppercase KPI, teks subjudul, tanggal, dan placeholder form. |
| **Success / Completed** | `#4EDEA3` | Angka KPI tuntas, badge "Selesai" (`bg-[rgba(0,165,114,0.2)]`), progress bar hijau. |
| **Warning / Pending** | `#FFB95F` | Badge "Menunggu / Tertunda" (`bg-[rgba(245,158,11,0.2)]`). |
| **Urgent Alert** | `#FFB4AB` (`text-[#ffb4ab]`) | Metrik tenggat hari ini dan teks perhatian. |
| **Danger / Delete Action** | `#FFB4AB` / `#690005` | Tombol Hapus (`bg-[#ffb4ab] text-[#690005] hover:bg-[#ff897d]`). |

---

### 2. Tipografi & Tata Letak

1. **Font Family:**
   * Teks & Heading: `Plus Jakarta Sans` dan `Inter` (sans-serif).
   * Konfigurasi CDN Google Fonts:
     ```html
     <link rel="preconnect" href="https://fonts.googleapis.com">
     <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
     <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=Plus+Jakarta+Sans:wght@500;600;700;800&display=swap" rel="stylesheet">
     ```
2. **Hierarki Visual:**
   * **Page Title:** `text-[32px] font-bold text-[#dde2f5] tracking-tight`
   * **Bento Metric Counter:** `text-[32px] font-bold` (Total: `#dde2f5`, Pending: `#ffc174`, Selesai: `#4edea3`)
   * **Card Title:** `text-[16px] font-semibold text-[#dde2f5]` (Completed: `line-through text-[#d8c3ad]/60`)
   * **Card Description:** `text-[12px] text-[#d8c3ad]/70`
   * **Badge & Micro-copy:** `text-[11px] font-semibold tracking-wider uppercase`

---

### 3. Komponen Khusus Sesuai Figma

#### A. 4 Bento Metric Widgets
1. **Total Beban Tugas:** Counter besar putih kebiruan, teks `Semua kategori`, garis bar kuning.
2. **Perlu Tindakan (Pending):** Counter kuning emas, teks `Prioritas aktif`, garis bar oranye.
3. **Tuntas Diselesaikan:** Counter hijau emerald, teks persentase tercapai, garis bar hijau.
4. **Tenggat Hari Ini:** Counter warna salmon merah muda (`#ffb4ab`), nama tugas darurat terdekat, disertai ikon radial gauge.

#### B. Quick In-Place Add Task Bar
Bar horizontal ramping dengan efek glassmorphism gelap:
* Ikon list / task di sebelah kiri.
* Input judul berlatar gelap transparan (`rgba(8,14,27,0.8)`).
* Pemilih tanggal deadline ringkas.
* Tombol aksi `+ TAMBAH` berwarna Amber tegas dengan teks gelap.

#### C. Custom Checkbox Aksi Cepat (`TC-01`)
* **State Pending:** Kotak persegi `border border-[#d8c3ad]/40 bg-[#1a1f2d] hover:border-[#f59e0b]`.
* **State Completed:** Kotak persegi terisi penuh warna Amber `#f59e0b` dengan ikon centang putih/gelap dan efek transisi lembut.

#### D. Alert Banner Validasi (`TC-02`)
* Kotak peringatan bergaya dark-theme `bg-rose-950/80 border border-rose-500/50 text-rose-200` dengan pesan mutlak: *"Judul tugas tidak boleh kosong!"*.
