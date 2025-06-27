# Panduan CSS Grid align-content

## Penjelasan align-content

**`align-content`** adalah properti CSS Grid yang mengatur **alignment vertikal** dari **seluruh grid** di dalam grid container. Properti ini adalah pasangan vertikal dari `justify-content`.

### Konsep Dasar:
- **Align** = Vertical alignment (sumbu Y)
- **Content** = Seluruh grid sebagai satu blok
- Bekerja ketika **total tinggi grid lebih kecil** dari container
- Mengatur distribusi ruang kosong vertikal di sekitar grid

### Kapan align-content Bekerja?
```css
.container {
    height: 500px; /* Container 500px tinggi */
    display: grid;
    grid-template-rows: 100px 100px 100px; /* Total grid: 300px */
    /* Sisa ruang: 500px - 300px = 200px */
    align-content: center; /* 200px dibagi rata atas-bawah */
}
```

**Penjelasan:** Container memiliki tinggi 500px, tapi grid hanya butuh 300px. Sisa 200px akan didistribusikan sesuai nilai `align-content`.

## Sintaks

```css
.grid-container {
    align-content: start | end | center | stretch | space-around | space-between | space-evenly;
}
```

## Nilai-nilai align-content

### 1. `start` (Default)
Grid disejajarkan ke **atas** (start) dari container.

```css
.container {
    display: grid;
    grid-template-columns: repeat(3, 150px);
    grid-template-rows: repeat(2, 100px);
    height: 400px; /* Lebih tinggi dari total grid */
    align-content: start;
    gap: 10px;
}
```

**Hasil:** Grid akan menempel di bagian atas container, menyisakan ruang kosong di bawah.

### 2. `end`
Grid disejajarkan ke **bawah** (end) dari container.

```css
.container {
    display: grid;
    grid-template-columns: repeat(3, 150px);
    grid-template-rows: repeat(2, 100px);
    height: 400px;
    align-content: end;
    gap: 10px;
}
```

**Hasil:** Grid akan menempel di bagian bawah container, menyisakan ruang kosong di atas.

### 3. `center`
Grid disejajarkan ke **tengah** vertikal dari container.

```css
.container {
    display: grid;
    grid-template-columns: repeat(3, 150px);
    grid-template-rows: repeat(2, 100px);
    height: 400px;
    align-content: center;
    gap: 10px;
}
```

**Hasil:** Grid akan berada di tengah container, dengan ruang kosong yang sama di atas dan bawah.

### 4. `stretch`
Grid rows akan **meregang** untuk mengisi seluruh tinggi container.

```css
.container {
    display: grid;
    grid-template-columns: repeat(3, 150px);
    grid-template-rows: repeat(2, 1fr); /* Gunakan fr untuk stretch */
    height: 400px;
    align-content: stretch;
    gap: 10px;
}
```

**Hasil:** Grid rows akan meregang mengisi seluruh tinggi container. Biasanya digunakan dengan unit `fr`.

### 5. `space-between`
Ruang kosong didistribusikan **di antara** grid rows.

```css
.container {
    display: grid;
    grid-template-columns: repeat(3, 150px);
    grid-template-rows: repeat(3, 80px);
    height: 400px;
    align-content: space-between;
    gap: 0; /* Hilangkan gap untuk melihat efek */
}
```

**Hasil:** Row pertama menempel atas, row terakhir menempel bawah, ruang kosong dibagi rata di antara rows.

### 6. `space-around`
Ruang kosong didistribusikan **di sekitar** setiap grid row.

```css
.container {
    display: grid;
    grid-template-columns: repeat(3, 150px);
    grid-template-rows: repeat(3, 80px);
    height: 400px;
    align-content: space-around;
    gap: 0;
}
```

**Hasil:** Setiap row mendapat ruang yang sama di atas dan bawahnya. Ruang di ujung container setengah dari ruang antar-row.

### 7. `space-evenly`
Ruang kosong didistribusikan **sama rata** di semua tempat.

```css
.container {
    display: grid;
    grid-template-columns: repeat(3, 150px);
    grid-template-rows: repeat(3, 80px);
    height: 400px;
    align-content: space-evenly;
    gap: 0;
}
```

**Hasil:** Ruang di ujung container sama dengan ruang antar-row. Distribusi paling merata.

## Perbedaan dengan align-items

```css
/* align-content: mengatur posisi SELURUH GRID */
.container-content {
    display: grid;
    grid-template-rows: repeat(2, 100px); /* Total: 200px */
    height: 400px; /* Container: 400px */
    align-content: center; /* Grid 200px di tengah container 400px */
}

/* align-items: mengatur posisi INDIVIDUAL ITEMS dalam area */
.container-items {
    display: grid;
    grid-template-rows: repeat(2, 150px);
    align-items: center; /* Item di tengah area masing-masing */
}

/* Kombinasi keduanya */
.container-both {
    display: grid;
    grid-template-rows: repeat(2, 100px);
    height: 400px;
    align-content: center; /* Grid di tengah container */
    align-items: center;   /* Item di tengah area masing-masing */
}
```

**Penjelasan:**
- `align-content`: Mengatur posisi keseluruhan grid dalam container
- `align-items`: Mengatur posisi individual items dalam grid area masing-masing

## Kombinasi dengan justify-content

```css
.perfect-center {
    display: grid;
    grid-template-columns: repeat(3, 120px);
    grid-template-rows: repeat(2, 100px);
    width: 500px;
    height: 350px;
    gap: 10px;
    
    /* Perfect centering */
    justify-content: center; /* Horizontal center */
    align-content: center;   /* Vertical center */
    
    background: #f8f9fa;
    border: 2px solid #dee2e6;
}
```

**Hasil:** Grid akan berada tepat di tengah-tengah container, baik horizontal maupun vertikal.

## Shorthand: place-content

```css
.container {
    display: grid;
    width: 500px;
    height: 400px;
    
    /* Cara panjang */
    align-content: center;
    justify-content: center;
    
    /* Cara singkat - hasil sama */
    place-content: center center;
    
    /* Jika nilai sama */
    place-content: center;
}
```

**Penjelasan:** `place-content` adalah shorthand untuk `align-content` dan `justify-content`. Format: `place-content: align-content justify-content`.

## Contoh Praktis: Layout Halaman

```css
.page-layout {
    display: grid;
    grid-template-columns: 1fr;
    grid-template-rows: auto 1fr auto;
    grid-template-areas:
        "header"
        "main"
        "footer";
    min-height: 100vh;
    
    /* Jika konten kurang dari 100vh */
    align-content: space-between;
}

.header {
    grid-area: header;
    background: #2c3e50;
    color: white;
    padding: 20px;
}

.main {
    grid-area: main;
    padding: 20px;
    background: #ecf0f1;
}

.footer {
    grid-area: footer;
    background: #34495e;
    color: white;
    padding: 15px;
}
```

**Penjelasan:** Layout akan menggunakan `space-between` untuk mendorong footer ke bawah ketika konten main sedikit.

## Contoh Card Layout dengan Responsive

```css
.card-container {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 20px;
    padding: 20px;
    min-height: 80vh;
}

/* Mobile: center cards */
@media (max-width: 768px) {
    .card-container {
        align-content: center;
    }
}

/* Desktop: start dari atas */
@media (min-width: 769px) {
    .card-container {
        align-content: start;
    }
}
```

## Tips dan Best Practices

### 1. Gunakan dengan Min-Height untuk Flexibility
```css
.flexible-layout {
    display: grid;
    grid-template-rows: auto 1fr auto;
    min-height: 100vh; /* Minimum full screen */
    align-content: stretch; /* Expand jika konten lebih banyak */
}
```

### 2. Kombinasi yang Efektif
```css
.center-everything {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    place-content: center; /* Shorthand untuk center-center */
    min-height: 100vh;
    gap: 20px;
}
```

### 3. Responsive Alignment
```css
.responsive-grid {
    display: grid;
    grid-template-rows: repeat(3, auto);
    min-height: 100vh;
}

/* Mobile: space around untuk breathing room */
@media (max-width: 768px) {
    .responsive-grid {
        align-content: space-around;
    }
}

/* Desktop: space between untuk full utilization */
@media (min-width: 769px) {
    .responsive-grid {
        align-content: space-between;
    }
}
```

## Kesalahan yang Harus Dihindari

### 1. Menggunakan align-content tanpa Ruang Kosong
```css
/* ❌ Salah: grid mengisi penuh tinggi, tidak ada ruang */
.no-space {
    display: grid;
    grid-template-rows: 1fr 1fr;
    height: 400px;
    align-content: center; /* Tidak ada efek */
}

/* ✅ Benar: ada ruang kosong */
.with-space {
    display: grid;
    grid-template-rows: 100px 100px;
    height: 400px;
    align-content: center; /* Ada efek */
}
```

### 2. Confusing dengan align-items
```css
/* ❌ Salah konsep */
.wrong {
    display: grid;
    align-content: center; /* Mengatur grid, bukan item */
    /* Tapi maksudnya ingin center item dalam area */
}

/* ✅ Benar: jika ingin center items */
.correct {
    display: grid;
    align-items: center; /* Mengatur item dalam area */
}
```

### 3. Tidak Mempertimbangkan Container Height
```css
/* ❌ Buruk: tidak ada tinggi container yang jelas */
.unclear-height {
    display: grid;
    align-content: center; /* Tidak jelas center dari mana */
}

/* ✅ Baik: tinggi container yang jelas */
.clear-height {
    display: grid;
    height: 100vh; /* atau min-height */
    align-content: center;
}
```

## Debugging align-content

### 1. Tambahkan Border untuk Visualisasi
```css
.debug-container {
    display: grid;
    align-content: center;
    border: 3px solid red; /* Lihat boundary container */
    background: rgba(255, 0, 0, 0.1);
}

.debug-grid {
    background: rgba(0, 255, 0, 0.2); /* Lihat area grid */
    border: 2px dashed blue;
}
```

### 2. Test dengan Nilai Berbeda
```css
.test-container {
    display: grid;
    grid-template-rows: repeat(2, 100px);
    height: 400px;
    
    /* Ganti untuk testing */
    align-content: start;    /* Test 1 */
    /* align-content: center; */  /* Test 2 */
    /* align-content: end; */     /* Test 3 */
    /* align-content: space-between; */ /* Test 4 */
}
```

## Kesimpulan

`align-content` adalah properti penting untuk mengontrol distribusi vertikal seluruh grid dalam container. Kunci penggunaannya:

- **Pastikan ada ruang kosong** vertikal di container
- **Berbeda dengan align-items** yang mengatur individual items
- **Sangat berguna** untuk layout full-height dan centering
- **Kombinasikan dengan justify-content** untuk kontrol lengkap
- **Gunakan shorthand place-content** untuk kode yang lebih bersih

Memahami `align-content` akan membantu Anda membuat layout vertikal yang profesional dan responsif.