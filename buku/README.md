# Instruction: Penyusunan Buku ber-ISBN (Core)

Instruction inti untuk AI saat menyusun, mengedit, atau memvalidasi **naskah
buku yang akan didaftarkan ISBN** (buku ajar/teks, monograf, referensi, buku
umum/populer, atau karya sastra). Aturan di file ini **universal** untuk semua
buku ber-ISBN.

**Cara pakai:** salin file ini sebagai `CLAUDE.md` (atau file instruction AI
lain) di repo naskah buku Anda. Bila penerbit menyediakan template, gabungkan
overlay templatenya (mis. [`template-bukupedia.md`](template-bukupedia.md)).
Untuk **buku non-fiksi ilmiah** (buku ajar, monograf, referensi), gabungkan
juga [`manuscript/README.md`](../manuscript/README.md) — aturan integritas
sitasi, de-AI, istilah wajar bahasa Indonesia, serta figure & tabel ada di
sana dan **tidak diduplikasi** di sini. Sesuaikan bagian bertanda `{...}`.

| Jenis buku | File yang digabung |
|------------|--------------------|
| Buku ajar / teks / monograf / referensi (non-fiksi ilmiah) | `README.md` + `manuscript/README.md` (+ overlay template penerbit) |
| Buku umum / populer non-ilmiah | `README.md` (+ overlay template penerbit) |
| Karya sastra (novel, antologi, puisi) | `README.md` (+ overlay template penerbit); integritas sitasi tidak wajib |

---

## 1. Kelayakan ISBN — cek SEBELUM menulis & sebelum submit (WAJIB)

> ISBN diberikan untuk **buku yang diedarkan untuk publik luas**, bukan
> dokumen internal. Cek kelayakan di awal agar tidak menyusun naskah yang
> pasti ditolak.

1. **Minimal 60 halaman isi.** Hitungan **isi saja** (batang tubuh bab);
   TIDAK termasuk front matter (halaman judul, daftar isi, prakata) dan back
   matter (daftar pustaka, indeks, lampiran). Bila di bawah 60 halaman,
   laporkan ke user — jangan "menggelembungkan" dengan spasi/margin.
2. **Untuk peredaran publik luas**, bukan komunitas/kalangan terbatas.
   Penerbit (bila berkolaborasi) ikut bertanggung jawab atas konten dan
   memberi kontribusi nyata, bukan sekadar mencetak.
3. **DILARANG (tidak layak ISBN) — kategori berikut ditolak:**
   - **Materi ajar internal:** tugas kuliah, modul internal, handout institusi.
   - **Karya tugas mahasiswa:** laporan praktik/magang, skripsi/tesis/disertasi
     mentah, tugas akademik.
   - **Laporan penelitian mentah** yang belum diolah menjadi buku untuk
     pembaca umum.
4. **Boleh, dengan syarat diolah jadi buku untuk pembaca umum:** buku ajar
   versi edar-umum (bukan diktat internal), buku referensi/monograf, atau
   orasi ilmiah — semuanya **minimal 60 halaman** dan dikembangkan sebagai
   buku, bukan disalin mentah dari naskah aslinya.
5. **Bila bahan berasal dari skripsi/tesis/disertasi/laporan** (kasus umum):
   WAJIB **transformasi menjadi buku** — buang bahasa "laporan" (Bab I–V kaku,
   "penelitian ini bertujuan..."), ubah jadi narasi bab yang mengalir untuk
   pembaca, hilangkan lampiran administratif, dan tulis ulang, bukan salin-
   tempel. (Bila sumbernya laporan, lihat juga
   [`manuscript/laporan.md`](../manuscript/laporan.md) untuk konteks asalnya.)

## 2. Struktur buku (WAJIB — sesuaikan template penerbit)

1. **Front matter** (bernomor Romawi i, ii, ...): sampul depan, halaman judul
   (+ metadata), halaman redaksi/hak cipta (memuat ISBN, penerbit, tahun,
   pernyataan kolaborasi bila ada), prakata, daftar isi. (Bila ada: daftar
   gambar/tabel, kata pengantar.)
2. **Main matter** (bernomor Arab 1, 2, ...): bab-bab bernomor ("BAB 1",
   "BAB 2", ...) dengan section & subsection berjenjang. Setiap bab punya
   pembuka yang mengaitkan ke benang merah buku dan penutup/ringkasan.
3. **Back matter:** daftar pustaka, glosarium (bila perlu), kredit gambar,
   indeks, tentang penulis, sampul belakang (sinopsis/blurb).
4. **Urutan & kelengkapan mengikuti template penerbit secara harfiah**
   (mis. overlay `template-bukupedia.md`). Halaman redaksi WAJIB lengkap:
   tanpa metadata & ISBN yang benar, buku tidak sah edar.

## 3. Standar konten & narasi buku (WAJIB)

1. **Satu benang merah untuk pembaca sasaran.** Tetapkan siapa pembacanya
   (mahasiswa? praktisi? umum?) dan jaga level bahasa konsisten. Buku
   menuntun pembaca dari dasar ke lanjut, bukan kumpulan artikel lepas.
2. **Tiap bab berdiri sebagai unit belajar:** tujuan bab jelas, isi runtut,
   contoh/ilustrasi konkret, ringkasan di akhir. Untuk buku ajar: tambahkan
   latihan/soal dan tujuan pembelajaran bila relevan.
3. **Progresi antar-bab logis:** konsep dipakai di bab N sudah diperkenalkan
   di bab < N. Rujukan silang antar-bab memakai nomor bab/section, bukan
   "seperti dijelaskan sebelumnya" yang kabur.
4. **Konsistensi internal:** istilah, notasi, gaya penomoran, dan penulisan
   nama/entitas seragam di seluruh buku (buat daftar istilah bila perlu).
5. **Hak cipta & orisinalitas:** kutipan panjang, gambar, dan tabel dari
   sumber lain WAJIB izin/atribusi yang benar (dicatat di kredit gambar /
   daftar pustaka). Untuk integritas sitasi non-fiksi ilmiah, ikuti
   `manuscript/README.md` Bagian 1–2.

## 4. Gaya bahasa & integritas — rujuk core manuscript (WAJIB non-fiksi)

> Agar tidak ada duplikasi aturan, kaidah gaya dipusatkan di
> [`manuscript/README.md`](../manuscript/README.md).

1. **De-AI / hindari AI-tell:** ikuti `manuscript/README.md` Bagian 4 (tanpa
   em-dash, batasi kata promosi, hindari pembuka formulaik & kata khas-LLM).
   Buku panjang rawan pola berulang — variasikan ritme antar-bab.
2. **Istilah wajar bahasa Indonesia:** ikuti `manuscript/README.md` Bagian 5
   (istilah baku bila lazim, istilah asing dicetak miring, ejaan KBBI/PUEBI,
   hindari terjemahan mesin yang kaku).
3. **Integritas sitasi & data (non-fiksi ilmiah):** ikuti
   `manuscript/README.md` Bagian 1–2 (setiap sitasi punya entri terverifikasi
   API, dilarang fabrikasi, angka tertelusur ke sumber). Karya sastra
   dikecualikan dari aturan sitasi.
4. **Figure & tabel:** ikuti `manuscript/README.md` Bagian 6, disesuaikan
   gaya tabel/caption template penerbit (mis. `template-bukupedia.md`).

## 5. Review kelayakan mandiri (WAJIB sebelum menyatakan siap submit)

1. **Jalankan self-review dan nyatakan status: LAYAK atau TIDAK LAYAK**,
   disertai analisis kriteria yang terpenuhi/tidak, catatan khusus, dan
   rekomendasi perbaikan — meniru format review ISBN penerbit.
2. **Bila TIDAK LAYAK, sebutkan pemicunya secara spesifik** (mis. "< 60
   halaman isi", "masih berbentuk laporan skripsi", "sasaran komunitas
   terbatas") dan langkah konkret agar layak — jangan diloloskan diam-diam.

## 6. Checklist buku ber-ISBN

- [ ] Isi ≥ 60 halaman (batang tubuh, di luar front/back matter); bukan
      kategori terlarang (modul internal, tugas mahasiswa, laporan mentah).
- [ ] Bila dari skripsi/tesis/laporan: sudah ditransformasi jadi narasi buku,
      bukan salin-tempel.
- [ ] Struktur lengkap: front matter (halaman redaksi + ISBN + metadata),
      main matter (bab bernomor), back matter (daftar pustaka, tentang penulis,
      sampul belakang) — sesuai template penerbit.
- [ ] Satu benang merah untuk pembaca sasaran; tiap bab unit belajar dengan
      tujuan & ringkasan; progresi antar-bab logis; istilah konsisten.
- [ ] Hak cipta/atribusi gambar & kutipan beres (kredit gambar/daftar pustaka).
- [ ] (Non-fiksi ilmiah) Gaya & integritas mengikuti `manuscript/README.md`
      Bagian 1–2 & 4–6; sitasi terverifikasi API; tanpa fabrikasi.
- [ ] Self-review kelayakan dijalankan; status LAYAK/TIDAK LAYAK dinyatakan
      dengan alasan spesifik.
- [ ] Checklist overlay template penerbit (bila dipakai) juga sudah dicek.

---

*Saripati dari panduan review ISBN Bukupedia
(`naskah.bukupedia.co.id/llmreview/isbn`) dan template buku Bukupedia
(`universitas.bukupedia.co.id/template`).*
