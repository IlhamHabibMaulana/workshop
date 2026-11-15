# UI/UX Design Prompt for Google Stitch
## Target Platform: https://stitch.withgoogle.com/

Copy and paste the detailed prompt below directly into Google Stitch to generate the Tailwind CSS interface:

```text
Design a modern, ultra-clean, and responsive Web Task Management / To-Do List Dashboard using Tailwind CSS and Phosphor / Heroicons styling. The visual aesthetic should feel like a premium SaaS productivity tool (such as Linear or Notion) built on a light, distraction-free palette: Slate-50 background, pure white cards with subtle borders (border-slate-200), Indigo-600 primary accents, Emerald-600 success states, and Rose-600 danger alerts.

The interface must strictly incorporate the following components:

1. Top Navigation & Header Bar:
   - Application title: "Task Manager - Aplikasi To-Do List" with a sleek task-check logo icon.
   - Professional subtitle: "Kelola daftar tugas harian, tenggat waktu, dan pantau progres kerja Anda."
   - Right-side status pills: A dynamic indicator badge showing a pulsing green dot with text "Supabase Connected", alongside an Indonesian locale live date display ("id-ID").

2. Summary / KPI Metrics Section (3 Dynamic Cards Grid at the Top):
   - Card 1 (Total Tasks): Icon with a stack/clipboard symbol, label "Total Tugas", bold numeric counter (e.g. "12 Tugas"), with subtle slate badge "Semua data".
   - Card 2 (Completed Tasks): Icon with a check-circle symbol in emerald theme, label "Tugas Selesai", bold numeric counter (e.g. "8 Tugas"), badge with emerald text "Completed".
   - Card 3 (Pending Tasks): Icon with an hourglass/clock symbol in amber theme, label "Tugas Tertunda", bold numeric counter (e.g. "4 Tugas"), badge with amber text "Pending".

3. Main Interactive Two-Column Split Layout:
   - LEFT COLUMN (Form Input & Management - 4 or 5 cols on lg screen):
     * A structured white card titled "Formulir Tugas" with a dynamic badge indicating mode ("Tambah Tugas Baru" vs "Edit Tugas #ID").
     * Dismissible Error Alert Box (Hidden by default, styled with bg-rose-50 border border-rose-200 text-rose-700 rounded-lg p-3 text-sm font-medium flex items-center gap-2) specifically designated to render error messages like "Judul tugas tidak boleh kosong!".
     * Form Fields:
       - Input "Judul Tugas" (text, placeholder: "Contoh: Menyelesaikan Laporan Modul 3", required indicator).
       - Textarea "Deskripsi Tugas" (rows: 3, placeholder: "Tuliskan catatan atau rincian instruksi tugas di sini...").
       - Input "Deadline" (date picker with clean calendar icon).
       - Select Dropdown "Status Tugas" (Options: "Pending", "Completed").
     * Action Buttons:
       - Primary Submit Button: Indigo background, icon, label "Simpan Tugas" (with a built-in spinner loading state animation).
       - Secondary Cancel/Reset Button: Neutral slate border, label "Batal / Reset" (visible especially when editing an existing task).

   - RIGHT COLUMN (Data Table, Filter, and Controls - 7 or 8 cols on lg screen):
     * Control Bar:
       - Search Input: Search field with magnifying glass icon, placeholder: "Cari tugas berdasarkan judul atau deskripsi...".
       - Filter Dropdown: Selector for "Semua Status", "Pending", and "Completed".
     * Responsive Data Table:
       - Table Header: Columns for Checkbox / Quick Toggle (TC-01), Judul & Deskripsi Tugas, Deadline (formatted in Indonesian date style, e.g. "18 Nov 2026"), Status Badge (Yellow/Amber for Pending, Emerald for Completed), and Aksi (Action buttons).
       - Table Row Items: Clean typography, interactive row hover (hover:bg-slate-50/80), custom styled round checkbox for quick completion toggle, title that strikes through with opacity-50 when status is "Completed", and two compact action buttons: Edit (slate-indigo button with pencil icon) and Delete (slate-rose button with trash icon).
       - Empty State: A clean illustrated empty state (folder/clipboard icon, headline "Belum ada tugas", subtitle "Silakan tambahkan tugas baru melalui formulir di sebelah kiri") displayed when tasks array is empty or search returns zero results.

Ensure high accessibility, clear focus rings (focus:ring-2 focus:ring-indigo-500), smooth transition animations for status toggles, and fully mobile-responsive stacking on screens smaller than 1024px.
```
