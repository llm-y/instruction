# Instruction: Pembangunan Sistem AI Agentic

Instruction untuk AI saat membangun atau memelihara **sistem AI agentic** —
aplikasi yang memakai LLM untuk membantu keputusan manusia (pipeline
screening, ekstraksi, sintesis, review, dsb). Salin sebagai `CLAUDE.md`
(atau file instruction AI lain) di repo sistem Anda, sesuaikan bagian
bertanda `{...}`.

**Cara pakai:** file ini (core) berlaku untuk semua sistem agentic;
tambahkan overlay bila jenis pipeline-nya cocok.

| Jenis sistem | File yang digabung |
|--------------|--------------------|
| Sistem agentic umum | `README.md` saja |
| Pipeline SLR (systematic literature review) | `README.md` + [`slr.md`](slr.md) |

---

## 1. Empat invariant arsitektur (WAJIB untuk fitur yang menyentuh keputusan penting)

Setiap fitur yang menyentuh **keputusan penting user** (menerima/menolak,
mengklasifikasi, mengekstrak, menyimpulkan) WAJIB memenuhi:

1. **HITL (Human-in-the-Loop):** AI **mengusulkan/menandai**, MANUSIA
   **memutuskan**. Jangan auto-apply keputusan penting tanpa konfirmasi
   manusia. Sediakan **gate** yang memblok kemajuan pipeline sampai
   keputusan manusia lengkap.
2. **xAI (Explainable):** setiap flag/keputusan AI membawa **provenance**
   yang bisa diaudit — sumber sinyal, bukti, dan **klausa kriteria yang
   dikutip** — tersimpan dan bisa diekspor. Output AI selalu menyertakan
   **atribusi model** (provider + NAMA model asli, bukan hanya provider,
   karena satu provider bisa punya banyak model).
3. **Neuro-Symbolic:** gabungkan **aturan simbolik deterministik**
   (diturunkan dari definisi/kriteria yang TERSIMPAN dan bisa diedit user)
   DENGAN **penilaian neural (LLM)**. Aturan menjamin konsistensi pada
   kasus pasti; LLM menangani nuansa. **LLM bukan satu-satunya hakim.**
4. **Konfigurasi dari DATA, bukan hardcode (multi-tenant):** sistem dipakai
   banyak user dengan kebutuhan berbeda. SEMUA kriteria/aturan/ambang HARUS
   berasal dari **data sesi/konfigurasi yang bisa diedit user** — JANGAN
   menanam aturan spesifik-kasus di kode atau prompt. Butuh aturan baru →
   beri **mekanisme edit (HITL)** + simpan di data.

Plus satu prinsip pemulihan data:

5. **Self-heal, BUKAN edit database manual:** koreksi data dilakukan lewat
   **aksi UI normal**; JANGAN pernah menyuruh user mengedit database
   langsung. State tak-konsisten/legacy harus **pulih sendiri** saat operasi
   rutin. Jaga **invariant di SETIAP titik tulis**: bila dua field
   saling-eksklusif, set satu → clear lawannya. Pada data **shared
   lintas-user**, self-heal harus memakai kunci yang aman lintas-tenant
   (mis. dedup by-ID kanonik di jalur tulis), BUKAN penghapusan
   ber-scope-sesi yang bisa menghapus data user lain.

## 2. Reproducible error — setiap kegagalan LLM WAJIB bisa direproduksi user (xAI)

Setiap error yang melibatkan LLM/provider WAJIB bisa diproduksi-ulang oleh
USER langsung dari UI (tanpa akses server/DB/log developer), agar laporan
bug langsung *actionable*:

1. **Tangkap jejak LENGKAP saat call LLM gagal:** `{step, role, provider,
   NAMA model, system prompt LENGKAP, user prompt LENGKAP, error mentah,
   durasi, estimasi token, timestamp}`. Simpan di store khusus terbatas
   (mis. last-failed per sesi) — jangan gemukkan log audit utama dengan
   full-text.
2. **Sediakan REPLAY dari UI:** endpoint + tombol yang mengirim ULANG prompt
   asli (boleh diedit) ke provider, lalu tampilkan **respons mentah/error
   apa adanya** + timing. Inilah cara pinpoint akar: context overflow,
   JSON rusak, 429, 401, base URL salah.
3. **Redaksi rahasia:** API key/secret TIDAK pernah ikut di payload
   debug/replay yang dikirim ke klien (redact `***`).
4. **Pesan error self-explanatory + actionable:** sebut NAMA model, dugaan
   akar masalah, dan langkah perbaikan — user paham tanpa membaca kode.
5. **JANGAN telan error diam-diam:** `catch {}` / log-saja tanpa surfacing
   ke UI melanggar invariant ini — user tak bisa melaporkan apa yang tak
   terlihat.
6. **Pesan error yang benar di backend TAK berguna bila UI tak
   menampilkannya.** Verifikasi error benar-benar **surface di UI
   end-to-end**: setiap status/state error harus punya cabang render yang
   menampilkannya secara jelas dan recoverable — bukan jatuh ke tampilan
   pasif yang menelan pesannya.

## 3. UX operasi AI yang lama (WAJIB untuk semua aksi ber-LLM)

1. **JANGAN proses sinkron-lama di handler HTTP** (risiko timeout proxy).
   Pola: handler memulai **job background**, balas segera
   `{started, total}`, frontend **poll** endpoint hasil berkala.
2. **Progress per-item ke live log** yang bisa dilihat user: log mulai,
   tiap item (`Item i/N: <nama>`), dan selesai — user tahu proses jalan
   dan sedang di mana.
3. **Umpan-balik mulai & selesai** (toast/status, bukan `alert()`):
   "AI menganalisis N item…" → "✅ N hasil via <model>".
4. **Anti dobel-eksekusi dua lapis:** tombol di-disable saat diklik dengan
   progres di teksnya, PLUS **guard server** (job in-flight → tolak job
   baru).
5. **Deteksi stall:** job macet yang hanya tampak "spinner abadi" membuat
   user menyimpulkan hang. Beri sinyal no-progress (mis. tak ada log baru
   dalam X menit) dan jalan keluar yang jelas.

## 4. Stabilitas protokol & determinisme pipeline (WAJIB untuk pipeline multi-tahap)

LLM non-deterministik — desain pipeline harus melindungi konsistensi hasil:

1. **Artefak protokol (kriteria, skema ekstraksi, framework) ditetapkan di
   awal dan JANGAN di-regenerate diam-diam** saat data berubah. Item yang
   diproses sebelum vs sesudah dengan protokol berbeda = hasil tak
   konsisten. Regenerasi hanya boleh atas **permintaan eksplisit user**
   (amendemen yang disengaja), dan saat itu WAJIB re-proses SEMUA item
   secara seragam.
2. **Default koreksi = PRESERVE, bukan reset.** Hasil yang sudah terkumpul
   dipertahankan; proses HANYA item yang baru/berubah (inkremental).
   Re-proses item yang tak berubah menggeser nilainya tanpa alasan.
3. **Tombol reset/wipe penuh dipisahkan tegas dari koreksi biasa:** label +
   konfirmasi eksplisit yang menjelaskan konsekuensinya. Jangan biarkan
   "balik sedikit" memicu wipe destruktif.
4. **Audit trail untuk setiap perubahan keputusan:** catat alasan tiap
   koreksi pasca-proses (provenance/xAI) dan perbarui hitungan/statistik
   turunannya. Perubahan kriteria = amendemen terdokumentasi + penerapan
   **simetris ke semua item**, bukan hanya yang menguntungkan.

## 5. Debugging & ketahanan (WAJIB saat menangani "kok tidak berubah / gagal")

1. **CEK STATE DATABASE DULU sebelum menyalahkan deploy/cache/server.**
   Urutan: (1) lihat dokumen/row aktual — field-nya benar berubah?
   (2) cek logika persistence — apakah nilai zero (nil/false/`""`/0)
   benar-benar tersimpan, atau dibuang diam-diam oleh serializer
   (mis. `omitempty` + `$set` yang tak meng-clear nilai lama)?
   (3) cek log runtime — langkahnya dijalankan atau di-skip?
   (4) BARU curigai deploy/cache/CI (cek versi/commit yang live).
2. **Ketahanan > timeout galak di jalur baca yang sering dipanggil.**
   Koneksi eksternal (DB remote, API) bisa flaky; timeout ketat mengubah
   "lambat sesaat" jadi error keras palsu. Obatnya: **retry pada error
   transien** di backend, dan di frontend yang nge-poll: jangan tampilkan
   panel error pada kegagalan PERTAMA — hanya setelah gagal beruntun
   (mis. ≥3), reset saat sukses. Timeout untuk anti-hang; retry/toleransi
   untuk anti-false-failure.
3. **Bedakan tiga kondisi: ADA / TERKONFIRMASI-ABSEN / UNKNOWN.** Pesan
   "hilang/gagal" pada kondisi yang belum pasti lebih buruk dari diam —
   user diarahkan ke tindakan destruktif yang salah. Jangan sarankan
   perbaikan destruktif saat status hanya "unknown".

## 6. Verifikasi deploy sebelum mengklaim fix live (WAJIB)

1. **"Build hijau" ≠ "sudah live".** Sebelum memberi tahu user bahwa fix
   tersedia: verifikasi **artefak yang benar-benar tersaji** — versi/commit
   di endpoint live, atau grep stamp versi di binary/file yang diunduh
   user. API status deploy bisa lag; bukti definitif adalah isi artefak
   live itu sendiri.
2. **Stamp versi saat build** (commit SHA via ldflags/env/build-arg) dan
   sediakan **endpoint versi** (mis. `GET /api/version`) — tanpa ini,
   laporan bug tak bisa dipetakan ke kode yang benar.
3. **Pikirkan jalur distribusi user:** bila user menjalankan komponen
   secara lokal, push ke repo saja TIDAK cukup — beri tahu langkah user
   (unduh ulang, hard-refresh) dan verifikasi artefak distribusinya
   ter-update.

## 7. Setiap laporan bug = sinyal UX (WAJIB saat menangani tiket)

Tiap laporan bug biasanya menandai DUA kegagalan: bug teknis, DAN celah UX
yang membuat user terpaksa melapor. Setelah memperbaiki akar teknis, WAJIB
tanya: *"kenapa user sampai harus melapor? bisakah UX membuatnya
swa-jelas / bisa-pulih / tercegah?"* — lalu tutup celah itu. Tiga mode
kegagalan UX yang berulang:

1. **Reaktif → proaktif:** kegagalan mahal (provider rusak/rate-limited)
   baru ketahuan setelah user investasi waktu lama. Sediakan **pre-flight
   check** sebelum operasi panjang; validasi konfigurasi sebelum commit.
2. **State diam → terlihat:** lihat aturan deteksi stall (Bagian 3).
3. **Pesan menyesatkan → jujur:** hint yang salah atau klaim gagal pada
   kondisi UNKNOWN mengarahkan user ke tindakan salah (lihat Bagian 5).

Lengkapi juga **bekal reproduksi di laporan bug** agar tanpa tanya-balik:
error console frontend (ring-buffer), versi backend & frontend, snapshot
state (tanpa rahasia), dan screenshot UI otomatis. Laporan harus
**swasembada** — developer tidak butuh akses ke database/mesin user.

## 8. Model pengujian: "siap diuji" ≠ "selesai" (WAJIB)

1. Korektnya **perilaku** TIDAK bisa diklaim hanya dari unit test + build
   hijau. **User = tester manusia nyata** yang menjalankan alur sungguhan.
2. Setelah implementasi: jalankan build + unit test + verifikasi mekanis
   yang relevan, lalu nyatakan **"siap diuji"** — BUKAN "selesai/matang".
3. **"Selesai" hanya setelah user menjalankan tes nyata** dan hasilnya
   sesuai. Bedakan unit test (komponen) dari verifikasi perilaku
   end-to-end (butuh user).

## 9. Checklist sebelum menyatakan siap diuji

- [ ] Keputusan penting lewat gate HITL; tidak ada auto-apply diam-diam.
- [ ] Setiap keputusan AI membawa provenance + atribusi provider & nama
      model; bisa diaudit/diekspor.
- [ ] Kriteria/aturan/ambang dari data yang bisa diedit user; tidak ada
      yang di-hardcode di kode/prompt.
- [ ] Kegagalan LLM tertangkap lengkap (prompt penuh + error mentah) dan
      bisa di-replay dari UI; rahasia ter-redact.
- [ ] Tidak ada error yang ditelan; semua status error punya cabang render
      di UI yang jelas dan recoverable.
- [ ] Operasi lama = job background + poll + progress per-item + anti
      dobel-eksekusi dua lapis + deteksi stall.
- [ ] Artefak protokol tidak ter-regenerate diam-diam; koreksi berjalur
      PRESERVE/inkremental; audit trail perubahan keputusan terisi.
- [ ] Jalur baca yang sering dipanggil tahan koneksi flaky (retry transien,
      toleransi gagal-pertama di poller).
- [ ] Versi ter-stamp di build + endpoint versi tersedia; klaim "fix live"
      hanya setelah artefak live terverifikasi.
- [ ] Root cause DAN celah UX-nya sama-sama ditutup untuk tiap tiket.
- [ ] Dinyatakan "siap diuji", bukan "selesai", sampai user memverifikasi.

---

*Saripati dari `CLAUDE.md` repo nsa (sistem SLR agentic: backend Go +
frontend HITL + pipeline ingestion).*
