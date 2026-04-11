# /status — Project Status Report

Ringkasan cepat progress project + recent actions.

## Instruksi untuk Claude Code

Ketika user menjalankan `/status`, generate laporan ini secara otomatis:

```bash
echo "=== GIT STATUS ==="
git status --short
git log --oneline -5
git branch

echo "=== TESTS ==="
# Jalankan test suite (disesuaikan stack)

echo "=== TODO/FIXME ==="
grep -r "TODO\|FIXME\|HACK\|XXX" --include="*.dart" --include="*.ts" --include="*.js" --include="*.php" --include="*.py" . --exclude-dir=node_modules --exclude-dir=.git 2>/dev/null | head -20

echo "=== RECENT ACTIONS ==="
tail -20 .claude/logs/action-log.md 2>/dev/null || echo "No action log found"
```

Format output final:
```
## 📊 Project Status — [tanggal]

### Git
- Branch: [branch saat ini]
- Last commit: [hash + message]
- Modified files: [jumlah]
- Untracked files: [jumlah]

### Tests
- Status: [X/X passing]
- Last run: [waktu]

### Open Issues
- [list TODO/FIXME yang ditemukan]

### Recent Actions (last 10)
[dari action-log.md]

### Next Steps
[Berdasarkan context, sarankan apa yang harus dikerjakan selanjutnya]
```
