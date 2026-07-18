# Overlay: Template Buku Bukupedia (LaTeX)

Overlay spesifikasi template LaTeX penerbit **Bukupedia**. **Pakai bersama
[`README.md`](README.md) (core)** — aturan kelayakan ISBN, struktur, dan
narasi ada di sana; file ini hanya mengunci **format & tata letak** sesuai
template. Untuk penerbit lain, ganti nilai `{...}` dengan spesifikasi
templatenya.

Sumber template: `universitas.bukupedia.co.id/template`.

---

## T1. Ukuran halaman & margin (WAJIB — jangan diubah)

1. **Ukuran buku 15,5 × 23 cm.** Margin atas/bawah 2 cm, kiri/kanan 1,5 cm.
   Sampul depan & belakang gambar berukuran 15,5 × 23 cm.
2. **Jangan override** ukuran, margin, atau spacing dari kelas template —
   sama seperti kaidah venue di `manuscript/README.md` Bagian 7 poin 8.

## T2. Font & paragraf (WAJIB)

1. **Font isi: Carlito 11pt, spasi tunggal.** Semua paragraf menjorok
   (indent), **termasuk paragraf pertama** setelah judul.
2. **Judul bab:** 24pt tebal, rata kanan, dengan garis bawah biru.
3. **Section:** 12pt tebal, HURUF KAPITAL semua.
4. **Subsection:** 11pt biasa, berlabel huruf `a)`, `b)`, `c)`.
5. **Prakata memakai drop cap** (huruf awal besar) sesuai template.

## T3. Penomoran halaman (WAJIB)

1. **Front matter: angka Romawi kecil** (i, ii, iii, ...).
2. **Main matter & back matter: angka Arab** (1, 2, 3, ...).
3. **Posisi nomor: tengah bawah** halaman.

## T4. Tabel, gambar & kode (WAJIB)

1. **Tabel:** ukuran font 8pt, **grid penuh** (bergaris lengkap), header
   diarsir abu-abu, isi rata tengah. (Catatan: ini berbeda dari gaya booktabs
   di `manuscript/README.md` Bagian 6 — **ikuti gaya template penerbit ini**
   untuk buku Bukupedia.)
2. **Caption tabel:** 8pt rata tengah, format `Tabel X.X.`, diletakkan
   **di atas** tabel.
3. **Caption gambar:** 8pt rata tengah, format `Gambar X.X`, diletakkan
   **di bawah** gambar.
4. **Blok kode:** monospace dalam kotak tak-terputus (non-breaking box),
   **tanpa** syntax highlighting.
5. Aturan integritas & de-AI untuk teks di dalam gambar/tabel tetap berlaku
   (`manuscript/README.md` Bagian 6) — yang berbeda hanya gaya kosmetiknya.

## T5. Bagian buku yang disediakan template (WAJIB dilengkapi)

1. **`\frontmatter`:** sampul depan, halaman judul (+ metadata), halaman
   redaksi (hak cipta/ISBN/penerbit/tahun), prakata (drop cap), daftar isi.
2. **`\mainmatter`:** bab bernomor ("BAB 1", "BAB 2", ...) + section &
   subsection berjenjang.
3. **`\backmatter`:** daftar pustaka (**gaya APA**), glosarium (dikelompokkan
   per huruf), kredit gambar, indeks (header huruf tebal), tentang penulis
   (foto rata kiri), sampul belakang.
4. **Halaman redaksi WAJIB terisi benar** (ISBN, penerbit, tahun, pernyataan
   kolaborasi bila ada) — bukan placeholder template yang tertinggal.
5. **Jalankan audit siap produksi** (core Bagian 5) terhadap sisa khas
   template ini: prakata contoh, entri daftar isi/glosarium/indeks contoh,
   teks bab contoh, dan drop cap pada paragraf dummy — semua harus diganti
   isi nyata sebelum naskah diserahkan.

## T6. Checklist template Bukupedia

- [ ] Ukuran 15,5 × 23 cm; margin 2 cm (atas/bawah) & 1,5 cm (kiri/kanan);
      kelas template tidak dioverride.
- [ ] Font Carlito 11pt spasi tunggal; semua paragraf menjorok termasuk yang
      pertama; hierarki judul (bab 24pt, section kapital 12pt, subsection
      berhuruf) sesuai.
- [ ] Penomoran: Romawi di front matter, Arab di main/back matter, posisi
      tengah bawah.
- [ ] Tabel 8pt grid penuh header abu-abu; caption `Tabel X.X.` di atas &
      `Gambar X.X` di bawah (8pt rata tengah); blok kode monospace tanpa
      highlight.
- [ ] Front/main/back matter lengkap; daftar pustaka gaya APA; halaman
      redaksi terisi benar (ISBN + metadata), tanpa placeholder tersisa.
- [ ] Audit siap produksi (core Bagian 5) dijalankan: tak ada prakata/bab/
      entri daftar-isi-glosarium-indeks contoh atau paragraf dummy dari
      template Bukupedia yang tersisa.

---

*Saripati dari template buku Bukupedia (`universitas.bukupedia.co.id/template`).*
