# /debug — Systematic Debugging

Gunakan saat ada bug, error, test fail. JANGAN coba fix dulu sebelum root cause ditemukan.

## Instruksi untuk Claude Code

Ketika user menjalankan `/debug <deskripsi>`, ikuti **4 Phase** ini:

---

## IRON LAW
```
TIDAK ADA FIX TANPA ROOT CAUSE.
Jika belum selesai Phase 1, tidak boleh ke Phase 2.
```

---

## Phase 1: Root Cause Investigation

### 1.1 Baca error lengkap
- Jangan skip error message
- Baca stack trace dari atas ke bawah
- Catat: file name, line number, error type

### 1.2 Reproduce consistently
```bash
# Jalankan command yang trigger error
# Confirm error muncul konsisten
```

### 1.3 Isolate
- Cari baris kode yang jadi sumber masalah
- Minimal reproduction case

### 1.4 Trace dependencies
- Apa yang dipanggil sebelum error?
- Ada perubahan recent?
```bash
git log --oneline -10
git diff HEAD~1
```

### Output Phase 1:
Tulis diagnosis:
```
ROOT CAUSE IDENTIFIED:
- File: [path]
- Line: [nomor]
- Cause: [penjelasan clear]
- Type: [logic/syntax/dependency/env/race condition/dll]
```

---

## Phase 2: Fix Planning

Setelah root cause jelas:
1. Identifikasi minimal fix yang diperlukan
2. Pertimbangkan side effects
3. Tulis test yang akan catch bug ini
4. Baru implement fix

---

## Phase 3: Implementation & Verification

```bash
# Tulis failing test dulu
# Implement fix
# Run test → confirm fix works
# Run ALL tests → confirm nothing broken
```

**IRON LAW VERIFICATION:**
```
Tidak ada klaim "sudah fix" tanpa:
1. Test berjalan
2. Output dibaca lengkap
3. Zero failures dikonfirmasi
```

---

## Phase 4: Prevention

- Apakah ada test yang seharusnya catch ini?
- Apakah perlu tambah test coverage?
- Apakah ada kode serupa yang bisa punya bug sama?

---

## Log
```bash
echo "[$(date -Iseconds)] DEBUG: [deskripsi masalah]" >> .claude/logs/action-log.md
echo "[$(date -Iseconds)] ROOT_CAUSE: [penjelasan]" >> .claude/logs/action-log.md
echo "[$(date -Iseconds)] FIX: [apa yang diubah]" >> .claude/logs/action-log.md
```
