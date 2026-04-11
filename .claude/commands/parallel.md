# /parallel — Dispatch Parallel Subagents

Gunakan saat ada 2+ task independen yang bisa dikerjakan bersamaan.

## Instruksi untuk Claude Code

Ketika user menjalankan `/parallel <deskripsi tasks>`, atau ketika kamu detect ada multiple independent tasks:

---

## Kapan Pakai

✅ **Gunakan parallel jika:**
- 2+ task independen (fix berbeda, fitur berbeda)
- Task tidak share state
- Bisa dikerjakan tanpa urutan

❌ **Jangan parallel jika:**
- Task tightly coupled (A harus selesai sebelum B)
- Task modify file yang sama
- Kamu belum punya plan

---

## Template Dispatch

```
Aku akan dispatch [N] subagent secara paralel:

Task 1: [Judul]
- Scope: [file/folder tertentu saja]
- Goal: [output yang diharapkan]
- Constraint: Jangan ubah file di luar scope ini

Task 2: [Judul]
- Scope: [file/folder tertentu saja]
- Goal: [output yang diharapkan]
- Constraint: Jangan ubah file di luar scope ini

[Task()] untuk masing-masing
```

---

## Penting

- Setiap subagent dapat **fresh context** — tidak mewarisi session ini
- Berikan **instruksi lengkap** ke setiap subagent (jangan asumsi mereka tahu)
- Setelah selesai, **review results** sebelum integrate
- Check untuk **konflik** antar perubahan

---

## Review Integration

Setelah subagent selesai:
```bash
git diff HEAD  # Lihat semua perubahan
git log --oneline -[N]  # Commit dari setiap subagent
```

Verifikasi:
- [ ] Tidak ada konflik
- [ ] Semua tests masih pass
- [ ] Output sesuai yang diharapkan

---

## Log
```bash
echo "[$(date -Iseconds)] PARALLEL: Dispatched [N] subagents for: [deskripsi]" >> .claude/logs/action-log.md
echo "[$(date -Iseconds)] PARALLEL_DONE: Results integrated" >> .claude/logs/action-log.md
```
