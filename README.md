# instruction

Kumpulan file *instruction* untuk task-task tertentu. Setiap folder berisi
`README.md` yang isinya siap dipakai sebagai `CLAUDE.md` (atau file
instruction AI lain) di project Anda.

## Daftar Instruction

| Folder | Task |
|--------|------|
| [`manuscript/`](manuscript/README.md) | Validasi integritas akademik penulisan ilmiah. Core universal ([`README.md`](manuscript/README.md)) + overlay per jenis naskah: [`journal.md`](manuscript/journal.md) untuk artikel jurnal bereputasi tinggi, [`proposal.md`](manuscript/proposal.md) untuk proposal penelitian/disertasi/tesis. Pakai: core + satu overlay |

## Konsep Umum: File *Instruction* untuk AI

***Instruction*** adalah file teks berisi instruksi, konteks, dan aturan project yang **selalu disertakan (di-inject) ke dalam setiap prompt** yang dikirim ke AI. Salah satu contoh implementasinya adalah `CLAUDE.md` di Claude Code. Konsep ini tidak terikat pada satu AI tertentu; setiap AI coding assistant punya nama filenya sendiri, tapi cara kerjanya sama:

| AI / Tool | Nama File Instruction |
|-----------|----------------------|
| Claude Code (Anthropic) | `CLAUDE.md` |
| GitHub Copilot | `.github/copilot-instructions.md` |
| Cursor | `.cursorrules` / `.cursor/rules/` |
| Gemini CLI (Google) | `GEMINI.md` |
| OpenAI Codex CLI | `AGENTS.md` |
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
