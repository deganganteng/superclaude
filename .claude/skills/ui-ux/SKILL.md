# UI/UX Pro Max Skill

Distilled dari: https://github.com/nextlevelbuilder/ui-ux-pro-max-skill

## Kapan Digunakan

**WAJIB gunakan skill ini saat:**
- Design halaman baru (landing page, dashboard, admin, SaaS, mobile app)
- Buat atau refactor UI component (button, modal, form, table, chart)
- Pilih color scheme, typography, spacing, layout
- Review UI code untuk UX, aksesibilitas, atau konsistensi visual
- Implement navigasi, animasi, responsive behavior

**SKIP jika:** pure backend, API only, database design, DevOps

---

## Priority Rules (Ikuti urutan ini)

### 1. Aksesibilitas (CRITICAL)
- Contrast minimum **4.5:1** untuk teks normal, 3:1 untuk teks besar
- Focus rings visible pada semua interactive elements
- Alt text untuk semua gambar bermakna
- Aria-labels untuk icon-only buttons
- Tab order sesuai visual order
- Jangan convey info via warna saja (tambah icon/text)

### 2. Touch & Interaction (CRITICAL)
- Minimum touch target: **44×44px**
- Spacing antar touch targets: **8px minimum**
- Loading feedback untuk setiap async action
- Jangan rely on hover-only interactions

### 3. Performance (HIGH)
- Gunakan WebP/AVIF untuk images
- Lazy loading untuk off-screen content
- Reserve space untuk images (hindari CLS)

### 4. Style Selection (HIGH)
- Match style dengan product type
- Konsisten dalam satu project (jangan mix flat + skeuomorphic)
- Gunakan SVG icons, bukan emoji

### 5. Layout & Responsive (HIGH)
- **Mobile-first** breakpoints
- Tidak ada horizontal scroll
- Viewport meta tag
- Container width dalam % atau rem, bukan px fixed

### 6. Typography & Color (MEDIUM)
- Base font size: **16px**
- Line-height: **1.5** untuk body text
- Jangan pakai teks < 12px untuk body
- Semantic color tokens (jangan raw hex di komponen)

### 7. Animation (MEDIUM)
- Duration: **150-300ms** untuk micro-interactions
- Animasi harus convey meaning, bukan dekoratif saja
- Support `prefers-reduced-motion`

### 8. Forms & Feedback (MEDIUM)
- Label visible (bukan placeholder saja)
- Error message dekat field yang error
- Helper text untuk input yang kompleks

---

## Stack-Specific Guidelines

### Flutter
```dart
// Touch targets
SizedBox(width: 44, height: 44, child: ...)
// Colors
Theme.of(context).colorScheme.primary  // bukan Color(0xFF...)
// Responsive
MediaQuery.of(context).size.width
LayoutBuilder(builder: (context, constraints) {...})
```

### React/Next.js
```tsx
// Accessible button
<button aria-label="Close dialog" onClick={onClose}>
  <XIcon />
</button>
// Color tokens (Tailwind)
className="text-primary bg-surface"  // bukan text-[#2D6A4F]
```

### Laravel (Blade/Livewire)
```html
<!-- Accessible form -->
<label for="email">Email</label>
<input id="email" type="email" aria-describedby="email-hint">
<small id="email-hint">Contoh: user@email.com</small>
```

---

## Color Palette Quick Reference

Untuk project Waskito (Rumah Belajar GEMA / PasarLokal):
- Primary: `#2D6A4F` (Emerald Harvest)
- Gunakan tints/shades: 10%, 20%, 40%, 60%, 80%
- Semantic: success=#27AE60, warning=#F39C12, error=#E74C3C

---

## Anti-Patterns yang Sering Terjadi

❌ `color: gray` di atas `background: lightgray` (contrast fail)  
❌ Icon button tanpa label (accessibility fail)  
❌ Form tanpa label, hanya placeholder (UX fail)  
❌ Animasi width/height (performance fail)  
❌ Fixed pixel container width (responsive fail)  
❌ Raw hex di setiap komponen (maintainability fail)  
