# Overlay: Laporan Penelitian & Teknis

Overlay untuk laporan penelitian (kemajuan/akhir hibah), laporan teknis, dan
laporan proyek riset. **Pakai bersama [`README.md`](README.md) (core)** —
aturan integritas, de-AI, istilah, dan figure ada di sana; file ini hanya
menambah yang spesifik laporan.

> **Beda laporan dari jurnal & proposal:** laporan **melaporkan yang SUDAH
> dikerjakan** (lampau), jadi aturan penuh core Bagian 2 (setiap angka
> tertelusur ke run nyata) berlaku sepenuhnya — beda dari proposal yang
> menulis target. Tapi laporan **bukan artikel jurnal**: tidak wajib
> novelty/positioning ketat, dan pembacanya penyandang dana/institusi/mitra,
> bukan reviewer anonim. Bila laporan akan diangkat jadi artikel, gabungkan
> juga [`journal.md`](journal.md).

---

## L1. Struktur mengikuti template pemberi tugas (WAJIB)

1. **Ikuti template resmi penyandang dana/institusi secara harfiah** — untuk
   laporan hibah biasanya: Ringkasan, Pendahuluan, Tinjauan Pustaka, Metode,
   **Hasil dan Luaran yang Dicapai**, Status Luaran, Kesimpulan, Daftar
   Pustaka, dan **Lampiran bukti luaran**. Simpan template dan rujuk
   (mis. `{Template_Laporan_Institusi.docx}`). Format salah = temuan termudah.
2. **Ringkasan/executive summary padat:** tujuan, apa yang dikerjakan, hasil
   utama **dengan angka nyata**, dan status pencapaian luaran — cukup dibaca
   berdiri sendiri oleh evaluator/pemberi dana.
3. **Konsistensi internal** (core Bagian 1 & J-analog): istilah, notasi, dan
   angka identik di ringkasan = body = tabel = lampiran.

## L2. Akuntabilitas luaran & realisasi (WAJIB — inti laporan)

1. **Petakan janji proposal → realisasi.** Buat tabel `luaran yang
   dijanjikan → status (tercapai/proses/tidak) → bukti`. Setiap target di
   proposal harus punya baris; yang belum tercapai **dinyatakan jujur**, bukan
   disamarkan.
2. **Bukti luaran dilampirkan, bukan diklaim:** artikel (status submit/accepted
   + bukti), HKI/paten (nomor pendaftaran), prototipe (foto/tautan repo),
   dataset (DOI). Klaim "accepted" tanpa bukti = temuan audit.
3. **Hasil null/negatif tetap dilaporkan** (selaras core Bagian 3 poin 3):
   yang tidak berhasil ditulis apa adanya beserta analisis penyebab dan
   rencana lanjut — laporan menilai proses, bukan hanya kemenangan.
4. **Realisasi anggaran & jadwal (bila diminta):** serapan dana dan
   penyimpangan dari timeline dijelaskan wajar; angka anggaran tunduk aturan
   ketertelusuran yang sama dengan angka hasil (core Bagian 2).

## L3. Integritas hasil yang dilaporkan (WAJIB)

1. **Semua angka hasil tunduk penuh core Bagian 2:** tertelusur ke skrip +
   data + commit, deskripsi metode == yang dieksekusi, tanpa fabrikasi, tanpa
   hardcoded. Laporan sering jadi sumber angka untuk artikel lanjutan —
   kesalahan di sini menjalar.
2. **Metode ditulis cukup untuk ditelusuri ulang** (analog core/J Methods):
   data, protokol, parameter, dan lingkungan eksekusi — agar pihak lain
   (auditor, mahasiswa penerus) bisa memverifikasi.
3. **Bedakan hasil antar-tahap/eksperimen dengan tegas** (core Bagian 2 poin
   6): jangan mencampur angka satu kegiatan seolah hasil kegiatan lain.

## L4. Checklist laporan

- [ ] Format 100% sesuai template penyandang dana/institusi (urutan bagian,
      ringkasan, lampiran, gaya sitasi).
- [ ] Tabel janji proposal → realisasi luaran lengkap; yang belum tercapai
      dinyatakan jujur, bukan disamarkan.
- [ ] Setiap klaim luaran punya bukti terlampir (bukti submit/accepted, nomor
      HKI, tautan prototipe/dataset).
- [ ] Hasil null/negatif dilaporkan apa adanya dengan analisis penyebab.
- [ ] Semua angka hasil (dan anggaran, bila ada) tertelusur ke sumber nyata;
      tidak ada fabrikasi (core Bagian 2).
- [ ] Metode cukup rinci untuk ditelusuri ulang oleh auditor/penerus.
- [ ] (Bila akan dipublikasikan) Checklist `journal.md` juga dicek.
