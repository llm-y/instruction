# Overlay: Pipeline SLR (Systematic Literature Review)

Overlay untuk sistem agentic yang mengorkestrasi **pipeline SLR** (PRISMA,
target publikasi Q1). **Pakai bersama [`README.md`](README.md) (core)** —
invariant HITL/xAI/neuro-symbolic, reproducible error, UX, dan debugging
ada di sana; file ini hanya menambah yang spesifik metodologi SLR.

> Prinsip payung: SLR yang *defensible* menuntut **protokol ditetapkan
> a priori dan diterapkan SERAGAM ke semua studi**. Ini pengetatan dari
> core Bagian 4 (stabilitas protokol): pada SLR, pelanggarannya bukan
> sekadar bug — ia **cacat metodologis** yang membatalkan validitas review.

---

## S1. Protokol a priori & amendemen (WAJIB)

1. **Protokol (PICO/pertanyaan riset, kriteria inklusi-eksklusi, strategi
   pencarian, skema ekstraksi) ditetapkan & TERSIMPAN sebelum screening
   dimulai** — sebagai data sesi yang bisa diedit user (core Bagian 1
   poin 4), bukan tertanam di prompt.
2. **Protokol yang berubah mengikuti data = HARKing** (red flag Q1).
   Framework/skema ekstraksi JANGAN di-regenerate saat set paper berubah;
   regenerasi hanya lewat **amendemen eksplisit** dari user.
3. **Amendemen protokol WAJIB terdokumentasi** (apa yang berubah, mengapa,
   kapan, atas keputusan siapa) dan diterapkan **SIMETRIS**: re-screening/
   re-ekstraksi ke SEMUA record dengan protokol baru — bukan hanya
   beberapa paper yang kebetulan menguntungkan.

## S2. Screening & keputusan studi (WAJIB)

1. **Setiap keputusan include/exclude melewati gate HITL** (core Bagian 1
   poin 1): AI menandai + memberi alasan, manusia memutuskan; pipeline
   tidak maju sebelum keputusan lengkap.
2. **Setiap flag AI mengutip klausa kriteria** yang menjadi dasarnya
   (xAI, core Bagian 1 poin 2) — bukan alasan generik "tidak relevan".
3. **Screening dua lapis (neuro-symbolic):** aturan deterministik dari
   kriteria tersimpan menangani kasus pasti (menjamin recall dan
   konsistensi), LLM menangani nuansa; hasil keduanya dibedakan di
   provenance.
4. **Setiap record yang dieksklusi pada tahap eligibility punya alasan
   tercatat** yang terpetakan ke kriteria — dibutuhkan untuk PRISMA dan
   pertanyaan reviewer "kenapa paper X tidak masuk?".

## S3. Hitungan PRISMA & audit trail (WAJIB)

1. **Hitungan PRISMA (identified → deduplicated → screened → eligible →
   included) dihitung dari DATA, bukan diketik manual**, dan diperbarui
   otomatis setiap keputusan berubah. Angka flow diagram harus selalu
   bisa direkonsiliasi dengan record aktual.
2. **Perubahan include/exclude pasca-ekstraksi dicatat beralasan** di
   audit trail. "Terasa sedikit" BUKAN justifikasi — melonggarkan
   kriteria post-hoc demi menggelembungkan N = selection bias.
3. **Ekstraksi inkremental:** data yang sudah diekstrak dipertahankan;
   ekstrak HANYA paper yang baru ter-include (LLM non-deterministik →
   re-ekstraksi paper tak berubah menggeser nilai → merusak
   reproducibility; core Bagian 4 poin 2).

## S4. Korpus, dedup & metadata (WAJIB)

1. **Dedup memakai ID kanonik (DOI; fallback title-similarity dengan
   ambang eksplisit)** dan dilakukan di **jalur ingest/tulis** — pada
   korpus shared lintas-user, JANGAN pernah menghapus ber-scope-sesi
   (core Bagian 1 poin 5). Waspadai paper sama mendapat ID internal beda
   antar-run (mis. hash file sebelum DOI ter-resolve vs ID berbasis DOI
   sesudahnya).
2. **Metadata studi diverifikasi ke sumber otoritatif** (CrossRef/DataCite
   by DOI) sebelum dipakai untuk dedup, screening, atau ekspor — jangan
   percaya metadata hasil ekstraksi PDF mentah.
3. **Kontrak field antar-komponen pipeline ditulis eksplisit** (nama field,
   kapitalisasi, key matching) — komponen ingestion dan komponen konsumen
   sering berbeda repo/bahasa; mismatch key = data "hilang" diam-diam.

## S5. Reproducibility untuk bagian Methods (WAJIB)

1. **Rekam parameter pencarian lengkap** per database: query string persis,
   database/sumber, tanggal eksekusi, filter, jumlah hasil — ini bahan
   langsung bagian Methods dan lampiran PRISMA-S.
2. **Semua artefak keputusan bisa diekspor** (kriteria, keputusan +
   alasan + provenance, hitungan PRISMA, log amendemen) supaya klaim di
   naskah tertelusur ke data pipeline (selaras instruction `manuscript/`
   Bagian 2).
3. **Atribusi model di ekspor:** provider + nama model + peran (screening/
   ekstraksi/sintesis) tercatat per keputusan — reviewer Q1 kini
   menanyakan peran AI dalam SLR; jawabannya harus dari data, bukan
   ingatan.

## S6. Checklist SLR

- [ ] Protokol lengkap tersimpan sebagai data sesi SEBELUM screening;
      tidak ada kriteria yang hidup hanya di prompt.
- [ ] Tidak ada regenerasi framework/skema diam-diam; semua amendemen
      terdokumentasi dan diterapkan simetris ke semua record.
- [ ] Semua keputusan include/exclude lewat gate HITL dengan kutipan
      klausa kriteria; eksklusi eligibility beralasan tercatat.
- [ ] Hitungan PRISMA dihitung dari data dan selalu rekonsiliasi dengan
      record; audit trail perubahan keputusan terisi beralasan.
- [ ] Ekstraksi inkremental (hanya paper baru); data lama tak tergeser.
- [ ] Dedup by-DOI di jalur ingest; aman lintas-tenant; kontrak field
      antar-komponen terdokumentasi.
- [ ] Query, sumber, tanggal, dan hasil pencarian terekam per database;
      semua artefak keputusan + atribusi model bisa diekspor.
