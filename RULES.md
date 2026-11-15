# AI CODING & SECURITY GUARDRAILS
## Aturan Wajib Pengembangan Aplikasi To-Do List

Dokumen ini berisi instruksi dan hukum mutlak yang mengikat seluruh asisten AI maupun developer dalam menulis atau memperbarui kode program pada repositori ini.

---

### RULE 1: Kepatuhan Skema & Spesifikasi SKPL
1. Nama tabel database wajib tepat: `tasks`.
2. Nama field/kolom wajib 100% identik (huruf kecil, tanpa singkatan aneh):
   * `id`
   * `judul`
   * `deskripsi`
   * `deadline`
   * `status`
3. Nilai enum status hanya boleh berisi: `'Pending'` atau `'Completed'`.
4. Pesan peringatan kesalahan validasi wajib sama persis dengan yang disyaratkan SKPL:
   * **"Judul tugas tidak boleh kosong!"**

---

### RULE 2: Proteksi Mutlak Terhadap Serangan XSS (`SEC-01`)
1. **DILARANG KERAS** menggunakan manipulasi DOM berbasis string yang rentan terhadap eksekusi kode berbahaya, seperti:
   * ❌ `element.innerHTML = ...`
   * ❌ `element.outerHTML = ...`
   * ❌ `document.write(...)`
   * ❌ Atribut inline JavaScript seperti `onclick="hapus('${tugas.id}')"` yang merender data mentah.
2. **WAJIB** menerapkan salah satu dari dua pendekatan keamanan berikut saat merender data dinamis dari pengguna atau Supabase:
   * **Pendekatan A (Direkomendasikan):** Buat elemen menggunakan `document.createElement()` dan masukkan nilai teks menggunakan property `.textContent`:
     ```javascript
     const tdJudul = document.createElement('td');
     tdJudul.textContent = tugas.judul; // Aman dari injeksi XSS
     ```
   * **Pendekatan B:** Jika menggunakan template literals untuk penyusunan elemen terstruktur, seluruh variabel string dari database/input WAJIB disaring melalui fungsi sanitasi `escapeHtml()`:
     ```javascript
     function escapeHtml(str) {
       if (str === null || str === undefined) return '';
       return String(str)
         .replace(/&/g, '&amp;')
         .replace(/</g, '&lt;')
         .replace(/>/g, '&gt;')
         .replace(/"/g, '&quot;')
         .replace(/'/g, '&#039;');
     }
     ```
3. **Uji Validasi:** Pengujian menggunakan payload `<img src=x onerror=alert(1)>` wajib menghasilkan karakter teks statis yang aman di browser tanpa pernah memunculkan window alert.

---

### RULE 3: Validasi Logika Berlapis Sisi Klien (`TC-01` & `TC-02`)
1. **Tidak Bergantung Pada Atribut HTML Saja:** Jangan hanya mengandalkan atribut HTML5 `required` atau `maxlength` pada input, karena atribut tersebut sangat mudah dihapus oleh pengguna melalui fitur *Inspect Element* browser.
2. **Validasi JavaScript Sebelum Request API:**
   * Di dalam fungsi event listener submit formulir, lakukan verifikasi pembersihan spasi (*trimming*):
     ```javascript
     const inputJudul = document.getElementById('input-judul').value.trim();
     if (!inputJudul || inputJudul === "") {
       // Hentikan proses simpan
       showErrorAlert("Judul tugas tidak boleh kosong!");
       return;
     }
     ```
   * Jika validasi gagal, panggilan fungsi Supabase (`supabase.from('tasks').insert(...)`) **DILARANG** dieksekusi.
3. **Akurasi Quick Toggle (`TC-01`):**
   * Event handler pada checkbox baris tabel harus langsung memperbarui field `status` di tabel `tasks` (`Pending` ↔ `Completed`).
   * UI harus memberikan umpan balik instan (*optimistic UI update* atau *immediate reload*) tanpa memicu reload satu halaman penuh (*full page reload*).

---

### RULE 4: Manajemen Kredensial & Batasan Keamanan (`SEC-02`)
1. **Kunci yang Diizinkan di Sisi Klien:**
   * Hanya variabel `SUPABASE_URL` dan `SUPABASE_ANON_KEY` (Public Anonymous Key) yang boleh dicantumkan pada kode frontend (`index.html` / `app.js`).
2. **Kunci Terlarang:**
   * **DILARANG KERAS** menuliskan, menyimpan, maupun menyinggung `SUPABASE_SERVICE_ROLE_KEY` atau `STITCH_API_KEY` di dalam kode frontend.
   * Service Role Key memiliki hak bypass RLS (*Row Level Security*) penuh dan dapat menghancurkan seluruh database jika terekspos ke browser publik.
3. Seluruh pembatasan akses dan integritas data dibebankan kepada kebijakan **Row Level Security (RLS)** dan database `CHECK` constraints di level Supabase PostgreSQL.
