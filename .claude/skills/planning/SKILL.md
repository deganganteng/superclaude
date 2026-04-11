# Writing Plans Skill

Distilled dari: https://github.com/obra/superpowers

## Kapan Digunakan
Sebelum implementasi **apapun** yang:
- Menyentuh lebih dari 1 file
- Estimasi > 30 menit
- Melibatkan perubahan arsitektur

**Announce:** "Membuat implementation plan untuk [fitur]"

---

## Prinsip Plan yang Baik

- **DRY** — Jangan repeat context
- **YAGNI** — Jangan implement yang belum perlu
- **TDD** — Setiap task mulai dari failing test
- **Bite-sized** — Setiap task 2-5 menit
- **Frequent commits** — Commit setelah setiap task selesai

---

## Format Plan

Simpan ke: `docs/plans/YYYY-MM-DD-<nama-fitur>.md`

```markdown
# [Nama Fitur] — Implementation Plan
**Tanggal:** YYYY-MM-DD
**Branch:** feature/nama-fitur
**Estimasi total:** X jam

## Context
[1-3 kalimat: kenapa fitur ini, apa yang dipecahkan]

## File Structure
| File | Status | Responsibility |
|------|--------|----------------|
| path/file.ext | NEW | Deskripsi |
| path/file2.ext | MODIFY | Deskripsi |

## Tasks

### Task 1: [Judul Singkat]
**File:** `path/to/file`
1. Tulis failing test untuk [behavior]
2. Run → confirm FAIL
3. Implement [minimal code]
4. Run test → confirm PASS
5. `git commit -m "feat: [pesan]"`

### Task 2: [Judul Singkat]
...

## Definition of Done
- [ ] Semua tests pass
- [ ] Review clean
- [ ] Docs updated jika perlu
```

---

## Task Granularity

**Terlalu besar:**
- "Implement auth system"
- "Build dashboard"

**Tepat:**
- "Buat model User dengan validasi email"
- "Implement login endpoint dengan JWT response"
- "Tambah middleware auth ke protected routes"

---

## Scope Check

Jika fitur cover multiple independent subsystems → **pisah menjadi beberapa plan**.

Setiap plan harus bisa produce working software secara mandiri.
