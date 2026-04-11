# Systematic Debugging Skill

Distilled dari: https://github.com/obra/superpowers

## Iron Law
```
TIDAK ADA FIX TANPA ROOT CAUSE.
Symptom fixes = failure.
```

## Kapan Digunakan
- Test failure
- Bug di production/development
- Unexpected behavior
- Performance problems
- Build failures

**Gunakan TERUTAMA saat:**
- Kamu sudah coba beberapa fix tapi gagal
- "Quick fix" terasa obvious (biasanya salah)
- Lagi under time pressure (rushing = rework)

---

## 4 Phase Process

### Phase 1: Root Cause Investigation

**Step 1: Baca error dengan teliti**
- Jangan skip error message apapun
- Baca stack trace lengkap dari atas ke bawah
- Catat: file, line number, error type, message exact

**Step 2: Reproduce**
```bash
# Jalankan command yang trigger error
# Pastikan error muncul konsisten
# Jika flaky — catat kapan muncul / tidak muncul
```

**Step 3: Isolate**
```bash
# Minimal reproduction
# Hapus semua yang tidak diperlukan
# Apakah error masih muncul?

git log --oneline -10  # Ada perubahan recent yang related?
git diff HEAD~1 -- [file yang suspect]
```

**Step 4: Trace**
- Apa yang terjadi sebelum error?
- Dependency apa yang terlibat?
- Environment variables? Database state?

**Output wajib sebelum lanjut:**
```
ROOT CAUSE:
- File: path/to/file.ext
- Line: XX
- Cause: [penjelasan clear satu kalimat]
- Type: [logic/syntax/type/null/race/env/dependency]
```

---

### Phase 2: Fix Planning

Setelah root cause JELAS:
1. Tentukan minimal fix (YAGNI — jangan over-engineer)
2. Pertimbangkan side effects
3. **Tulis failing test dulu** yang catch bug ini
4. Baru implement fix

---

### Phase 3: Implementation & Verification

```bash
# 1. Tulis test yang fail karena bug ini
# 2. Confirm test fail
# 3. Implement fix
# 4. Confirm test pass
# 5. Run SEMUA tests — pastikan tidak ada yang break
```

**Verification Iron Law:**
```
Tidak boleh klaim "sudah fix" tanpa:
1. Test dijalankan fresh (bukan dari memory)
2. Output dibaca LENGKAP
3. Zero failures dikonfirmasi dari output
```

---

### Phase 4: Prevention

- Apakah test coverage cukup?
- Ada kode serupa yang bisa punya bug sama?
- Perlu update dokumentasi?

---

## Common Mistake Patterns

| Pattern | Salah | Benar |
|---------|-------|-------|
| "Looks like a caching issue" | Clear cache langsung | Verify memang caching dulu |
| "Just try this fix" | Implement tanpa understand | Root cause dulu |
| "It was working yesterday" | Blame perubahan random | Git bisect untuk isolate |
| "Tests are flaky" | Skip test | Fix test, understand non-determinism |

---

## Debug Tools by Stack

### Flutter/Dart
```dart
debugPrint('Value: $variable');
assert(condition, 'Message');
// Flutter DevTools untuk widget tree
```

### Laravel/PHP
```php
\Log::debug('Value:', ['data' => $variable]);
dd($variable);  // dump and die
// Telescope untuk request/query inspection
```

### JavaScript/TypeScript
```js
console.log('Value:', variable);
debugger;  // breakpoint
// React DevTools untuk component state
```
