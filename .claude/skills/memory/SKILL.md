# Memory & Context Skill

Distilled dari: https://github.com/thedotmack/claude-mem

## Tujuan

Maintain konteks penting **antar session** tanpa harus explain ulang dari awal.

---

## Cara Kerja

Claude Code tidak punya memory bawaan antar session. Skill ini menggunakan file-based memory di `.claude/` sebagai persistent context.

---

## Files yang Dikelola

| File | Isi | Update kapan |
|------|-----|-------------|
| `PROJECT_CONTEXT.md` | Stack, arsitektur, setup | Saat ada perubahan besar |
| `logs/action-log.md` | Semua action yang dilakukan | Otomatis setiap action |
| `logs/decisions.md` | Architecture decisions | Saat ada keputusan penting |
| `logs/session-summary.md` | Ringkasan tiap session | Di akhir session panjang |

---

## Format Decision Log

Saat membuat keputusan arsitektur penting, catat di `logs/decisions.md`:

```markdown
## [YYYY-MM-DD] [Judul Keputusan]

**Konteks:** Apa situasinya
**Keputusan:** Apa yang dipilih
**Alasan:** Kenapa ini dipilih vs alternatif
**Dampak:** File/sistem apa yang terpengaruh
**Trade-offs:** Apa yang dikompromikan
```

---

## Format Session Summary

Di akhir session panjang (opsional tapi berguna), simpan ke `logs/session-summary.md`:

```markdown
## Session [YYYY-MM-DD HH:MM]

### Apa yang dikerjakan
- [task 1]
- [task 2]

### Status
- [fitur X]: DONE / IN PROGRESS / BLOCKED

### Keputusan yang dibuat
- [keputusan penting]

### Untuk session berikutnya
- [hal yang perlu dilanjutkan]
- [context yang perlu diingat]
```

---

## Cara Pakai di Awal Session

Saat mulai session baru di project yang sudah ada:

```
1. Claude baca CLAUDE.md (otomatis)
2. Claude baca PROJECT_CONTEXT.md
3. Claude baca logs/session-summary.md (jika ada)
4. Claude baca logs/action-log.md (10 entry terakhir)
5. Siap kerja dengan full context
```

---

## Tips

- Jangan hapus `action-log.md` — ini audit trail
- Update `PROJECT_CONTEXT.md` kalau stack berubah (misal tambah package besar)
- Session summary sangat berguna untuk project yang dikerjakan selama berhari-hari
