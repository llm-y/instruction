# CLAUDE.md — Aturan kerja repo instruction

## Tujuan repo
Kumpulan file *instruction* untuk task tertentu. Satu folder = satu task.
Isi folder siap disalin/digabung menjadi `CLAUDE.md` (atau file instruction
AI lain) di project pengguna. Konsepnya dijelaskan di `README.md` root.

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
3. **Instruction harus generik & portabel:** dilarang path absolut mesin
   lokal, kredensial, email, atau nama project pribadi. Nilai yang harus
   diisi pengguna ditulis sebagai placeholder `{...}` (mis. `{email-anda}`).
4. **Gaya penulisan:** bahasa Indonesia; aturan bernomor; penanda **WAJIB**
   pada judul bagian yang mengikat; tebalkan kalimat inti tiap aturan;
   setiap file instruction diakhiri checklist yang bisa dicek AI sebelum
   menyatakan selesai.
5. **Sumber saripati dicatat** di footer file (dari CLAUDE.md repo mana
   aturan didistilasi), tanpa menyalin detail spesifik project sumber.

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
