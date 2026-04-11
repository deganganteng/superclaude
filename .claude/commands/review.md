# /review — Code Review Before Commit

Jalankan sebelum commit perubahan besar atau sebelum minta merge.

## Instruksi untuk Claude Code

Ketika user menjalankan `/review`, lakukan:

### Step 1: Get changes
```bash
git diff HEAD
git status
git log --oneline -5
```

### Step 2: Check each changed file

Untuk setiap file yang berubah, review:

**Functionality:**
- [ ] Logic benar dan handles edge cases
- [ ] Error handling ada dan proper
- [ ] Tidak ada hardcoded values yang seharusnya di-config

**Code Quality:**
- [ ] Naming jelas dan konsisten
- [ ] Tidak ada code yang duplikat (DRY)
- [ ] Tidak ada dead code
- [ ] Complexity tidak berlebihan

**Testing:**
- [ ] Ada test untuk perubahan ini
- [ ] Test cases cover happy path dan edge cases
- [ ] Tidak ada test yang di-skip tanpa alasan

**Security (jika relevan):**
- [ ] Input validation ada
- [ ] Tidak ada sensitive data di kode (API keys, passwords)
- [ ] SQL injection / XSS prevention

**Performance (jika relevan):**
- [ ] Tidak ada N+1 queries
- [ ] Tidak ada unnecessary re-renders (untuk React/Flutter)

### Step 3: Run tests
```bash
# Jalankan test suite
# (command disesuaikan dengan stack project)
```

### Step 4: Report

Format output:
```
## Code Review Report
**Files changed:** X
**Tests:** X/X passing

### ✅ Good
- [hal yang bagus]

### ⚠️ Suggestions (tidak blocking)
- [file.ext:line] - [saran improvement]

### ❌ Issues (harus fix sebelum commit)
- [file.ext:line] - [masalah yang harus difix]

### Verdict: APPROVE / NEEDS CHANGES
```

### Step 5: Log
```bash
echo "[$(date -Iseconds)] REVIEW: Code review completed — [APPROVE/NEEDS CHANGES]" >> .claude/logs/action-log.md
```
