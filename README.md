# instruction

Kumpulan file *instruction* untuk task-task tertentu. Satu folder = satu
task: `README.md` di dalamnya adalah instruction inti (core) yang siap
dipakai sebagai `CLAUDE.md` (atau file instruction AI lain) di project
Anda; beberapa folder punya **overlay** — file tambahan per sub-jenis task
yang digabungkan dengan core saat dipakai.

## Untuk AI — pilih instruksi yang cocok secara otomatis

Bila pengguna hanya memberi tautan root ini tanpa memilih task — mis. *"sesuaikan dengan instruksi di https://ll.my.id/instruction/"* sambil menaruh dokumen di folder kerjanya — **lakukan ini lebih dulu, sebelum mengerjakan apa pun:**

1. **Periksa isi folder/dokumen pengguna** (jenis file, struktur, isi) untuk menentukan jenis pekerjaan.
2. **Pilih SATU baris** di tabel rute di bawah, lalu **ambil file core + overlay-nya** sebagai instruksi (cara ambil: lihat [Cara Memakai](#cara-memakai-tanpa-perlu-git); URL mentah `https://raw.githubusercontent.com/llm-y/instruction/main/{path}`).
3. **Bila ambigu, cocok >1, atau tak ada yang pas — TANYA pengguna.** Jangan menebak diam-diam, dan jangan menerapkan aturan yang tidak relevan dengan dokumennya.

| Ciri dokumen / pekerjaan pengguna | Ambil (core + overlay) |
|---|---|
| Artikel/naskah untuk **jurnal atau konferensi** (mis. `.tex`/`.docx` berstruktur IMRaD, ada abstrak & hasil) | `manuscript/README.md` + `manuscript/journal.md` |
| **Proposal** penelitian / disertasi / tesis (bab 1–3, rencana, belum ada hasil) | `manuscript/README.md` + `manuscript/proposal.md` |
| **Laporan** penelitian / akhir hibah / laporan teknis | `manuscript/README.md` + `manuscript/laporan.md` |
| **Capstone project** mahasiswa vokasi (proyek terapan integratif, ada mitra/requirement/uji terima, sering tim) | `manuscript/README.md` + `manuscript/capstone.md` |
| Naskah **buku ber-ISBN** (bab-bab buku, buku ajar, monograf, novel, antologi) | `buku/README.md` (+ `manuscript/README.md` bila ilmiah, + overlay template penerbit bila ada) |
| **Kode aplikasi/agen berbasis LLM** (pipeline screening, ekstraksi, review, sintesis) | `agentic/README.md` (+ `agentic/slr.md` bila pipeline SLR) |

Detail tiap task ada di tabel **Daftar Instruction** berikut.

## Daftar Instruction

| Folder | Task |
|--------|------|
| [`manuscript/`](manuscript/README.md) | Validasi integritas akademik penulisan ilmiah. Core universal ([`README.md`](manuscript/README.md)) + overlay per jenis naskah: [`journal.md`](manuscript/journal.md) untuk artikel jurnal bereputasi tinggi, [`proposal.md`](manuscript/proposal.md) untuk proposal penelitian/disertasi/tesis, [`laporan.md`](manuscript/laporan.md) untuk laporan penelitian/teknis, [`capstone.md`](manuscript/capstone.md) untuk laporan capstone project vokasi. Pakai: core + satu overlay |
| [`buku/`](buku/README.md) | Penyusunan buku ber-ISBN (buku ajar, monograf, referensi, umum, sastra): kelayakan ISBN (min 60 halaman isi, edar publik, bukan modul/tugas/laporan mentah), struktur front/main/back matter, narasi buku, self-review LAYAK/TIDAK LAYAK. Overlay: [`template-bukupedia.md`](buku/template-bukupedia.md) (spesifikasi LaTeX penerbit). Non-fiksi ilmiah: gabungkan `manuscript/README.md` |
| [`agentic/`](agentic/README.md) | Pembangunan sistem AI agentic: invariant HITL/xAI/neuro-symbolic/multi-tenant, reproducible error, UX operasi AI panjang, stabilitas protokol pipeline, debugging state-first, verifikasi deploy, model pengujian. Overlay: [`slr.md`](agentic/slr.md) untuk pipeline SLR (PRISMA) |

## Cara Memakai (tanpa perlu Git)

Anda **tidak perlu menginstal Git atau paham teknis.** Dari tabel di atas, pilih satu task, catat file **core**-nya dan (bila ada) **satu overlay**. Lalu pakai salah satu cara:

**1. Cukup berikan tautannya ke asisten AI (paling mudah).** Tempel tautan halaman core ke prompt AI Anda:

> tolong gunakan instruksi ini https://ll.my.id/instruction/manuscript/

Halaman itu adalah **core**; instruksi di dalamnya memberi tahu AI bahwa ia perlu **satu overlay** (mis. jurnal/proposal/laporan) dan cara mengambilnya. Agar makin pasti, sebutkan jenis naskahnya, atau tempel sekalian kedua tautan (core + overlay):

> Ikuti https://ll.my.id/instruction/manuscript/ dan https://ll.my.id/instruction/manuscript/journal.html sebagai aturan saat membantu naskah jurnal saya.

**2. Ambil file mentah via `curl`.** Tiap file tersedia sebagai markdown mentah. Gabungkan core + overlay menjadi satu file instruction (beri nama `CLAUDE.md`/`AGENTS.md`/`QWEN.md`/dst sesuai tool Anda):

```bash
curl -sL \
  https://raw.githubusercontent.com/llm-y/instruction/main/manuscript/README.md \
  https://raw.githubusercontent.com/llm-y/instruction/main/manuscript/journal.md \
  > CLAUDE.md
```

Pola URL mentah: `https://raw.githubusercontent.com/llm-y/instruction/main/{folder}/{file}` — ganti `{folder}/{file}` sesuai task Anda (mis. `buku/README.md`, `agentic/slr.md`).

**3. Unduh semua sekaligus (ZIP).** <https://github.com/llm-y/instruction/archive/refs/heads/main.zip>

## Konsep Umum: File *Instruction* untuk AI

***Instruction*** adalah file teks berisi instruksi, konteks, dan aturan project yang **selalu disertakan (di-inject) ke dalam setiap prompt** yang dikirim ke AI. Salah satu contoh implementasinya adalah `CLAUDE.md` di Claude Code. Konsep ini tidak terikat pada satu AI tertentu; setiap AI coding assistant punya nama filenya sendiri, tapi cara kerjanya sama:

| AI / Tool | Nama File Instruction |
|-----------|----------------------|
| Claude Code (Anthropic) | `CLAUDE.md` |
| GitHub Copilot | `.github/copilot-instructions.md` |
| Cursor | `.cursorrules` / `.cursor/rules/` |
| Gemini CLI (Google) | `GEMINI.md` |
| OpenAI Codex CLI | `AGENTS.md` |
| Qwen Code (Alibaba) | `QWEN.md`; `AGENTS.md` juga dibaca otomatis |
| Kiro (AWS) | *steering files*: `.kiro/steering/*.md` (project) atau `~/.kiro/steering/` (global); `AGENTS.md` juga dibaca otomatis |
| Google Antigravity (`agy` CLI) | `AGENTS.md` + `GEMINI.md` (root workspace); *rules* di `.agents/rules/*.md` (project) atau `~/.gemini/GEMINI.md` (global) |
| Windsurf | `.windsurfrules` |

Karena konsepnya sama untuk semua AI, dalam repo ini kita menyebutnya secara umum sebagai ***instruction*** saja.

## Cara Kerjanya

Cara kerja file instruction pada dasarnya sederhana:

1. **Saat sesi dimulai**, tool AI (misalnya Claude Code) mencari file instruction di lokasi-lokasi yang sudah ditentukan (root project, home directory pengguna, dll).
2. **Isi file dimuat ke dalam *context window*** — biasanya digabungkan ke dalam *system prompt* atau ditempatkan di awal percakapan, **sebelum** prompt/pertanyaan dari pengguna.
3. **Setiap prompt pengguna diproses dengan instruction ini sebagai konteks.** AI tidak "mengingat" file ini secara permanen — file ini dikirim ulang sebagai bagian dari context pada setiap sesi/request. Itulah mengapa disebut "di-inject di setiap prompt".
4. Karena selalu ada di context, AI konsisten mengikuti aturan project tanpa pengguna harus mengulang-ulang instruksi yang sama.

Secara konseptual, request yang sampai ke model kira-kira berbentuk:

```text
[System Prompt bawaan tool]
[Isi file instruction / CLAUDE.md]   ← di-inject otomatis
[Riwayat percakapan]
[Prompt terbaru dari pengguna]
```

## Menggunakan Instruction dengan API Lain

Karena file instruction hanyalah teks biasa, kita bisa memakai pola yang sama saat memanggil **API AI apa pun** secara langsung — cukup baca isi filenya lalu sertakan sebagai *system prompt*. Contoh dengan Python:

```python
# Baca file instruction
with open("CLAUDE.md") as f:
    instruction = f.read()

# --- Contoh dengan Anthropic API ---
import anthropic
client = anthropic.Anthropic()
response = client.messages.create(
    model="claude-sonnet-5",
    max_tokens=1024,
    system=instruction,  # instruction di-inject sebagai system prompt
    messages=[{"role": "user", "content": "Buatkan endpoint login"}],
)

# --- Contoh dengan OpenAI API ---
from openai import OpenAI
client = OpenAI()
response = client.chat.completions.create(
    model="gpt-4o",
    messages=[
        {"role": "system", "content": instruction},  # instruction di-inject
        {"role": "user", "content": "Buatkan endpoint login"},
    ],
)
```

Dengan pola ini, satu file instruction yang sama bisa dipakai oleh Claude Code, API Anthropic, API OpenAI, Gemini, model lokal (Ollama), atau tool AI lainnya — instruction menjadi **satu sumber kebenaran (single source of truth)** untuk aturan project, apa pun AI-nya.

### Contoh: Kiro (kiro.dev)

Di [Kiro](https://kiro.dev) milik AWS, instruction disebut ***steering files***: file markdown di `.kiro/steering/` yang di-inject ke context agent. Cara memakai instruction dari repo ini:

```bash
# dari root project Anda
mkdir -p .kiro/steering
cp path/ke/instruction/manuscript/README.md  .kiro/steering/manuscript-core.md
cp path/ke/instruction/manuscript/journal.md .kiro/steering/manuscript-journal.md
```

Secara default steering file selalu disertakan (*always included*). Mode inklusi bisa diatur lewat front matter di awal file, misalnya hanya dimuat saat file tertentu disentuh:

```markdown
---
inclusion: fileMatch
fileMatchPattern: "**/*.tex"
---
# Instruction: Integritas Akademik Penulisan Ilmiah
...
```

Alternatif: Kiro juga otomatis membaca `AGENTS.md` di root workspace, jadi menaruh gabungan instruction sebagai `AGENTS.md` juga berfungsi (sekaligus terbaca oleh tool lain yang mendukung standar `AGENTS.md`, seperti OpenAI Codex).

### Contoh: OpenAI Codex CLI

Di [Codex CLI](https://github.com/openai/codex) milik OpenAI, instruction ditaruh di file `AGENTS.md` yang dibaca otomatis dan **digabung berlapis** dari yang paling umum ke paling spesifik. Karena pola pakai repo ini adalah core + satu overlay, gabungkan keduanya menjadi satu `AGENTS.md`:

```bash
# dari root project Anda — gabung core + satu overlay jadi AGENTS.md
cat path/ke/instruction/manuscript/README.md \
    path/ke/instruction/manuscript/journal.md > AGENTS.md
```

Codex memuat `AGENTS.md` dari beberapa lokasi sekaligus (yang lebih spesifik menimpa yang umum):

| Lokasi | Cakupan |
|--------|---------|
| `~/.codex/AGENTS.md` | global, berlaku untuk semua project |
| `AGENTS.md` (root repo) | seluruh project, biasanya di-commit ke git |
| `AGENTS.md` (subfolder) | dimuat saat Codex bekerja di folder tersebut |

Karena `AGENTS.md` sudah menjadi standar bersama (dibaca juga oleh Kiro dan tool lain), satu file gabungan ini bisa dipakai lintas-tool tanpa menyalin ulang.

### Contoh: Google Antigravity (`agy` CLI)

[Antigravity](https://antigravity.google) milik Google membaca `AGENTS.md` (dan `GEMINI.md`) di root workspace — sama seperti Codex, jadi file `AGENTS.md` gabungan yang sama bisa langsung dipakai:

```bash
# dari root project Anda — gabung core + satu overlay jadi AGENTS.md
cat path/ke/instruction/buku/README.md \
    path/ke/instruction/buku/template-bukupedia.md > AGENTS.md

# periksa file konteks yang benar-benar dimuat sebelum agent bekerja
agy inspect
```

Sebagai alternatif khusus Antigravity, instruction bisa ditaruh sebagai *rules*:

| Lokasi | Cakupan |
|--------|---------|
| `~/.gemini/GEMINI.md` | rules global, berlaku untuk semua project |
| `.agents/rules/*.md` | rules khusus project ini (workspace) |
| `AGENTS.md` (root workspace) | konteks project, standar lintas-tool |

Perintah `agy inspect` menampilkan konfigurasi yang termuat (`.agents/`, `AGENTS.md`, instruksi project), berguna untuk memastikan instruction sudah terbaca.

## Apa itu CLAUDE.md?

`CLAUDE.md` adalah implementasi konsep instruction di atas pada **Claude Code**: file yang dibaca secara otomatis setiap kali memulai sesi di sebuah project. File ini berfungsi sebagai "memori project" — tempat menyimpan konteks dan aturan yang perlu diketahui Claude agar dapat bekerja sesuai dengan konvensi project tersebut.

### Fungsi Utama

1. **Memberikan konteks project** — menjelaskan struktur codebase, arsitektur, dan teknologi yang digunakan, sehingga AI tidak perlu menebak-nebak setiap kali memulai sesi baru.
2. **Menyimpan perintah-perintah penting** — misalnya cara build, menjalankan test, lint, atau deploy (contoh: `npm run build`, `pytest`, dll), agar AI langsung menggunakan perintah yang benar.
3. **Menetapkan konvensi dan aturan coding** — gaya penulisan kode, penamaan variabel, pola arsitektur, atau library yang wajib/dilarang dipakai.
4. **Mencatat hal-hal yang tidak terlihat dari kode** — keputusan desain, batasan (constraints), atau peringatan khusus (misalnya "jangan ubah file X secara langsung").

### Lokasi File

`CLAUDE.md` dapat ditempatkan di beberapa lokasi dengan cakupan yang berbeda:

| Lokasi | Cakupan |
|--------|---------|
| `./CLAUDE.md` (root project) | Berlaku untuk seluruh project, biasanya di-commit ke git agar dipakai bersama tim |
| `./CLAUDE.local.md` | Instruksi pribadi untuk project ini, tidak di-commit ke git |
| `~/.claude/CLAUDE.md` | Instruksi global yang berlaku untuk semua project di komputer pengguna |
| Subdirektori (misal `src/CLAUDE.md`) | Instruksi tambahan yang dimuat saat Claude bekerja di direktori tersebut |

### Cara Membuat

File ini bisa dibuat secara manual, atau dibuat otomatis dengan menjalankan perintah `/init` di dalam sesi Claude Code — Claude akan menganalisis codebase dan menghasilkan `CLAUDE.md` awal secara otomatis.

### Tips Menulis Instruction yang Baik

- Tulis singkat dan spesifik — file ini dimuat ke context setiap sesi, jadi hindari isi yang bertele-tele (menghemat token dan menjaga fokus AI).
- Fokus pada informasi yang **tidak bisa disimpulkan dari kode** (perintah khusus, aturan tim, keputusan desain).
- Perbarui secara berkala seiring berkembangnya project.
