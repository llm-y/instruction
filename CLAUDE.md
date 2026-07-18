# CLAUDE.md — Aturan kerja repo instruction

## Tujuan repo
Kumpulan file *instruction* untuk task tertentu. Satu folder = satu task.
Isi folder siap disalin/digabung menjadi `CLAUDE.md` (atau file instruction
AI lain) di project pengguna. Konsepnya dijelaskan di `README.md` root.

Repo ini juga dipublikasikan sebagai situs via **GitHub Pages** di
**https://ll.my.id/instruction/**. Di sana `README.md` tiap folder menjadi
halaman indeks direktori itu (dibuka seperti `index.html`), jadi jaga agar
`README.md` bisa berdiri sebagai halaman depan yang wajar.

## Struktur & konvensi
1. **Satu folder per task.** `README.md` di dalam folder = instruction inti
   (core) yang universal untuk task itu. Variasi per sub-jenis ditulis
   sebagai **overlay** terpisah di folder yang sama (mis.
   `manuscript/journal.md`, `manuscript/proposal.md`) — cara pakai:
   core + SATU overlay.
2. **Jangan duplikasi aturan antara core dan overlay.** Aturan universal
   naik ke core; overlay hanya berisi yang spesifik sub-jenis, dan merujuk
   core dengan nomor bagiannya (mis. "core Bagian 3"). Bila mengubah nomor
   bagian di core, perbarui semua rujukan di overlay.
2b. **Komposisi lintas-folder (bila dua task ortogonal).** Bila satu naskah
   memerlukan dua folder pada sumbu berbeda (mis. `buku/` = produksi/format
   buku, `manuscript/` = integritas isi ilmiah), folder yang lebih spesifik
   **merujuk** folder lain via path relatif (`../manuscript/README.md
   Bagian N`) alih-alih menyalin aturannya. Ini komposisi sah, bukan
   pengecualian — tetap berlaku aturan "jangan duplikasi". Batasi hanya untuk
   task yang benar-benar ortogonal (satu tak menggantikan yang lain).
3. **Instruction harus generik & portabel:** dilarang path absolut mesin
   lokal, kredensial, email, atau nama project pribadi. Nilai yang harus
   diisi pengguna ditulis sebagai placeholder `{...}` (mis. `{email-anda}`).
4. **Gaya penulisan:** bahasa Indonesia; aturan bernomor; penanda **WAJIB**
   pada judul bagian yang mengikat; tebalkan kalimat inti tiap aturan;
   setiap file instruction diakhiri checklist yang bisa dicek AI sebelum
   menyatakan selesai.
5. **Sumber saripati dicatat** di footer file (dari CLAUDE.md repo mana
   aturan didistilasi), tanpa menyalin detail spesifik project sumber.
6. **Link antar-file pakai path relatif ke `.md`, bukan `.html` atau URL
   absolut.** Repo dibaca di dua tempat — GitHub (tampilan repo) DAN GitHub
   Pages (`ll.my.id/instruction`). GitHub Pages (Jekyll: `jekyll-relative-links`
   + `jekyll-readme-index`) otomatis me-rewrite link relatif `.md`: mis.
   `manuscript/README.md` → `/instruction/manuscript/`, `journal.md` →
   `journal.html`, `../README.md` → `/instruction/`. Satu bentuk link `.md`
   yang sama sudah benar di KEDUA konteks (terverifikasi di situs Pages) —
   jangan hardcode `.html` atau URL absolut, dan pastikan file target
   memang ada agar rewrite tidak gagal.

## Saat menambah/mengubah instruction
- Folder baru → tambahkan barisnya di tabel "Daftar Instruction" di
  `README.md` root.
- Perubahan aturan → cek konsistensi silang: core ↔ overlay ↔ checklist
  (aturan baru idealnya muncul juga sebagai butir checklist).
- Instruction ini di-inject ke setiap sesi AI pengguna → jaga ringkas;
  bila file membengkak, pecah jadi overlay, jangan biarkan panjang.

## Workflow (WAJIB tiap selesai perubahan)
`git add -A` → `commit` (pesan deskriptif) → `push` ke `main` memakai
**GHPAT** dari `/home/adb/awangga/.env`. Push langsung ke URL
(`https://${GHPAT}@github.com/llm-y/instruction.git`) agar token tidak
tersimpan di konfigurasi remote, dan **selalu mask token** di output
(`| sed "s/${GHPAT}/***/g"`). Jangan pernah mencetak isi `.env`.
