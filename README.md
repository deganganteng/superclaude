# 🧠 Claude Superstack

> Drop `.claude/` folder ini ke root project apapun → Claude Code langsung siap kerja dengan context penuh, semi-autonomous, dan terorganisir.

Distilled dari 5 repo terbaik:
- [obra/superpowers](https://github.com/obra/superpowers) — Subagent workflows, debugging, planning
- [affaan-m/everything-claude-code](https://github.com/affaan-m/everything-claude-code) — Documentation lookup, MCP patterns
- [nextlevelbuilder/ui-ux-pro-max-skill](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill) — UI/UX design intelligence
- [browser-use/browser-use](https://github.com/browser-use/browser-use) — Browser automation
- [thedotmack/claude-mem](https://github.com/thedotmack/claude-mem) — Cross-session memory via file-based context

---

## 📁 Struktur

```
.claude/
├── CLAUDE.md                    ← Otak utama — dibaca Claude Code pertama kali
├── PROJECT_CONTEXT.md           ← Konteks project spesifik (diisi via /project-init)
├── settings.json                ← Permissions Claude Code (semi-auto)
├── commands/
│   ├── project-init.md          ← /project-init  — auto-detect & setup project
│   ├── plan.md                  ← /plan <fitur>   — buat implementation plan
│   ├── debug.md                 ← /debug          — systematic debugging 4-phase
│   ├── review.md                ← /review         — code review sebelum commit
│   ├── status.md                ← /status         — ringkasan progress
│   ├── parallel.md              ← /parallel       — dispatch subagents paralel
│   └── browser.md               ← /browser        — browser automation
├── skills/
│   ├── ui-ux/SKILL.md           ← UI/UX Pro Max
│   ├── debugging/SKILL.md       ← Systematic Debugging
│   ├── planning/SKILL.md        ← Writing Plans
│   ├── planning/SUBAGENT.md     ← Subagent-Driven Development
│   └── memory/SKILL.md          ← Cross-session context
└── logs/
    └── action-log.md            ← Audit trail semua action Claude
```

---

## ⚡ Quickstart

### 1. Clone atau download

```bash
git clone https://github.com/waskito/claude-superstack.git
cp -r claude-superstack/.claude /path/to/project-kamu/
```

Atau download ZIP → extract → copy folder `.claude/` ke root project.

### 2. Buka project di Claude Code

```bash
cd project-kamu
claude
```

### 3. Inisialisasi context

```
/project-init
```

Claude akan auto-scan stack, framework, struktur folder, lalu generate `PROJECT_CONTEXT.md` yang relevan. Dari sini dia udah ngerti project kamu.

---

## 🤖 Behavior

### Semi-Autonomous Mode

| Action | Perlu Konfirmasi? |
|--------|:-----------------:|
| Baca file, jalankan bash, install deps | ❌ |
| Buat/edit file, run tests | ❌ |
| **Commit** (tunjukkan diff dulu) | ✅ |
| **Push** ke remote | ✅ |
| **Merge** ke main/master | ✅ |
| Delete file permanen | ✅ |

Sebelum commit, Claude akan tunjukkan diff dan propose pesan commit — kamu approve atau tolak.

### Action Logging

Semua action penting tercatat otomatis di `.claude/logs/action-log.md`:

```
[2025-01-15T10:23:01] INIT: Project context initialized via /project-init
[2025-01-15T10:35:12] PLAN: Created plan for auth-system at docs/plans/...
[2025-01-15T11:02:44] COMMIT_REQUEST: "feat: add JWT middleware" — awaiting approval
```

---

## 🛠️ Commands

Jalankan dengan `/nama` di Claude Code:

### `/project-init`
Auto-detect tech stack, framework, struktur folder, dan generate `PROJECT_CONTEXT.md`. Jalankan pertama kali di project baru.

### `/plan <nama-fitur>`
Buat implementation plan sebelum mulai coding. Simpan ke `docs/plans/YYYY-MM-DD-nama.md`.

Format output:
```markdown
# [Fitur] — Implementation Plan
## File Structure      ← file mana yang dibuat/diubah
## Tasks               ← bite-sized, TDD, dengan commit per task
## Definition of Done  ← checklist selesai
## Risks               ← potensi masalah + mitigasi
```

### `/debug <deskripsi>`
Systematic debugging 4-phase. **Tidak ada fix tanpa root cause** — ini iron law-nya.

```
Phase 1: Root Cause Investigation
Phase 2: Fix Planning
Phase 3: Implementation + Verification
Phase 4: Prevention
```

### `/review`
Code review sebelum commit. Cek functionality, code quality, testing, security.

### `/status`
Ringkasan cepat: git status, test results, open TODOs, recent actions.

### `/parallel <deskripsi tasks>`
Dispatch multiple subagents untuk independent tasks secara bersamaan.

### `/browser <url atau task>`
Browser automation via browser-use. Untuk scraping, UI testing, form automation.

---

## 🎓 Skills

Skills dibaca Claude secara otomatis saat relevan dengan task.

### UI/UX Pro Max
Triggered saat ada task design, komponen, atau styling. Berisi:
- Priority rules (accessibility → touch → performance → style → layout → typography → animation → forms)
- Stack-specific guidelines (Flutter, React/Next.js, Laravel)
- Anti-patterns yang sering terjadi

### Systematic Debugging
Triggered saat ada bug atau error. Iron law: **root cause dulu, baru fix**.

### Writing Plans
Triggered sebelum implementasi fitur apapun yang menyentuh >1 file.

### Subagent-Driven Development
Untuk task besar dengan multiple independent subtasks. Fresh subagent per task + two-stage review (spec compliance → code quality).

### Memory & Context
File-based memory untuk maintain konteks antar session. Update `PROJECT_CONTEXT.md` kalau ada perubahan besar di arsitektur.

---

## 🔄 Typical Workflow

### Fitur baru
```
/plan auth-system
→ Review plan
→ Claude implement per task (TDD)
→ Claude propose commit → kamu approve
→ /review sebelum merge
→ Push + merge manual
```

### Bug fix
```
/debug "login gagal setelah deploy"
→ Claude trace root cause
→ Claude fix + verify
→ Claude propose commit → kamu approve
```

### Mulai hari kerja
```
/status
→ Lihat apa yang terakhir dikerjakan
→ Lanjut dari situ
```

---

## 📋 PROJECT_CONTEXT.md

File ini adalah "memory" Claude tentang project kamu. Generate via `/project-init` atau isi manual:

```markdown
## 📦 Project Info
- Nama, Stack, Framework, Database

## 🏗️ Arsitektur
Ringkasan singkat sistem

## 📁 Folder Penting
Folder kunci dan fungsinya

## ⚙️ Setup & Run
Install, run dev, test commands

## 🎯 Fitur Utama
List fitur yang sudah ada

## 🔄 Konvensi Kode
Naming convention, code style

## 🚀 Next Steps
Apa yang sedang/akan dikerjakan
```

Update file ini setiap kali ada perubahan arsitektur signifikan.

---

## 🧩 Cara Adapt ke Project Kamu

Setelah `/project-init`, kamu bisa prompt Claude Code untuk sesuaikan lebih lanjut:

```
"Baca .claude/CLAUDE.md dan PROJECT_CONTEXT.md, 
lalu sesuaikan semua skills dan commands 
dengan stack [Flutter/Laravel/Next.js] yang aku pakai. 
Fokus ke [area tertentu misalnya: mobile UI, REST API, auth]."
```

Claude akan baca context yang ada dan sesuaikan behaviour-nya.

---

## ⚙️ Kustomisasi

### Ubah permissions
Edit `.claude/settings.json`. Default semi-auto (execute bebas, tanya sebelum commit).

Untuk **full auto** (termasuk commit otomatis):
```json
{
  "permissions": {
    "allow": ["Bash(*)", "Read(*)", "Write(*)", "Edit(*)", "MultiEdit(*)", "Glob(*)", "Grep(*)", "LS(*)", "TodoRead(*)", "TodoWrite(*)", "Task(*)", "WebFetch(*)", "WebSearch(*)", "mcp__github__create_pull_request", "mcp__github__push_files"],
    "deny": []
  }
}
```

### Tambah skill baru
Buat file baru di `.claude/skills/nama-skill/SKILL.md`, lalu daftarkan di tabel skill di `CLAUDE.md`.

### Tambah command baru
Buat file baru di `.claude/commands/nama-command.md` dengan format yang sama.

---

## 📌 Catatan

- **`.claude/logs/`** — jangan di-gitignore, ini audit trail yang berguna
- **`PROJECT_CONTEXT.md`** — commit ini ke repo, jadi tim lain bisa langsung `/project-init` juga
- **`settings.json`** — sesuaikan level autonomy per project (production vs side project)
- Folder ini kompatibel dengan **Claude Code** versi terbaru (mendukung `/commands` dan `settings.json`)

---

## 🙏 Credits

| Repo | Kontribusi |
|------|-----------|
| [obra/superpowers](https://github.com/obra/superpowers) | Subagent workflows, systematic debugging, writing plans, verification before completion |
| [affaan-m/everything-claude-code](https://github.com/affaan-m/everything-claude-code) | Documentation lookup patterns, MCP server integration |
| [nextlevelbuilder/ui-ux-pro-max-skill](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill) | UI/UX design intelligence, 50+ styles, accessibility rules |
| [browser-use/browser-use](https://github.com/browser-use/browser-use) | Browser automation concepts |
| [thedotmack/claude-mem](https://github.com/thedotmack/claude-mem) | Persistent memory patterns |

---

*Dibuat oleh Waskito Dehan — feel free to fork dan adapt.*
