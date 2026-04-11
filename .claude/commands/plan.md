# /plan — Implementation Plan Writer

Gunakan sebelum implementasi fitur apapun yang membutuhkan lebih dari 1 file.

## Instruksi untuk Claude Code

Ketika user menjalankan `/plan <nama-fitur>`, lakukan:

### Step 1: Announce
Tulis: "Membuat implementation plan untuk: [nama-fitur]"

### Step 2: Gather context
```bash
# Baca PROJECT_CONTEXT.md
cat .claude/PROJECT_CONTEXT.md 2>/dev/null

# Scan file relevan
# (berdasarkan nama fitur, cari file yang mungkin terlibat)
```

### Step 3: Write the plan

Simpan ke `docs/plans/YYYY-MM-DD-<nama-fitur>.md` dengan format:

```markdown
# [Nama Fitur] — Implementation Plan
**Tanggal:** YYYY-MM-DD
**Estimasi:** X jam
**Branch:** feature/nama-fitur

---

## Context
[Kenapa fitur ini dibuat, apa yang dipecahkan]

## File Structure
[File mana yang dibuat/dimodifikasi dan tanggung jawabnya]

| File | Status | Tanggung Jawab |
|------|--------|----------------|
| path/to/file.ext | NEW/MODIFY | Deskripsi singkat |

## Tasks

### Task 1: [Nama Task]
**File:** `path/to/file`
**Estimasi:** X menit

Steps:
1. Tulis failing test
2. Jalankan → confirm fail
3. Implement minimal code
4. Jalankan test → confirm pass
5. Commit: `feat: [deskripsi singkat]`

### Task 2: [Nama Task]
...

## Testing Checklist
- [ ] Unit tests
- [ ] Integration tests  
- [ ] Manual test flow

## Definition of Done
- [ ] Semua tests pass
- [ ] No console errors/warnings
- [ ] Code review clean
- [ ] Dokumentasi updated

## Risks & Mitigations
| Risk | Mitigation |
|------|-----------|
| [risiko] | [cara mitigasi] |
```

### Step 4: Log action
```bash
echo "[$(date -Iseconds)] PLAN: Created plan for [nama-fitur] at docs/plans/YYYY-MM-DD-[nama].md" >> .claude/logs/action-log.md
```

### Step 5: Ask
"Plan sudah dibuat di docs/plans/[nama-file]. Mau langsung mulai implementasi?"
