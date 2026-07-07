# instruction

Project Instructions

## Apa itu CLAUDE.md?

`CLAUDE.md` adalah file instruksi khusus yang dibaca secara otomatis oleh **Claude Code** setiap kali memulai sesi di sebuah project. File ini berfungsi sebagai "memori project" — tempat menyimpan konteks dan aturan yang perlu diketahui Claude agar dapat bekerja sesuai dengan konvensi project tersebut.

### Fungsi Utama

1. **Memberikan konteks project** — menjelaskan struktur codebase, arsitektur, dan teknologi yang digunakan, sehingga Claude tidak perlu menebak-nebak setiap kali memulai sesi baru.
2. **Menyimpan perintah-perintah penting** — misalnya cara build, menjalankan test, lint, atau deploy (contoh: `npm run build`, `pytest`, dll), agar Claude langsung menggunakan perintah yang benar.
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

### Tips Menulis CLAUDE.md yang Baik

- Tulis singkat dan spesifik — file ini dimuat ke context setiap sesi, jadi hindari isi yang bertele-tele.
- Fokus pada informasi yang **tidak bisa disimpulkan dari kode** (perintah khusus, aturan tim, keputusan desain).
- Perbarui secara berkala seiring berkembangnya project.
