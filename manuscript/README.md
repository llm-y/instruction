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

## 6. Checklist sebelum menyatakan selesai

- [ ] Dokumen ter-build bersih: 0 citation undefined, 0 error bibliografi.
- [ ] Semua entri bibliografi terverifikasi API (CrossRef/DataCite).
- [ ] Semua angka/klaim tertelusur ke data & run nyata; tidak ada fabrikasi.
- [ ] Deskripsi metode di teks == yang benar-benar dieksekusi.
- [ ] Frekuensi kata promosi & AI-tell sudah dicek (`grep -oic`).
- [ ] Tidak ada em-dash; tidak ada pembuka klausa formulaik berlebih.
- [ ] (Naskah Indonesia) Istilah konsisten & wajar, tanpa terjemahan harfiah
      kaku; ejaan sesuai KBBI/PUEBI.
- [ ] Klaim tidak overclaim; antisipasi serangan reviewer sudah tertulis.

---

*Saripati dari `CLAUDE.md` repo RMA (paper IEEE) dan repo proposal disertasi.*
