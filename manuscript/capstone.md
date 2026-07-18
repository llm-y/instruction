# Overlay: Laporan Capstone Project (Vokasi)

Overlay untuk laporan **capstone project** mahasiswa vokasi (D3/D4/Sarjana
Terapan) — proyek puncak yang mengintegrasikan kompetensi lintas-matakuliah
untuk menyelesaikan **masalah nyata** (sering dari mitra industri/masyarakat),
umumnya berbasis tim. **Pakai bersama [`README.md`](README.md) (core)** —
aturan integritas, de-AI, istilah, figure, dan LaTeX ada di sana; file ini
hanya menambah yang spesifik capstone.

> **Beda capstone dari laporan riset & proposal:** capstone **melaporkan yang
> SUDAH dibangun** (lampau), jadi aturan penuh core Bagian 2 (angka tertelusur
> ke run/pengujian nyata) berlaku sepenuhnya — beda dari proposal. Tapi
> capstone **bukan riset ilmiah**: nilainya pada **solusi terapan yang
> berfungsi + demonstrasi kompetensi**, bukan novelty/kontribusi keilmuan.
> Karena itu J3 (statistik/ablasi) umumnya tidak berlaku; yang dituntut adalah
> requirement terpenuhi dan uji terima lolos. Untuk prinsip pelaporan luaran
> yang jujur, [`laporan.md`](laporan.md) juga relevan sebagai rujukan.

---

## C1. Struktur mengikuti template prodi/kampus (WAJIB)

1. **Ikuti template resmi prodi/politeknik secara harfiah** — urutan bab,
   penomoran, halaman pengesahan (pembimbing + penguji + mitra bila ada),
   margin, gaya sitasi. Simpan dan rujuk (mis. `{Template_Capstone_Prodi.docx}`).
   Ketidakpatuhan format adalah temuan termudah bagi penguji.
2. **Struktur lazim capstone** (sesuaikan template): Pendahuluan (latar &
   **masalah nyata/kebutuhan mitra**, tujuan, batasan, manfaat), Tinjauan
   (dasar teori + **standar/teknologi** yang dipakai), Analisis & Perancangan
   (kebutuhan → desain), Implementasi, **Pengujian & Hasil**, Penutup
   (kesimpulan + saran), Lampiran (manual, kode, bukti luaran).
3. **Rumusan masalah → tujuan → requirement → solusi → pengujian saling
   mengunci satu-ke-satu.** Setiap tujuan punya requirement terukur dan bukti
   pemenuhannya di bagian pengujian; tidak ada tujuan yang menggantung.
4. **Konsistensi internal:** istilah, notasi, nama modul/komponen seragam di
   seluruh naskah, gambar, dan tabel (core Bagian 5 untuk istilah Indonesia).

## C2. Fokus proyek terapan & demonstrasi kompetensi (WAJIB — inti capstone)

1. **Masalah harus nyata dan spesifik**, bukan dibuat-buat: jelaskan konteks
   pengguna/mitra, kondisi sebelum solusi, dan mengapa layak diselesaikan.
   Sertakan bukti kebutuhan (wawancara/observasi/data mitra) bila ada.
2. **Requirement terukur + kriteria keberhasilan** ditetapkan di awal:
   fungsional (apa yang harus bisa dilakukan sistem) dan non-fungsional
   (kinerja, keandalan, kegunaan). Kriteria inilah yang diuji di C3.
3. **Justifikasi keputusan desain & teknologi bersitasi** (core Bagian 1 & 3):
   mengapa memilih teknologi/metode X, bukan sekadar "karena populer".
   Pilihan mengikuti praktik/standar yang dirujuk, bukan asumsi.
4. **Pemetaan ke capaian pembelajaran (CPL/CPMK) & integrasi kompetensi:**
   tunjukkan capstone menyatukan kompetensi lintas-matakuliah — petakan bagian
   proyek ke capaian pembelajaran yang dituntut prodi.
5. **Proyek tim — kontribusi tiap anggota eksplisit & jujur:** siapa
   mengerjakan apa, tanpa mengklaim kerja anggota lain. Kontribusi individual
   yang jelas melindungi saat sidang dan menjaga keadilan penilaian.

## C3. Pengujian, uji terima & luaran (WAJIB)

1. **Semua hasil pengujian tunduk penuh core Bagian 2:** angka/kinerja
   tertelusur ke run nyata (skrip/log/perangkat), deskripsi metode uji ==
   yang benar-benar dijalankan, tanpa fabrikasi, tanpa hardcoded.
2. **Uji terima (acceptance) terhadap requirement C2:** tabel `requirement →
   metode uji → hasil (lolos/tidak) → bukti`. Setiap requirement punya baris;
   yang belum terpenuhi **dinyatakan jujur** beserta analisis penyebab
   (selaras core Bagian 3 poin 3 — hasil null tetap punya nilai).
3. **Bukti luaran dilampirkan, bukan diklaim:** prototipe/produk/sistem (foto/
   tautan repo/demo), manual penggunaan, dan **serah-terima ke mitra** bila
   ada. Klaim "berjalan di lingkungan mitra" tanpa bukti = temuan.
4. **Skema pengujian cukup untuk ditelusuri ulang** oleh penguji/penerus:
   lingkungan, data uji, langkah, dan hasil didokumentasikan.

## C4. Integritas karya mahasiswa & bimbingan (WAJIB)

1. **Anti-plagiarisme:** semua parafrase, gambar, dan tabel dari sumber lain
   disitasi (core Bagian 1); jalankan cek similarity sesuai aturan prodi.
2. **Kode/aset pihak ketiga diatribusi + patuhi lisensinya:** library,
   template, dataset, dan aset (ikon/gambar) dicantumkan sumber & lisensinya;
   bagian yang dibuat sendiri dibedakan tegas dari yang memakai karya orang.
3. **Setiap klaim bisa dipertanggungjawabkan ke pembimbing ganda** (dosen +
   pembimbing industri/mitra): angka dari run nyata, keputusan desain punya
   alasan, dan tidak ada bagian yang tidak dipahami pengerjaannya.

## C5. Persiapan sidang & demo (WAJIB menjelang sidang)

1. **Demo yang benar-benar berfungsi** lebih meyakinkan daripada slide:
   siapkan lingkungan demo yang stabil, data contoh, dan skenario alur utama.
   Sediakan **rekaman cadangan** bila demo langsung berisiko gagal.
2. **Kuasai setiap keputusan:** mampu menjawab "mengapa teknologi/metode ini?",
   "apa yang terjadi bila beban/masukan di luar rencana?", "requirement mana
   yang belum terpenuhi dan mengapa?", "apa kontribusi Anda spesifiknya?"
   (untuk tim).
3. **Batasan yang jujur menaikkan, bukan menurunkan, nilai** (core Bagian 3):
   sebutkan yang belum sempurna beserta rencana perbaikan, jangan
   menyembunyikannya di depan penguji.

## C6. Checklist capstone

- [ ] Format 100% sesuai template prodi (urutan bab, pengesahan pembimbing/
      penguji/mitra, gaya sitasi).
- [ ] Masalah nyata & spesifik; requirement terukur; rumusan masalah → tujuan
      → requirement → solusi → pengujian mengunci satu-ke-satu.
- [ ] Keputusan desain/teknologi bersitasi; pemetaan ke CPL/CPMK ada; (tim)
      kontribusi tiap anggota eksplisit & jujur.
- [ ] Tabel uji terima requirement → hasil → bukti lengkap; yang belum
      terpenuhi dinyatakan jujur; semua angka dari run nyata (core Bagian 2).
- [ ] Bukti luaran terlampir (prototipe/demo/manual, serah-terima mitra bila
      ada).
- [ ] Integritas: similarity dicek; kode/aset pihak ketiga diatribusi +
      lisensi; tiap klaim bisa dipertanggungjawabkan ke pembimbing ganda.
- [ ] (Sidang) Demo berfungsi + rekaman cadangan; setiap keputusan &
      keterbatasan bisa dijelaskan lisan.

---

*Overlay untuk laporan capstone project vokasi; melengkapi core integritas
akademik `manuscript/README.md`.*
