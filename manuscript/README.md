# Instruction: Validasi Integritas Akademik Penulisan Ilmiah

Instruction untuk AI saat menulis, mengedit, atau memvalidasi naskah akademik:
artikel jurnal bereputasi tinggi, artikel ilmiah, laporan dan proposal
penelitian, disertasi, serta tesis. Salin isi file ini sebagai `CLAUDE.md`
(atau file instruction AI lain) di repo naskah Anda, lalu sesuaikan bagian
yang ditandai `{...}`.

---

## 1. Integritas sitasi & bibliografi (WAJIB)

1. **Setiap sitasi di naskah HARUS punya entri di file bibliografi** (mis.
   setiap `\cite{key}`/`\textcite{key}` punya entri di `.bib`). Sebelum
   menyelesaikan pekerjaan: rebuild dokumen dan pastikan **0 "Citation ...
   undefined"** di log dan **0 error** di log bibliografi (`.blg`).
2. **Setiap entri bibliografi HARUS diverifikasi ke API otoritatif** sebelum
   dianggap final — JANGAN mengisi author/DOI/volume/halaman dari ingatan:
   - DOI penerbit → **CrossRef**: `https://api.crossref.org/works/{DOI}`
   - DOI arXiv (`10.48550/arXiv.*`) → **DataCite**: `https://api.datacite.org/dois/{DOI}`
   - Sertakan `?mailto={email-anda}` pada request CrossRef (polite pool).
   - Cocokkan seluruh field: title, author lengkap, journal/venue, volume,
     number, pages, year, DOI.
3. **Dilarang keras sitasi fabrikasi.** Jika metadata tidak bisa diverifikasi
   lewat API, tandai entrinya dan **laporkan ke user** — jangan diteruskan.
   (Catatan BibTeX: `%` tidak dikenal di dalam blok `@{}`; komentar inline
   merusak parsing — tandai di luar entri.)
4. Format bibliografi konsisten: nama author penuh (`Family, Given and ...`),
   lindungi akronim dengan kurung kurawal (`{EEG}`, `{BCI}`, `{CNN}`),
   en-dash untuk rentang halaman (`920--928`).

## 2. Integritas klaim & data — klaim HARUS sesuai bukti (WAJIB)

1. **Setiap angka dan klaim hasil di naskah harus dapat ditelusuri ke
   sumbernya**: skrip yang menghasilkannya, file data/CSV sumber, dan commit.
   Tidak ada angka yang "muncul" tanpa jejak run/eksperimen nyata.
2. **Deskripsi metode di teks WAJIB persis sama dengan yang benar-benar
   dieksekusi** (kode, protokol eksperimen, jumlah subjek/sampel, parameter).
   Sebelum klaim masuk naskah: buka kodenya/datanya, pastikan cocok. Bila
   berbeda → perbaiki teks ATAU jalankan ulang dengan metode yang benar.
   Jangan dibiarkan.
3. **Klaim "validasi/reproduksi" harus berasal dari run aktual**, bukan
   ditulis tangan. Angka pembanding harus benar-benar dari output.
4. **Dilarang angka hardcoded** di skrip plot/analisis — semua angka harus
   mengalir dari data sumber.
5. **Bila ragu apakah suatu angka valid → tandai INVALID/quarantine dan lapor
   ke user.** JANGAN diteruskan ke naskah.
6. Bedakan hasil dari metode yang berbeda dengan tegas — jangan pernah
   melaporkan angka dari satu pipeline/eksperimen seolah-olah hasil
   pipeline/eksperimen lain.

## 3. Prinsip argumentasi: ketegangan jadi rigor (WAJIB saat menulis klaim/novelty)

> Tujuan: argumen yang tahan serangan reviewer/penguji, bukan klaim yang
> menyenangkan.

1. **Ketegangan jangan disembunyikan — ubah jadi rigor.** Bila ada bukti
   (termasuk karya penulis sendiri) yang tampak menentang usulan, bingkai
   sebagai alur diagnosis → generalisasi, dan tundukkan usulan pada bar
   metodologis yang sama (ablasi ketat, baseline *matched-budget /
   same-protocol*). Mengakui dan menjawab lebih kuat daripada menutupi.
2. **Novelty = insight/generalitas, BUKAN merakit blok yang sudah ada.**
   Kunci SATU kontribusi ilmiah utama. Jangan klaim "modulnya baru" bila
   komponennya sudah umum; yang baru adalah temuan/hukum empirisnya atau
   bukti generalitas lintas kasus.
3. **Anti-overclaim & siapkan narasi cadangan.** Jangan buat klaim yang tak
   bisa dibuktikan. Rancang agar kontribusi tidak bergantung pada satu hasil
   rapuh; jika hasil null, nilai harus tetap ada (generalitas,
   interpretabilitas, insight). "Sederhana sudah cukup" adalah temuan sah
   (*less-is-more*), bukan kegagalan.
4. **Mulai dari titik berangkat paling sederhana, naiki tangga kompleksitas
   anak tangga demi anak tangga.** Kompleksitas hanya ditambah bila ablasi
   membuktikan manfaatnya sepadan dengan biayanya (*earns its keep*). Jangan
   memprivilege rancangan kompleks sebagai titik awal.
5. **Tulis dengan antisipasi serangan reviewer/penguji.** Pre-empt vektor
   lethal yang umum: kebaruan inkremental, feasibility/scope berlebihan,
   keadilan baseline, validitas statistik (koreksi *multiple comparisons*),
   kedalaman teori, dan generalisasi klaim melebihi cakupan eksperimen.

## 4. Gaya tulisan — de-AI / hindari "AI-tell" (WAJIB saat menulis/mengedit prosa)

> Tujuan: prosa akademik yang natural, tidak "templated". Catatan: detektor
> similarity (mis. iThenticate) dan detektor-AI adalah hal terpisah dan
> keduanya tidak sempurna; aturan ini mengurangi sinyal AI-tell, BUKAN
> jaminan lolos detektor. Saat merestilasi (de-AI): **jangan ubah angka,
> sitasi, atau klaim** — hanya bentuk kalimatnya.

1. **Dilarang em-dash (`---`).** Pakai koma, tanda kurung, titik dua, atau
   pecah kalimat. En-dash (`--`) tetap untuk rentang angka (`8--12` Hz,
   `920--928`) dan senyawa (`CNN--Riemannian`).
2. **Jangan ulang kata bernuansa promosi:** *robust*, *novel*,
   *comprehensive*, *crucial*, *powerful*, *lightweight*, *seamless*,
   *reproducible*. Cek frekuensi sebelum selesai (`grep -oic`); idealnya
   ≤2–3 kemunculan per kata di seluruh naskah.
3. **Hindari pembuka klausa formulaik.** Inggris: *Moreover,* *Furthermore,*
   *Notably,* *Importantly,* *It is worth noting,* *Overall,*. Indonesia:
   "Selain itu,", "Lebih lanjut,", "Penting untuk dicatat,", "Secara
   keseluruhan,". Pakai transisi spesifik atau langsung ke isi.
4. **Hindari kata khas-LLM:** *delve*, *leverage* (pakai *use*),
   *underscore*, *pivotal*, *realm*, *tapestry*, *intricate*, *meticulous*,
   *showcase*.
5. **Variasikan ritme & struktur.** Hindari deret-tiga (tricolon) yang
   berulang terlalu rapi dan pola "not only X but also Y" / "tidak hanya X
   tetapi juga Y" yang berulang. Selingi kalimat pendek dan panjang.
6. **Konkret > generik.** Ganti klaim umum ("significantly improves
   performance") dengan angka/spesifik yang sudah terverifikasi (lihat
   Bagian 2).
7. **Hindari "implementation clutter"** — jangan sitir nama file/path repo di
   prosa naskah. Rujuk artefak via DOI/URL di *Data & Code Availability
   statement*; paling banyak sebut satu skrip entry-point reproduksi.
   Nama library (mis. scikit-learn) wajar disebut.

## 5. Istilah wajar bahasa Indonesia (WAJIB untuk naskah berbahasa Indonesia)

> Tujuan: naskah terbaca sebagai tulisan akademik Indonesia yang natural,
> bukan hasil terjemahan mesin — terjemahan harfiah yang kaku adalah salah
> satu AI-tell paling kentara dalam bahasa Indonesia.

1. **Pakai istilah baku bila sudah lazim di bidangnya**, mis. "pembelajaran
   mesin" (*machine learning*), "jaringan saraf tiruan", "himpunan data".
   Bila padanan Indonesia TIDAK lazim di komunitas riset, **pertahankan
   istilah asing dengan cetak miring** (*deep learning*, *overfitting*,
   *attention*) — jangan memaksakan terjemahan yang tidak dikenal
   ("pembelajaran mendalam yang dalam", "perhatian-diri").
2. **Konsisten satu istilah untuk satu konsep** di seluruh naskah. Jangan
   berganti-ganti antara "pelatihan"/"training" atau "citra"/"gambar"/"image"
   — pilih satu, catat di daftar istilah bila perlu.
3. **Hindari terjemahan harfiah yang kaku** khas mesin: "Dalam rangka untuk"
   (*in order to* → cukup "untuk"), "Hal ini dikarenakan oleh" (→ "karena"),
   "melakukan evaluasi terhadap" (→ "mengevaluasi"), "memiliki kemampuan
   untuk" (→ "dapat/mampu").
4. **Hindari kata/frasa AI-tell versi Indonesia** yang berlebihan:
   "menggarisbawahi", "menyoroti", "memanfaatkan" (bila cukup "menggunakan"),
   "sangat penting/krusial", "signifikan" tanpa dasar uji statistik, serta
   pembuka generik "Dalam era digital...", "Seiring dengan perkembangan
   teknologi...". Langsung ke persoalan spesifik.
5. **Ikuti kaidah PUEBI/EYD**: istilah asing dicetak miring, kata serapan
   baku ditulis sesuai KBBI (mis. "analisis" bukan "analisa", "metode" bukan
   "metoda", "sistem" bukan "sistim"), hindari campuran kata Inggris di
   tengah kalimat bila padanan bakunya lazim.
6. **Kalimat aktif dan langsung lebih disukai** daripada pasif berlapis khas
   terjemahan ("telah dilakukan pengujian oleh peneliti terhadap..." →
   "peneliti menguji...").

## 6. Figure & tabel — standar jurnal bereputasi tinggi (WAJIB saat membuat/mengedit gambar)

> Aturan integritas (Bagian 2) dan gaya bahasa (Bagian 4–5) **berlaku juga
> untuk semua teks di dalam gambar dan tabel**: label sumbu, legend, anotasi,
> caption, dan judul kolom.

### Integritas data dalam visualisasi

1. **Setiap gambar hasil harus digenerate dari data nyata lewat skrip yang
   tertelusur** (skrip + file data sumber + commit) — dilarang menggambar
   ulang/menghias angka secara manual, dilarang angka hardcoded di skrip plot.
2. **Jangan menyesatkan secara visual:** sumbu-y dipotong harus ditandai
   jelas, skala log disebutkan, error bar didefinisikan di caption (SD? SE?
   CI 95%?), jangan cherry-pick rentang data yang menguntungkan.
3. **Caption harus mandiri (self-contained):** pembaca memahami gambar tanpa
   membaca body text — apa yang diplot, dari data mana, n berapa, singkatan
   didefinisikan.

### Kosmetik — cek WAJIB sebelum gambar dianggap final

4. **Format & resolusi:** utamakan vektor (PDF/EPS/SVG) untuk plot dan
   diagram; raster (PNG/TIFF) minimal 300 dpi (600 dpi untuk line art).
   JANGAN screenshot plot lalu ditempel.
5. **Font terbaca saat tercetak:** ukuran teks dalam gambar ±8pt atau lebih pada
   ukuran cetak final (satu kolom ≈ 3,5 in / 8,9 cm; dua kolom ≈ 7 in). Satu
   keluarga font konsisten di semua gambar, idealnya serasi dengan font naskah.
6. **Konsistensi antar-gambar:** palet warna, gaya garis, marker, urutan
   legend, dan penamaan metode sama di seluruh naskah (metode yang sama =
   warna yang sama di semua gambar).
7. **Warna aman:** colorblind-safe (mis. palet Okabe–Ito, viridis) dan tetap
   terbaca bila dicetak hitam-putih (bedakan juga dengan gaya garis/marker,
   bukan warna saja).
8. **Bersihkan elemen sisa (chartjunk):** tanpa judul ganda (judul cukup di
   caption, bukan di dalam plot), tanpa gridline berlebih, tanpa border
   ganda, tanpa whitespace lebar, tanpa watermark/nama tool.
9. **Label lengkap:** semua sumbu berlabel dengan satuan, tick terbaca,
   legend tidak menutupi data, panel bertanda (a), (b), (c) bila multi-panel
   dan dirujuk per-panel di caption.

### De-AI pada gambar

10. **Teks dalam gambar mengikuti aturan de-AI** (Bagian 4–5): tanpa em-dash,
    tanpa kata promosi, istilah konsisten dengan body text (jangan "training
    accuracy" di gambar tapi "akurasi pelatihan" di teks).
11. **Dilarang diagram/ilustrasi generatif-AI** (skema "kartun" hasil
    text-to-image) untuk diagram metode — buat dengan tool diagram nyata
    (TikZ, draw.io, Inkscape, matplotlib). Banyak jurnal bereputasi melarang
    gambar hasil AI generatif, dan artefaknya (teks rusak, ikon aneh,
    ketidakkonsistenan garis) adalah AI-tell yang kentara.
12. **Hindari gaya "template AI" pada diagram:** kotak-panah seragam penuh
    gradien dan ikon dekoratif tanpa makna. Setiap elemen visual harus
    membawa informasi; diagram alur metode harus mencerminkan pipeline yang
    BENAR-BENAR dieksekusi (cek terhadap kode, selaras Bagian 2).

## 7. Struktur & narasi naskah (WAJIB saat menyusun/merevisi kerangka)

1. **Satu benang merah.** Seluruh naskah menceritakan SATU alur: gap →
   pertanyaan riset → metode → bukti → implikasi. Setiap paragraf yang tidak
   menyokong alur ini dipindah ke appendix atau dibuang.
2. **Abstrak memuat angka.** Pola: konteks (1 kalimat) → gap → metode →
   hasil utama DENGAN angka → implikasi. Tanpa sitasi, tanpa singkatan tak
   umum. Angka di abstrak WAJIB identik dengan body dan kesimpulan.
3. **Introduction berbentuk corong:** bidang → masalah spesifik → gap yang
   tajam (apa yang belum bisa dilakukan riset sebelumnya) → kontribusi
   eksplisit (daftar bernomor, tiap butir dapat diverifikasi di Results).
   Gap harus didukung sitasi, bukan asumsi.
4. **Related work = positioning, bukan katalog.** Kelompokkan per pendekatan,
   akhiri tiap kelompok dengan keterbatasannya relatif terhadap usulan.
   Sitasi pesaing terkuat secara jujur — reviewer sering adalah penulisnya.
   Pastikan ada sitasi mutakhir (3–5 tahun terakhir) di venue target.
5. **Kesimpulan ≠ ringkasan abstrak.** Jawab pertanyaan riset secara
   eksplisit, akui keterbatasan secara spesifik (bukan basa-basi), dan
   future work yang konkret. **Bagian *Limitations* yang jujur menaikkan,
   bukan menurunkan, peluang diterima.**
6. **Konsistensi internal:** notasi/simbol seragam (satu simbol satu makna),
   singkatan didefinisikan sekali saat pertama muncul, tense konsisten,
   angka di abstrak = body = tabel = kesimpulan.

## 8. Kekakuan metodologi & statistik (WAJIB untuk naskah bereksperimen)

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
   → buang dari klaim (selaras tangga kompleksitas, Bagian 3).
6. **Laporkan biaya:** waktu latih/inferensi, parameter, memori — reviewer
   jurnal bereputasi menanyakan trade-off akurasi vs biaya.

## 9. Etika publikasi & kepatuhan jurnal target (WAJIB sebelum submit)

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

## 10. Menghadapi review & sidang (WAJIB saat revisi/persiapan sidang)

1. **Response-to-reviewers point-by-point:** setiap komentar dikutip, dijawab
   satu per satu, dengan (a) jawaban langsung, (b) perubahan yang dilakukan,
   (c) lokasi perubahan (halaman/baris). Tidak ada komentar yang dilewati.
2. **Jangan defensif — reviewer yang "salah paham" berarti naskah kurang
   jelas.** Perbaiki naskahnya, jangan hanya membantah di response letter.
   Bila menolak saran, tolak dengan bukti/argumen kuat dan nada hormat.
3. **Komentar reviewer = daftar kelemahan gratis.** Bila diminta eksperimen
   tambahan yang masuk akal, kerjakan; hasilnya sering memperkuat paper.
4. **Persiapan sidang — kuasai setiap kata di naskah:** mampu menjelaskan
   setiap angka (dari run mana), setiap sitasi (pernah dibaca, bukan tempelan),
   setiap pilihan desain (mengapa X bukan Y), dan setiap batasan. Pertanyaan
   penguji paling umum: "mengapa metode ini?", "apa yang terjadi jika
   asumsi X dilanggar?", "apa kontribusi ilmiahnya dalam satu kalimat?",
   "apa bedanya dengan paper Z?".
5. **Siapkan slide cadangan** untuk pertanyaan yang bisa diantisipasi
   (Bagian 3 poin 5): ablasi detail, statistik lengkap, perbandingan dengan
   karya yang tidak masuk slide utama.
6. **Latih jawaban "tidak tahu" yang jujur:** "belum kami uji, tapi dugaan
   kami X karena Y" jauh lebih selamat daripada mengarang di depan penguji.

## 11. Checklist sebelum menyatakan selesai

- [ ] Dokumen ter-build bersih: 0 citation undefined, 0 error bibliografi.
- [ ] Semua entri bibliografi terverifikasi API (CrossRef/DataCite).
- [ ] Semua angka/klaim tertelusur ke data & run nyata; tidak ada fabrikasi.
- [ ] Deskripsi metode di teks == yang benar-benar dieksekusi.
- [ ] Frekuensi kata promosi & AI-tell sudah dicek (`grep -oic`).
- [ ] Tidak ada em-dash; tidak ada pembuka klausa formulaik berlebih.
- [ ] (Naskah Indonesia) Istilah konsisten & wajar, tanpa terjemahan harfiah
      kaku; ejaan sesuai KBBI/PUEBI.
- [ ] Semua figure dari skrip + data nyata; vektor/≥300 dpi; font terbaca;
      warna colorblind-safe; label+satuan lengkap; caption self-contained.
- [ ] Teks di gambar/tabel konsisten dengan body text dan lolos aturan de-AI;
      tidak ada diagram hasil AI generatif.
- [ ] Satu benang merah; abstrak beri angka; kontribusi bernomor dan
      terverifikasi di Results; limitations jujur; angka konsisten
      abstrak = body = kesimpulan.
- [ ] Bebas data leakage; baseline adil (matched-budget); mean ± SD/CI
      multi-seed; koreksi multiple comparisons; effect size dilaporkan;
      ablasi per komponen; biaya komputasi dilaporkan.
- [ ] Similarity dicek; format sesuai Guide for Authors; semua deklarasi
      (CRediT, COI, funding, ethics, data availability, penggunaan AI) ada;
      tidak dual submission.
- [ ] (Revisi) Semua komentar reviewer terjawab point-by-point dengan lokasi
      perubahan. (Sidang) Setiap angka, sitasi, dan pilihan desain bisa
      dipertanggungjawabkan lisan.
- [ ] Klaim tidak overclaim; antisipasi serangan reviewer sudah tertulis.

---

*Saripati dari `CLAUDE.md` repo RMA (paper IEEE) dan repo proposal disertasi.*
