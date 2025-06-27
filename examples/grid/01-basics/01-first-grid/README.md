## 📁 01-first-grid

### 🎯 Tujuan Pembelajaran:
- Memahami perbedaan sebelum dan sesudah `display: grid`
- Mengerti apa yang terjadi ketika elemen menjadi grid container
- Memahami behavior default dari grid

### 🔑 Konsep Utama:

**Sebelum Grid:**
```css
/* Tanpa Grid - elemen mengikuti normal document flow */
.container {
  /* tidak ada grid properties */
}
```

**Setelah Grid:**
```css
/* Dengan Grid - elemen menjadi grid container */
.container {
  display: grid; /* ✨ Magic happens here! */
}
```

### 💡 Apa yang Terjadi Ketika `display: grid`?

1. **Container menjadi Grid Container** - Parent element sekarang punya grid context
2. **Direct children menjadi Grid Items** - Semua child langsung otomatis jadi grid items
3. **Default behavior** - Tanpa property tambahan, items akan tersusun dalam 1 kolom
4. **Grid lines terbentuk** - Invisible grid lines mulai ada (bisa dilihat di dev tools)

### 🔍 Yang Perlu Diperhatikan:
- Grid items akan stack vertikal secara default (seperti block elements)
- Ukuran column mengikuti content dan container width
- Tidak ada gap/spacing otomatis

### 💭 Mental Model:
Bayangkan Anda punya **kotak kosong** (container). Ketika Anda tulis `display: grid`, kotak ini tiba-tiba punya **invisible grid lines** yang siap untuk diatur.

---