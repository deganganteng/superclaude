# Subagent-Driven Development Skill

Distilled dari: https://github.com/obra/superpowers

## Kapan Digunakan

Gunakan saat punya implementation plan dengan **multiple independent tasks** dan mau execute di session yang sama.

**Prasyarat:**
- Plan sudah ditulis
- Tasks mostly independent
- Tetap di session ini (bukan parallel session)

---

## Core Principle

```
Fresh subagent per task + two-stage review = quality fast
```

Setiap subagent dapat **fresh context** — jangan mewarisi history session ini. Kamu construct exactly apa yang mereka butuhkan.

---

## Process Per Task

```
1. Extract task text + context dari plan
2. Dispatch implementer subagent (fresh)
3. Subagent implement, test, self-review, commit
4. Dispatch spec compliance reviewer
5. Jika issues → implementer fix → reviewer re-review
6. Dispatch code quality reviewer
7. Jika issues → implementer fix → reviewer re-review
8. Mark task done di TodoWrite
9. Lanjut task berikutnya
```

---

## Model Selection

| Task Type | Model |
|-----------|-------|
| Isolated, clear spec, 1-2 files | Haiku (cheap) |
| Multi-file, integration concerns | Sonnet |
| Architecture, design, review | Opus |

---

## Subagent Statuses

| Status | Artinya | Action |
|--------|---------|--------|
| DONE | Selesai | Lanjut ke spec review |
| DONE_WITH_CONCERNS | Selesai + ada catatan | Baca concerns dulu |
| NEEDS_CONTEXT | Butuh info tambahan | Provide info, dispatch ulang |
| BLOCKED | Tidak bisa lanjut | Assess blocker, pecah task, atau eskalasi |

---

## Implementer Prompt Template

```
Kamu adalah implementer subagent untuk satu task spesifik.

PROJECT CONTEXT:
[isi dari .claude/PROJECT_CONTEXT.md]

TASK:
[full task text dari plan]

STACK:
[tech stack project]

INSTRUKSI:
1. Baca task dengan teliti
2. Tanya jika ada yang tidak jelas (SEBELUM mulai)
3. Implement dengan TDD
4. Self-review sebelum report
5. Commit dengan pesan conventional commits

JANGAN:
- Ubah file di luar scope task ini
- Skip writing tests
- Asumsi hal yang tidak disebutkan

Laporkan status: DONE / DONE_WITH_CONCERNS / NEEDS_CONTEXT / BLOCKED
```

---

## Red Flags — JANGAN Lakukan

- Start di branch main/master tanpa konfirmasi
- Skip spec review ATAU quality review
- Lanjut ke task berikutnya dengan review yang masih open issues
- Dispatch multiple implementers paralel (konflik!)
- Ignore subagent yang bilang BLOCKED
- Accept "close enough" dari spec reviewer

---

## Integration dengan Skills Lain

**Before:** Jalankan `skills/planning/SKILL.md` untuk buat plan

**During:** Setiap subagent pakai `skills/debugging/SKILL.md` jika ada bug

**After:** Jalankan `/review` untuk final code review
