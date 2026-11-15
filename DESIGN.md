# DESIGN SYSTEM & UI GUIDELINES
## Aplikasi To-Do List

Dokumen ini merupakan panduan standar visual, tata letak, dan interaksi yang wajib dipatuhi oleh pengembang maupun asisten AI dalam mengimplementasikan antarmuka web.

---

### 1. Palet Warna (Tailwind CSS Tokens)

Aplikasi dibangun menggunakan skema warna netral modern dengan penekanan fungsional (*semantic color coding*) untuk membedakan status dan aksi:

| Kategori | Token Tailwind | Kode Hex | Penggunaan UI |
| :--- | :--- | :--- | :--- |
| **Canvas Background** | `bg-slate-50` | `#F8FAFC` | Latar belakang seluruh halaman aplikasi. |
| **Card / Surface** | `bg-white` | `#FFFFFF` | Latar belakang kontainer kartu, panel form, dan tabel data. |
| **Border / Divider** | `border-slate-200` | `#E2E8F0` | Garis batas antar komponen, border kartu, dan pemisah baris tabel. |
| **Text Primary** | `text-slate-900` | `#0F172A` | Judul utama, heading, dan teks prioritas tertinggi. |
| **Text Secondary** | `text-slate-500` | `#64748B` | Label form, placeholder, subjudul, dan metadata (tanggal). |
| **Primary Brand** | `bg-indigo-600`, `hover:bg-indigo-700` | `#4F46E5` | Tombol simpan data, focus ring formulir, dan indikator aktif. |
| **Success / Completed** | `bg-emerald-600`, `text-emerald-700`, `bg-emerald-50` | `#059669` | Badge status `Completed`, kartu KPI tugas selesai, checkbox checked. |
| **Pending / Warning** | `bg-amber-500`, `text-amber-700`, `bg-amber-50` | `#F59E0B` | Badge status `Pending`, kartu KPI tugas tertunda. |
| **Danger / Error** | `bg-rose-600`, `text-rose-700`, `bg-rose-50` | `#E11D48` | Tombol hapus data, banner alert kegagalan validasi (`TC-02`). |

---

### 2. Tipografi & Tata Cara Penulisan

1. **Font Family:**
   * Font utama: `Inter`, `Plus Jakarta Sans`, atau fallback sans-serif sistem (`font-sans`).
   * Konfigurasi CDN Google Fonts:
     ```html
     <link rel="preconnect" href="https://fonts.googleapis.com">
     <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
     <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700&display=swap" rel="stylesheet">
     ```
2. **Hierarki Teks:**
   * **App Heading:** `text-2xl font-bold tracking-tight text-slate-900`
   * **Section / Card Heading:** `text-base font-semibold text-slate-800`
   * **KPI Numbers:** `text-3xl font-extrabold text-slate-900`
   * **Table Body / Form Text:** `text-sm font-normal text-slate-700`
   * **Micro-copy & Timestamps:** `text-xs font-medium text-slate-400`
3. **Standar Lokalisasi Indonesia (`id-ID`):**
   * Format penulisan tanggal wajib menggunakan standar Indonesia: `18 November 2026` atau format ringkas `18 Nov 2026`.
   * Implementasi JavaScript:
     ```javascript
     function formatIndonesianDate(dateString) {
       if (!dateString) return "-";
       const date = new Date(dateString);
       return new Intl.DateTimeFormat('id-ID', {
         day: 'numeric',
         month: 'short',
         year: 'numeric'
       }).format(date);
     }
     ```

---

### 3. Aturan Komponen Interaktif

#### A. Status Tombol & Loading State
* Tombol aksi tidak boleh dibiarkan tanpa respon saat proses asynchronous berlangsung (misal: saat menyimpan ke Supabase).
* Tombol wajib dinonaktifkan (`disabled`) dan menampilkan indikator loading (*spinner*) agar pengguna tidak melakukan *double submit*:
  ```html
  <button id="btn-submit" type="submit" class="inline-flex items-center justify-center px-4 py-2.5 bg-indigo-600 hover:bg-indigo-700 text-white font-medium text-sm rounded-lg transition-colors shadow-sm disabled:opacity-60 disabled:cursor-not-allowed">
    <svg id="submit-spinner" class="animate-spin -ml-1 mr-2 h-4 w-4 text-white hidden" fill="none" viewBox="0 0 24 24">
      <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
      <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8v8H4z"></path>
    </svg>
    <span id="submit-label">Simpan Tugas</span>
  </button>
  ```

#### B. Alert Banner Kegagalan Validasi (`TC-02`)
* Jika pengguna mengosongkan judul tugas, tampilkan kotak peringatan merah di atas formulir dengan animasi transisi yang jelas:
  ```html
  <div id="alert-error" class="hidden mb-4 p-3.5 bg-rose-50 border border-rose-200 rounded-lg flex items-start gap-3 text-rose-800 text-sm animate-fade-in" role="alert">
    <svg class="w-5 h-5 text-rose-500 shrink-0 mt-0.5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4m0 4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
    </svg>
    <div>
      <p class="font-semibold text-rose-900">Validasi Gagal</p>
      <p id="alert-error-message" class="text-rose-700">Judul tugas tidak boleh kosong!</p>
    </div>
  </div>
  ```

#### C. Empty State (Tabel Kosong)
* Ketika data tugas masih kosong atau pencarian tidak menghasilkan rekaman, jangan tampilkan tabel kosong yang membingungkan. Tampilkan visual *empty state*:
  ```html
  <div id="empty-state" class="text-center py-12 px-4">
    <div class="w-12 h-12 rounded-full bg-slate-100 text-slate-400 mx-auto flex items-center justify-center mb-3">
      <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2" />
      </svg>
    </div>
    <h3 class="text-sm font-semibold text-slate-800">Tidak ada tugas ditemukan</h3>
    <p class="text-xs text-slate-500 mt-1">Mulai dengan menambahkan tugas baru melalui formulir.</p>
  </div>
  ```

#### D. Quick Toggle Transition (`TC-01`)
* Ketika status tugas diubah menjadi `'Completed'` melalui klik checkbox:
  * Teks judul tugas seketika diberi style: `line-through text-slate-400`.
  * Badge berubah warna dari amber ke emerald.
  * Kartu metrik di atas otomatis melakukan re-kalkulasi secara instan.
