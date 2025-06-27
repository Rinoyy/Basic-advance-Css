# 📁 02-columns-rows - Grid Template Columns & Rows

## 🎯 Tujuan Pembelajaran
- Memahami `grid-template-columns` dan `grid-template-rows` secara mendalam
- Menguasai berbagai unit yang bisa digunakan (px, %, em, fr, auto)
- Memahami perbedaan explicit vs implicit grid
- Mengerti bagaimana grid tracks terbentuk dan berinteraksi

## 🔑 Konsep Fundamental

### Grid Template Columns
Property ini menentukan **ukuran dan jumlah kolom** dalam grid container.

```css
.container {
  display: grid;
  grid-template-columns: [ukuran-kolom-1] [ukuran-kolom-2] [ukuran-kolom-3] ...;
}
```

### Grid Template Rows  
Property ini menentukan **ukuran dan jumlah baris** dalam grid container.

```css
.container {
  display: grid;
  grid-template-rows: [ukuran-baris-1] [ukuran-baris-2] [ukuran-baris-3] ...;
}
```

## 📏 Unit-unit yang Bisa Digunakan

### 1. **Pixel (px) - Fixed Units**
```css
/* 3 kolom dengan lebar tetap */
.grid-fixed {
  grid-template-columns: 200px 300px 150px;
}
```
- ✅ **Pros**: Predictable, exact sizing
- ❌ **Cons**: Tidak responsive, bisa overflow di layar kecil

### 2. **Percentage (%) - Relative to Container**
```css
/* 3 kolom dengan persentase */
.grid-percentage {
  grid-template-columns: 30% 50% 20%;
}
```
- ✅ **Pros**: Responsive terhadap container
- ❌ **Cons**: Susah maintain spacing yang konsisten

### 3. **Em/Rem - Relative to Font Size**
```css
/* Kolom berdasarkan font size */
.grid-em {
  grid-template-columns: 20em 15rem 10em;
}
```
- ✅ **Pros**: Scale dengan typography
- 🤔 **Use case**: Layout yang font-dependent

### 4. **Auto - Content-based Sizing**
```css
/* Kolom menyesuaikan konten */
.grid-auto {
  grid-template-columns: auto auto auto;
}
```
- ✅ **Pros**: Perfect fit untuk content
- ❌ **Cons**: Unpredictable sizing

### 5. **Fractional (fr) - Available Space**
```css
/* Kolom berbagi remaining space */
.grid-fr {
  grid-template-columns: 1fr 2fr 1fr;
}
```
- ✅ **Pros**: Sangat responsive, flexible
- ✅ **Best practice**: Kombinasi dengan fixed units

## 🔀 Mixing Units - Real World Examples

### Example 1: Sidebar Layout
```css
.sidebar-layout {
  grid-template-columns: 250px 1fr;
  /* Sidebar tetap 250px, content area fleksibel */
}
```

### Example 2: Three Column Layout
```css
.three-column {
  grid-template-columns: 200px 1fr 150px;
  /* Left sidebar - Main content - Right sidebar */
}
```

### Example 3: Complex Magazine Layout
```css
.magazine {
  grid-template-columns: 1fr 2fr 1fr 200px;
  /* Small col - Main content - Small col - Ads */
}
```

### Example 4: Mixed Units Extreme
```css
.complex-grid {
  grid-template-columns: 100px 20% 1fr auto 2em;
  /* Fixed - Percentage - Flexible - Content - Font-based */
}
```

## 🆚 Explicit vs Implicit Grid

### Explicit Grid (Yang Anda Definisikan)
```css
.explicit {
  grid-template-columns: 1fr 1fr 1fr;  /* 3 kolom didefinisikan */
  grid-template-rows: 200px 100px;     /* 2 baris didefinisikan */
}
```

### Implicit Grid (Browser Generate Otomatis)
```html
<!-- HTML: 10 items, tapi grid cuma define 3 kolom × 2 baris = 6 cells -->
<div class="explicit">
  <div>Item 1</div>  <div>Item 2</div>  <div>Item 3</div>
  <div>Item 4</div>  <div>Item 5</div>  <div>Item 6</div>
  <div>Item 7</div>  <div>Item 8</div>  <div>Item 9</div>  <!-- Extra rows! -->
  <div>Item 10</div>
</div>
```

**Yang Terjadi:**
- Item 1-6: Masuk ke explicit grid (3×2)
- Item 7-10: Browser buat **implicit rows** otomatis
- Implicit rows punya tinggi `auto` (sesuai konten)

## 🎨 Perbedaan Behavior Columns vs Rows

### Columns Behavior
```css
.container {
  grid-template-columns: 200px 1fr 150px;
  /* Kalau ada item lebih → turun ke baris baru */
}
```

### Rows Behavior  
```css
.container {
  grid-template-columns: 1fr 1fr 1fr;
  grid-template-rows: 100px 200px;
  /* Kalau ada item lebih → buat implicit rows dengan tinggi auto */
}
```

## 🔄 Order Matters vs Position

### Normal Flow (Order Matters)
```css
.normal-flow {
  grid-template-columns: 1fr 1fr 1fr;
  /* Items mengisi grid dari kiri ke kanan, atas ke bawah */
}
```

### Explicit Positioning (Order Doesn't Matter)
```css
.positioned {
  grid-template-columns: 1fr 1fr 1fr;
}

.item-1 { grid-column: 3; }  /* Item 1 ke kolom 3 */
.item-2 { grid-column: 1; }  /* Item 2 ke kolom 1 */
.item-3 { grid-column: 2; }  /* Item 3 ke kolom 2 */
```

## 🔍 Deep Dive: Auto vs Fr vs Fixed

### Scenario: 3 Kolom dalam Container 900px

#### 1. Auto Sizing
```css
grid-template-columns: auto auto auto;
```
**Result**: Kolom size = content size
- Kolom 1: 150px (content width)
- Kolom 2: 200px (content width)  
- Kolom 3: 100px (content width)
- **Unused space**: 450px (tidak terpakai)

#### 2. Fr Sizing
```css
grid-template-columns: 1fr 1fr 1fr;
```
**Result**: Membagi available space equally
- Kolom 1: 300px (900px ÷ 3)
- Kolom 2: 300px (900px ÷ 3)
- Kolom 3: 300px (900px ÷ 3)
- **Unused space**: 0px

#### 3. Mixed Sizing
```css
grid-template-columns: 200px 1fr auto;
```
**Calculation Process**:
1. Fixed: 200px (kolom 1)
2. Auto: 150px (kolom 3 content)
3. Available: 900px - 200px - 150px = 550px
4. Fr gets: 550px (kolom 2)

**Result**:
- Kolom 1: 200px (fixed)
- Kolom 2: 550px (1fr = available space)
- Kolom 3: 150px (auto = content)

## ⚠️ Common Gotchas & Pitfalls

### 1. **Percentage Trap**
```css
/* ❌ Problematic */
.bad-percentage {
  grid-template-columns: 33% 33% 33%;
  gap: 20px;  /* Total > 100%! Overflow! */
}

/* ✅ Better */
.good-fr {
  grid-template-columns: 1fr 1fr 1fr;
  gap: 20px;  /* Fr units account for gap automatically */
}
```

### 2. **Auto Content Surprise**
```css
.auto-surprise {
  grid-template-columns: auto 1fr auto;
}
```
**Problem**: Jika content di kolom `auto` sangat panjang, bisa mengambil space yang tidak terduga.

### 3. **Fixed Unit Overflow**
```css
/* ❌ Dangerous di mobile */
.overflow-risk {
  grid-template-columns: 300px 400px 250px;  /* Total: 950px */
}

/* ✅ Responsive */
.responsive {
  grid-template-columns: 1fr 2fr 1fr;
}
```

## 🎯 Best Practices

### 1. **Start with Fr Units**
```css
/* Mulai dengan ini */
.container {
  grid-template-columns: 1fr 1fr 1fr;
}
```

### 2. **Add Fixed Sizes When Needed**
```css
/* Kemudian refine */
.container {
  grid-template-columns: 250px 1fr 200px;
}
```

### 3. **Use Auto Sparingly**
```css
/* Hati-hati dengan auto */
.container {
  grid-template-columns: auto 1fr;  /* OK untuk simple cases */
}
```

### 4. **Consider Mobile First**
```css
.responsive-grid {
  /* Mobile: 1 column */
  grid-template-columns: 1fr;
}

@media (min-width: 768px) {
  .responsive-grid {
    /* Desktop: 3 columns */
    grid-template-columns: 1fr 2fr 1fr;
  }
}
```

## 🧪 Experimental Playground Ideas

### 1. **Unit Comparison Test**
Buat 4 container dengan setup berbeda dan compare hasilnya:
```css
.test-1 { grid-template-columns: 300px 300px 300px; }
.test-2 { grid-template-columns: 33.33% 33.33% 33.33%; }
.test-3 { grid-template-columns: 1fr 1fr 1fr; }
.test-4 { grid-template-columns: auto auto auto; }
```

### 2. **Mixed Unit Exploration**
```css
.experiment {
  grid-template-columns: 100px 20% 1fr auto 2fr;
}
```

### 3. **Dynamic Content Test**
Buat grid dengan kolom `auto` dan test dengan content pendek vs panjang.

## 🔗 Connections

### 📖 **Previous**: [01-first-grid](../01-first-grid/README.md)
- Build upon basic `display: grid` understanding

### 📖 **Next**: [03-fr-units](../03-fr-units/README.md)  
- Deep dive into fractional units

### 📚 **Reference**: [../../docs/grid-properties.md](../../docs/grid-properties.md)
- Complete property reference

## 💡 Key Takeaways

1. **Columns define structure** - Jumlah nilai = jumlah kolom
2. **Units have trade-offs** - Pilih sesuai use case
3. **Fr units are magic** - Paling flexible dan responsive
4. **Mix units wisely** - Combine fixed + flexible
5. **Implicit grid happens** - Browser handle overflow otomatis
6. **Order matters by default** - Kecuali pakai explicit positioning

## 🎯 Ready untuk Next Step?

Setelah comfortable dengan concepts ini, Anda siap untuk:
- **03-fr-units**: Master fractional units
- **04-gap-spacing**: Perfect spacing
- **05-repeat-function**: Clean, efficient code

Happy gridding! 🚀