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

## C1. Model capstone bertahap — kenali proyek & profil targetnya (WAJIB, tentukan lebih dulu)

> Capstone dijalankan **bertahap, satu proyek per tahun**, masing-masing dengan
> **profil kompetensi target** yang harus dibuktikan oleh laporannya.
> **Sebelum menilai atau menulis laporan, tentukan dulu ini Proyek ke berapa**,
> lalu jadikan profil tahun itu kriteria utama penilaian. Bila tak jelas,
> TANYA mahasiswa/pengguna.

| Proyek | Waktu | Profil target | Bukti yang WAJIB tampak di laporan |
|--------|-------|---------------|------------------------------------|
| **Proyek 1** | Akhir tahun ke-1 | **Debugger** | Menemukan & menyelesaikan bug nyata; menguasai perkakas & alur pengembangan dasar: SCM (Git/GitHub), workflow (branch/PR/issue), CI/CD, *vibe coding* (pengembangan berbantuan AI), dan keterampilan teknis dasar minimal setara lulusan SMK RPL. |
| **Proyek 2** | Akhir tahun ke-2 | **Software Engineer** | Membangun **fitur lengkap end-to-end** (kebutuhan → desain → implementasi → integrasi) **beserta pengujiannya** (uji unit/integrasi yang ditulis sendiri, hasil & cakupan, CI menjalankan test otomatis), di atas fondasi perkakas Proyek 1. |
| **Proyek 3** | Akhir tahun ke-3 | **Software Architect** | Merancang **arsitektur sistem** (diagram, dekomposisi, trade-off berjustifikasi) + **integrasi antar-aplikasi via API** (REST/gRPC, kontrak/OpenAPI, komunikasi **Machine-to-Machine**) + **memimpin tim** (koordinasi, code review, integrasi kerja anggota), di atas fondasi Proyek 1 & 2. |

1. **Proyek 1 (Debugger) — laporan WAJIB membuktikan debugging nyata:** ada
   kasus bug konkret dengan alur **gejala → reproduksi → diagnosis → akar
   masalah → perbaikan → verifikasi**, bukan sekadar "membuat fitur". Sertakan
   bukti: langkah reproduksi, log/pesan error, dan commit/PR yang memperbaiki.
2. **Penguasaan perkakas ditunjukkan dengan BUKTI, bukan klaim:**
   - **SCM (Git/GitHub):** riwayat commit bermakna, pemakaian branch/PR, issue
     tracking — tautkan repo (bukan path lokal; core Bagian 4 poin 7).
   - **Workflow & kolaborasi:** alur branch → PR → review → merge terlihat.
   - **CI/CD:** pipeline otomatis (build/test/deploy) dengan konfigurasi &
     bukti jalannya (badge/log).
   - **Vibe coding:** pemakaian alat AI-assisted secara sadar dan bertanggung
     jawab — **tetap memahami & memverifikasi kode yang dihasilkan** (selaras
     C5 integritas), bukan tempelan buta.
3. **Standar minimal setara SMK RPL:** kompetensi teknis dasar (pemrograman,
   struktur data dasar, pemakaian tool) dianggap prasyarat dan harus terlihat
   terpenuhi; capstone menaikkannya ke konteks proyek nyata.
4. **Proyek 2 (Software Engineer) — laporan WAJIB membuktikan pembangunan
   fitur lengkap BESERTA pengujiannya**, bukan sekadar memperbaiki bug (itu
   Proyek 1). Yang wajib tampak:
   - **Fitur lengkap end-to-end:** kebutuhan → desain → implementasi →
     integrasi, berfungsi sesuai requirement (C3).
   - **Pengujian yang ditulis mahasiswa:** uji unit dan/atau integrasi dengan
     kode uji nyata, hasil eksekusi (lolos/gagal), dan **cakupan (coverage)**
     bila diukur — bukan hanya uji manual sekali jalan.
   - **CI menjalankan uji otomatis:** pipeline (dari Proyek 1) kini menjalankan
     *test suite* tiap perubahan; sertakan bukti (log/badge).
   - **Kualitas rekayasa:** kode modular, mengikuti konvensi, dan (bila ada)
     *code review* terlihat di PR.
5. **Proyek 3 (Software Architect) — laporan WAJIB membuktikan perancangan
   sistem, integrasi antar-aplikasi, dan kepemimpinan tim.** Yang wajib tampak:
   - **Arsitektur sistem:** diagram arsitektur/komponen, dekomposisi layanan,
     dan **keputusan desain beserta trade-off-nya** yang dijustifikasi (core
     Bagian 3) — di level sistem, bukan satu fitur (itu Proyek 2).
   - **Integrasi antar-aplikasi via API:** rancang & implementasi API
     (mis. REST/gRPC) dengan kontrak/spesifikasi (mis. OpenAPI), termasuk
     komunikasi **Machine-to-Machine (M2M)** antar-layanan — autentikasi
     antar-mesin (API key/OAuth client-credentials), penanganan error &
     versioning.
   - **Kepemimpinan tim:** bukti memimpin — pembagian & koordinasi tugas,
     memimpin *code review*, mengintegrasikan kerja anggota, dan menjaga mutu
     tim (bukan sekadar kontribusi kode individual, C3 poin 5).
   - Dibangun di atas Proyek 1 (debugging) & Proyek 2 (fitur + pengujian):
     sistem terintegrasi tetap teruji dan CI/CD tetap jalan.
6. **Catatan gaya:** *vibe coding* boleh untuk membangun PRODUK, tetapi
   **prosa laporan tetap tunduk aturan de-AI** (core Bagian 4) dan istilah
   wajar Indonesia (core Bagian 5) — jangan menyerahkan teks mentah hasil AI.

## C2. Struktur mengikuti template prodi/kampus (WAJIB)

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

## C3. Fokus proyek terapan & demonstrasi kompetensi (WAJIB — inti capstone)

1. **Masalah harus nyata dan spesifik**, bukan dibuat-buat: jelaskan konteks
   pengguna/mitra, kondisi sebelum solusi, dan mengapa layak diselesaikan.
   Sertakan bukti kebutuhan (wawancara/observasi/data mitra) bila ada.
2. **Requirement terukur + kriteria keberhasilan** ditetapkan di awal:
   fungsional (apa yang harus bisa dilakukan sistem) dan non-fungsional
   (kinerja, keandalan, kegunaan). Kriteria inilah yang diuji di C4.
3. **Justifikasi keputusan desain & teknologi bersitasi** (core Bagian 1 & 3):
   mengapa memilih teknologi/metode X, bukan sekadar "karena populer".
   Pilihan mengikuti praktik/standar yang dirujuk, bukan asumsi.
4. **Pemetaan ke capaian pembelajaran (CPL/CPMK) & profil tahun (C1):**
   tunjukkan capstone menyatukan kompetensi lintas-matakuliah dan **membuktikan
   profil target tahun itu** — petakan bagian proyek ke capaian yang dituntut.
5. **Proyek tim — kontribusi tiap anggota eksplisit & jujur:** siapa
   mengerjakan apa, tanpa mengklaim kerja anggota lain. Kontribusi individual
   yang jelas melindungi saat sidang dan menjaga keadilan penilaian.

## C4. Pengujian, uji terima & luaran (WAJIB)

1. **Semua hasil pengujian tunduk penuh core Bagian 2:** angka/kinerja
   tertelusur ke run nyata (skrip/log/perangkat), deskripsi metode uji ==
   yang benar-benar dijalankan, tanpa fabrikasi, tanpa hardcoded.
2. **Uji terima (acceptance) terhadap requirement C3:** tabel `requirement →
   metode uji → hasil (lolos/tidak) → bukti`. Setiap requirement punya baris;
   yang belum terpenuhi **dinyatakan jujur** beserta analisis penyebab
   (selaras core Bagian 3 poin 3 — hasil null tetap punya nilai).
3. **Bukti luaran dilampirkan, bukan diklaim:** prototipe/produk/sistem (foto/
   tautan repo/demo), manual penggunaan, dan **serah-terima ke mitra** bila
   ada. Klaim "berjalan di lingkungan mitra" tanpa bukti = temuan.
4. **Skema pengujian cukup untuk ditelusuri ulang** oleh penguji/penerus:
   lingkungan, data uji, langkah, dan hasil didokumentasikan.

## C5. Integritas karya mahasiswa & bimbingan (WAJIB)

1. **Anti-plagiarisme:** semua parafrase, gambar, dan tabel dari sumber lain
   disitasi (core Bagian 1); jalankan cek similarity sesuai aturan prodi.
2. **Kode/aset pihak ketiga diatribusi + patuhi lisensinya:** library,
   template, dataset, aset (ikon/gambar), dan **kode hasil AI (*vibe coding*)**
   dicantumkan sumber & statusnya; bagian yang dibuat/dipahami sendiri
   dibedakan tegas dari yang memakai karya orang/mesin.
3. **Setiap klaim bisa dipertanggungjawabkan ke pembimbing ganda** (dosen +
   pembimbing industri/mitra): angka dari run nyata, keputusan desain punya
   alasan, dan tidak ada bagian (termasuk kode AI) yang tidak dipahami.

## C6. Persiapan sidang & demo (WAJIB menjelang sidang)

1. **Demo yang benar-benar berfungsi** lebih meyakinkan daripada slide:
   siapkan lingkungan demo yang stabil, data contoh, dan skenario alur utama.
   Sediakan **rekaman cadangan** bila demo langsung berisiko gagal.
2. **Kuasai setiap keputusan:** mampu menjawab "mengapa teknologi/metode ini?",
   "apa yang terjadi bila beban/masukan di luar rencana?", "requirement mana
   yang belum terpenuhi dan mengapa?", "apa kontribusi Anda spesifiknya?"
   (untuk tim). Untuk Proyek 1: mampu menunjukkan **cara mendiagnosis bug**
   secara langsung, bukan hanya hasil akhirnya.
3. **Batasan yang jujur menaikkan, bukan menurunkan, nilai** (core Bagian 3):
   sebutkan yang belum sempurna beserta rencana perbaikan, jangan
   menyembunyikannya di depan penguji.

## C7. Checklist capstone

- [ ] Bahan bukti profil tersedia sebelum menulis (Proyek 1: repo + log/commit
      bug; Proyek 2: kode fitur + hasil uji; Proyek 3: desain + API/M2M + bukti
      kepemimpinan); yang kurang dilaporkan, tidak dikarang (core Bagian 2).
- [ ] Proyek ke berapa (1/2/3) sudah ditentukan; **profil target tahun itu
      (C1) terbukti** di laporan (Proyek 1: debugging nyata + SCM/workflow/
      CI-CD/vibe coding + dasar SMK RPL; Proyek 2: fitur lengkap end-to-end +
      pengujian ditulis sendiri + CI menjalankan test otomatis; Proyek 3:
      arsitektur sistem + integrasi API/M2M + memimpin tim).
- [ ] Format 100% sesuai template prodi (urutan bab, pengesahan pembimbing/
      penguji/mitra, gaya sitasi).
- [ ] Masalah nyata & spesifik; requirement terukur; rumusan masalah → tujuan
      → requirement → solusi → pengujian mengunci satu-ke-satu.
- [ ] Keputusan desain/teknologi bersitasi; pemetaan ke CPL/CPMK & profil
      tahun ada; (tim) kontribusi tiap anggota eksplisit & jujur.
- [ ] Tabel uji terima requirement → hasil → bukti lengkap; yang belum
      terpenuhi dinyatakan jujur; semua angka dari run nyata (core Bagian 2).
- [ ] Bukti luaran terlampir (prototipe/demo/manual, serah-terima mitra bila
      ada); bukti perkakas (repo/commit/PR, pipeline CI/CD) tertaut.
- [ ] Integritas: similarity dicek; kode/aset pihak ketiga & kode AI
      diatribusi + lisensi; tiap klaim bisa dipertanggungjawabkan ke
      pembimbing ganda.
- [ ] Prosa laporan tetap lolos de-AI (core Bagian 4) meski produk memakai
      vibe coding.
- [ ] (Sidang) Demo berfungsi + rekaman cadangan; setiap keputusan &
      keterbatasan bisa dijelaskan lisan.

---

*Overlay untuk laporan capstone project vokasi; melengkapi core integritas
akademik `manuscript/README.md`.*
