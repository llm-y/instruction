# Overlay: Artikel Jurnal Bereputasi Tinggi

Overlay untuk artikel jurnal / conference paper. **Pakai bersama
[`README.md`](README.md) (core)** — aturan integritas, de-AI, istilah, dan
figure ada di sana; file ini hanya menambah yang spesifik jurnal.

---

## J1. Narasi menyeluruh (WAJIB saat menyusun/merevisi kerangka)

1. **Satu benang merah.** Seluruh naskah menceritakan SATU alur: gap →
   pertanyaan riset → metode → bukti → implikasi. Setiap paragraf yang tidak
   menyokong alur ini dipindah ke appendix atau dibuang.
2. **Konsistensi internal:** notasi/simbol seragam (satu simbol satu makna),
   singkatan didefinisikan sekali saat pertama muncul, tense konsisten,
   angka di abstrak = body = tabel = kesimpulan.
3. **Setiap kontribusi bernomor di Introduction WAJIB terjawab dengan bukti
   di Results dan dibahas di Discussion.** Peta kontribusi → bukti →
   pembahasan harus utuh, tanpa kontribusi yang menggantung.

## J2. Standar konten per bagian — IMRaD (WAJIB saat menulis tiap bagian)

> Kerangka acuan = **IMRaD** (Introduction, Methods, Results, and
> Discussion). Sebagian venue menggabung Results+Discussion, memisah
> Background, atau memakai struktur lain untuk paper teori/review —
> **sesuaikan dengan *Guide for Authors*** (J4.2), tapi disiplin "apa yang
> BOLEH dan TIDAK BOLEH ada di tiap bagian" tetap berlaku.

1. **Judul & Abstract.** Judul spesifik memuat objek + kontribusi, tanpa
   hype. Abstract mengikuti pola: konteks (1 kalimat) → gap → metode →
   **hasil utama dengan angka** → implikasi. *Tidak boleh:* sitasi,
   singkatan tak umum, klaim tanpa angka. Angka di abstract WAJIB identik
   dengan body.
2. **Introduction — corong:** bidang → masalah spesifik → **gap yang tajam**
   (apa yang belum bisa dilakukan riset sebelumnya, didukung sitasi bukan
   asumsi) → **kontribusi eksplisit** (daftar bernomor, tiap butir dapat
   diverifikasi di Results). *Tidak boleh:* detail metode/hasil, atau
   berubah jadi mini-related-work.
3. **Related Work — positioning, bukan katalog.** Kelompokkan per
   pendekatan; akhiri tiap kelompok dengan **keterbatasannya relatif
   terhadap usulan**. Sitasi pesaing terkuat secara jujur (reviewer sering
   penulisnya) dan mutakhir (3–5 tahun terakhir) di venue target. *Tidak
   boleh:* rangkuman kronologis satu-paper-satu-paragraf tanpa sikap.
4. **Methods — cukup untuk reproduksi orang lain.** Muat: sumber & ukuran
   data + skema split; preprocessing; arsitektur/algoritma dengan
   notasi/rumus; setup (hardware, hyperparameter, seed, versi library);
   protokol evaluasi (metrik + uji statistik + skema validasi). Deskripsi
   WAJIB persis sama dengan yang dieksekusi (core Bagian 2). *Tidak boleh:*
   angka hasil/performa (itu Results), justifikasi tanpa sitasi.
5. **Results — temuan objektif.** Laporkan: tabel/gambar utama, angka
   **dengan dispersi** (SD/CI), uji signifikansi + effect size, dan ablasi.
   Tiap kontribusi Introduction dijawab bukti di sini. *Tidak boleh:*
   interpretasi/spekulasi/perbandingan mendalam (itu Discussion), metode
   baru, atau angka yang tak tertelusur ke run nyata (core Bagian 2).
6. **Discussion — makna, bukan pengulangan.** Muat: interpretasi (apa arti
   hasil, **mengapa** — mekanisme), perbandingan dengan penelitian terdahulu
   (angka pembanding dari sumber nyata, bukan ingatan), implikasi praktis/
   teoretis, dan **ancaman validitas + keterbatasan** yang spesifik. *Tidak
   boleh:* memperkenalkan hasil/data baru, atau sekadar mengulang Results
   tanpa menafsirkan.
7. **Conclusion.** Jawab pertanyaan riset secara eksplisit, tegaskan
   kontribusi, dan future work yang konkret. **Limitations yang jujur
   menaikkan, bukan menurunkan, peluang diterima.** *Tidak boleh:* jadi
   duplikat abstrak, atau memunculkan klaim/sitasi yang belum ada di body.

## J3. Kekakuan metodologi & statistik (WAJIB untuk naskah bereksperimen)

1. **Anti data leakage — cek eksplisit:** normalisasi/scaling di-fit HANYA
   pada train set, seleksi fitur & tuning hyperparameter di dalam
   cross-validation (nested bila perlu), tidak ada informasi subjek/waktu
   test yang bocor ke train. Leakage adalah alasan tolak paling mematikan.
2. **Perbandingan harus adil (*matched-budget, same-protocol*):** baseline
   di-tuning sama seriusnya dengan metode usulan, data split identik,
   metrik identik. Menang lawan baseline yang dilemahkan = temuan palsu.
3. **Statistik yang benar:** laporkan mean ± SD/CI dari beberapa run/seed
   (bukan single run terbaik), uji signifikansi yang sesuai asumsi datanya,
   koreksi *multiple comparisons* (Bonferroni/Holm/FDR) bila menguji banyak
   hipotesis, dan laporkan *effect size* — bukan hanya p-value.
4. **Reproducibility pack:** seed dicatat, versi library dipin, split
   dipublikasikan, perintah reproduksi satu-entry-point, data/kode dirilis
   (atau alasan legalnya dinyatakan) di *Data & Code Availability*.
5. **Ablasi membuktikan setiap komponen:** tiap komponen yang diklaim
   berkontribusi harus punya baris ablasi. Komponen tanpa bukti kontribusi
   → buang dari klaim (selaras tangga kompleksitas, core Bagian 3).
6. **Laporkan biaya:** waktu latih/inferensi, parameter, memori — reviewer
   jurnal bereputasi menanyakan trade-off akurasi vs biaya.

## J4. Etika publikasi & kepatuhan jurnal target (WAJIB sebelum submit)

1. **Anti-plagiarisme & self-plagiarism:** semua parafrase disitasi; teks
   dari paper sendiri sebelumnya tidak dipakai ulang tanpa sitasi. Jalankan
   cek similarity sebelum submit; jelaskan overlap yang sah (mis. preprint).
2. **Ikuti *Guide for Authors* jurnal target secara harfiah:** scope cocok
   (cek beberapa paper serupa pernah terbit di sana), batas kata/halaman,
   gaya referensi, struktur bagian, format gambar, highlights/graphical
   abstract bila diminta. Ketidakpatuhan format = desk reject.
3. **Deklarasi wajib lengkap:** kontribusi author (CRediT), conflict of
   interest, funding, ethics approval/IRB + informed consent (bila melibatkan
   subjek manusia/data pribadi), data & code availability.
4. **Deklarasi penggunaan AI:** ikuti kebijakan jurnal/penerbit (Elsevier,
   IEEE, Springer mewajibkan disclosure penggunaan LLM dalam penulisan; AI
   tidak boleh jadi author). Jangan disembunyikan.
5. **Dilarang dual submission** — satu naskah hanya di satu venue pada satu
   waktu. Preprint (arXiv) umumnya boleh; cek kebijakan jurnal.
6. **Cover letter spesifik:** mengapa naskah ini cocok untuk jurnal INI,
   kontribusi utama dalam 2–3 kalimat, dan pernyataan orisinalitas —
   bukan template generik.

## J5. Menghadapi review (WAJIB saat revisi)

1. **Response-to-reviewers point-by-point:** setiap komentar dikutip, dijawab
   satu per satu, dengan (a) jawaban langsung, (b) perubahan yang dilakukan,
   (c) lokasi perubahan (halaman/baris). Tidak ada komentar yang dilewati.
2. **Jangan defensif — reviewer yang "salah paham" berarti naskah kurang
   jelas.** Perbaiki naskahnya, jangan hanya membantah di response letter.
   Bila menolak saran, tolak dengan bukti/argumen kuat dan nada hormat.
3. **Komentar reviewer = daftar kelemahan gratis.** Bila diminta eksperimen
   tambahan yang masuk akal, kerjakan; hasilnya sering memperkuat paper.

## J6. Checklist jurnal

- [ ] Satu benang merah; kontribusi bernomor terverifikasi di Results dan
      dibahas di Discussion; angka konsisten abstrak = body = kesimpulan.
- [ ] Tiap bagian patuh standar konten IMRaD (J2): Methods tanpa angka
      hasil; Results tanpa interpretasi; Discussion tanpa hasil/data baru;
      Conclusion bukan duplikat abstrak.
- [ ] Bebas data leakage; baseline adil (matched-budget); mean ± SD/CI
      multi-seed; koreksi multiple comparisons; effect size dilaporkan;
      ablasi per komponen; biaya komputasi dilaporkan.
- [ ] Similarity dicek; format sesuai Guide for Authors; semua deklarasi
      (CRediT, COI, funding, ethics, data availability, penggunaan AI) ada;
      tidak dual submission.
- [ ] (Revisi) Semua komentar reviewer terjawab point-by-point dengan lokasi
      perubahan.
