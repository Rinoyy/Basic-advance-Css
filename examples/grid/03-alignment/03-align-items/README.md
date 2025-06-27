# Panduan CSS Grid align-items

## Penjelasan align-items

**`align-items`** adalah properti CSS Grid yang mengatur **alignment vertikal** (atas-bawah) dari **semua item grid** di dalam grid container. Properti ini diterapkan pada **grid container** dan mempengaruhi semua grid items sekaligus.

### Konsep Dasar:
- **Align** = Vertical alignment (sumbu Y)
- **Items** = Semua grid items dalam container
- Mengatur posisi item di dalam **grid area** masing-masing secara vertikal
- Pasangan dari `justify-items` (yang mengatur horizontal)

## Sintaks

```css
.grid-container {
    align-items: start | end | center | stretch;
}
```

## Nilai-nilai align-items

### 1. `stretch` (Default)
Item akan **meregang** untuk mengisi seluruh tinggi grid area.

```css
.container {
    display: grid;
    grid-template-columns: repeat(3, 150px);
    grid-template-rows: repeat(2, 120px);
    align-items: stretch;
    gap: 10px;
    border: 2px solid #333;
}

.item {
    background: #3498db;
    color: white;
    padding: 10px;
    /* Tidak perlu height, akan otomatis stretch */
}
```

**Penjelasan:** Setiap item akan mengisi penuh tinggi grid area (120px). Ini adalah nilai default, jadi tanpa `align-items` pun item akan stretch.

### 2. `start`
Item disejajarkan ke **atas** (start) dari grid area.

```css
.container {
    display: grid;
    grid-template-columns: repeat(3, 150px);
    grid-template-rows: repeat(2, 120px);
    align-items: start;
    gap: 10px;
}

.item {
    background: #e74c3c;
    color: white;
    padding: 10px;
    height: 60px; /* Lebih kecil dari grid area */
}
```

**Penjelasan:** Semua item akan menempel di bagian atas grid area masing-masing. Item hanya setinggi 60px dari 120px yang tersedia.

### 3. `end`
Item disejajarkan ke **bawah** (end) dari grid area.

```css
.container {
    display: grid;
    grid-template-columns: repeat(3, 150px);
    grid-template-rows: repeat(2, 120px);
    align-items: end;
    gap: 10px;
}

.item {
    background: #2ecc71;
    color: white;
    padding: 10px;
    height: 60px;
}
```

**Penjelasan:** Semua item akan menempel di bagian bawah grid area masing-masing, menyisakan ruang kosong di bagian atas.

### 4. `center`
Item disejajarkan ke **tengah** vertikal dari grid area.

```css
.container {
    display: grid;
    grid-template-columns: repeat(3, 150px);
    grid-template-rows: repeat(2, 120px);
    align-items: center;
    gap: 10px;
}

.item {
    background: #9b59b6;
    color: white;
    padding: 10px;
    height: 60px;
}
```

**Penjelasan:** Semua item akan berada di tengah vertikal grid area masing-masing, dengan ruang kosong yang sama di atas dan bawah.

## Contoh Praktis dengan Visualisasi

```css
/* Container demo untuk melihat efek align-items */
.demo-container {
    display: grid;
    grid-template-columns: repeat(2, 200px);
    grid-template-rows: repeat(2, 150px);
    gap: 20px;
    padding: 20px;
    background: #ecf0f1;
    border: 3px solid #34495e;
}

/* Item dengan tinggi lebih kecil untuk melihat efek alignment */
.demo-item {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
    padding: 15px;
    border-radius: 8px;
    height: 80px; /* Lebih kecil dari grid area (150px) */
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: bold;
    text-align: center;
}

/* Berbagai pilihan align-items */
.align-start { align-items: start; }
.align-end { align-items: end; }
.align-center { align-items: center; }
.align-stretch { align-items: stretch; }

/* Untuk stretch, hilangkan height agar bisa meregang */
.align-stretch .demo-item {
    height: auto;
}
```

**Penjelasan kode:**
- Grid area berukuran 150px tinggi
- Item hanya 80px tinggi
- Setiap class menghasilkan alignment berbeda
- Untuk `stretch`, height dihilangkan agar item bisa meregang penuh

## Kombinasi justify-items dan align-items

```css
.perfect-center {
    display: grid;
    grid-template-columns: repeat(3, 200px);
    grid-template-rows: repeat(2, 150px);
    gap: 15px;
    
    /* Kombinasi untuk center sempurna */
    justify-items: center; /* Horizontal center */
    align-items: center;   /* Vertical center */
}

.centered-item {
    background: #ff6b6b;
    color: white;
    padding: 20px;
    border-radius: 12px;
    width: 120px;  /* Lebih kecil dari 200px */
    height: 80px;  /* Lebih kecil dari 150px */
    display: flex;
    align-items: center;
    justify-content: center;
}
```

**Penjelasan:** Item akan berada tepat di tengah-tengah (horizontal dan vertikal) dari setiap grid area.

## Shorthand dengan place-items

```css
.container {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-template-rows: repeat(2, 120px);
    
    /* Cara panjang */
    align-items: center;
    justify-items: center;
    
    /* Cara singkat - hasil sama */
    place-items: center center;
    
    /* Jika nilai align dan justify sama */
    place-items: center;
}
```

**Penjelasan:** `place-items` adalah shorthand untuk `align-items` dan `justify-items`. Format: `place-items: align-items justify-items`.

## Perbedaan dengan Properti Lain

### align-items vs align-content

```css
/* align-items: mengatur posisi ITEM di dalam grid area */
.container-items {
    display: grid;
    grid-template-rows: repeat(3, 100px);
    align-items: center; /* Item di tengah area masing-masing */
}

/* align-content: mengatur posisi SELURUH GRID di dalam container */
.container-content {
    display: grid;
    grid-template-rows: repeat(3, 100px);
    align-content: center; /* Seluruh grid di tengah container */
    height: 500px; /* Container lebih tinggi dari grid */
}
```

### align-items vs align-self

```css
/* align-items: diterapkan pada CONTAINER, mempengaruhi SEMUA item */
.container {
    display: grid;
    grid-template-rows: repeat(3, 100px);
    align-items: center; /* Semua item ke tengah */
}

/* align-self: diterapkan pada ITEM INDIVIDUAL, override align-items */
.special-item {
    align-self: end; /* Hanya item ini ke bawah, yang lain tetap center */
}
```

## Contoh Real-World: Card Grid

```css
.card-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    grid-auto-rows: 300px; /* Tinggi tetap untuk semua card */
    gap: 25px;
    padding: 25px;
    align-items: start; /* Card mulai dari atas area */
}

.card {
    background: white;
    border-radius: 15px;
    box-shadow: 0 8px 25px rgba(0, 0, 0, 0.1);
    padding: 0;
    overflow: hidden;
    transition: transform 0.3s ease, box-shadow 0.3s ease;
    height: auto; /* Tinggi sesuai konten */
}

.card:hover {
    transform: translateY(-8px);
    box-shadow: 0 15px 35px rgba(0, 0, 0, 0.15);
}

.card-image {
    width: 100%;
    height: 180px;
    object-fit: cover;
}

.card-content {
    padding: 20px;
}

.card-title {
    color: #2c3e50;
    margin-bottom: 12px;
    font-size: 1.2em;
    font-weight: 600;
}

.card-text {
    color: #7f8c8d;
    line-height: 1.6;
    margin-bottom: 15px;
}

.card-button {
    background: #3498db;
    color: white;
    border: none;
    padding: 10px 20px;
    border-radius: 6px;
    cursor: pointer;
    transition: background 0.3s ease;
}

.card-button:hover {
    background: #2980b9;
}
```

**Penjelasan kode:**
- `grid-auto-rows: 300px` memberikan tinggi maksimal
- `align-items: start` membuat card mulai dari atas
- Card dengan `height: auto` akan menyesuaikan konten
- Jika konten card pendek, akan ada ruang kosong di bawah

## Responsive Design dengan align-items

```css
.responsive-grid {
    display: grid;
    grid-template-columns: 1fr;
    gap: 20px;
    padding: 20px;
}

/* Mobile: stretch untuk mengisi ruang */
.responsive-grid {
    align-items: stretch;
    grid-auto-rows: minmax(200px, auto);
}

/* Tablet: center untuk tampilan seimbang */
@media (min-width: 768px) {
    .responsive-grid {
        grid-template-columns: repeat(2, 1fr);
        align-items: center;
        grid-auto-rows: 250px;
    }
}

/* Desktop: start untuk alignment konsisten */
@media (min-width: 1024px) {
    .responsive-grid {
        grid-template-columns: repeat(3, 1fr);
        align-items: start;
        grid-auto-rows: 280px;
    }
}
```

## Contoh Interaktif dengan CSS Variables

```css
:root {
    --grid-align: center;
    --grid-justify: center;
}

.interactive-grid {
    display: grid;
    grid-template-columns: repeat(3, 150px);
    grid-template-rows: repeat(2, 120px);
    gap: 15px;
    padding: 20px;
    background: #f8f9fa;
    
    align-items: var(--grid-align);
    justify-items: var(--grid-justify);
}

.grid-item {
    background: #6c5ce7;
    color: white;
    padding: 15px;
    border-radius: 8px;
    width: 100px;
    height: 70px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: bold;
}

/* Kontrol dengan JavaScript */
.controls {
    margin-bottom: 20px;
}

.control-button {
    margin: 5px;
    padding: 8px 15px;
    border: none;
    border-radius: 5px;
    background: #74b9ff;
    color: white;
    cursor: pointer;
}

.control-button:hover {
    background: #0984e3;
}
```

```javascript
// JavaScript untuk mengubah align-items secara dinamis
function changeAlignment(value) {
    document.documentElement.style.setProperty('--grid-align', value);
}

// Contoh penggunaan:
// changeAlignment('start');
// changeAlignment('center');
// changeAlignment('end');
// changeAlignment('stretch');
```

## Tips dan Best Practices

### 1. Gunakan align-items untuk Konsistensi Vertikal
```css
/* ✅ Baik: semua item aligned vertikal konsisten */
.product-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    align-items: start; /* Produk mulai dari atas */
    gap: 20px;
}
```

### 2. Kombinasikan dengan Min-Height untuk Fleksibilitas
```css
.flexible-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    grid-auto-rows: minmax(150px, auto);
    align-items: stretch; /* Item mengisi tinggi minimum */
    gap: 15px;
}
```

### 3. Override Individual dengan align-self
```css
.container {
    display: grid;
    align-items: center; /* Default untuk semua */
}

.header-item {
    align-self: start; /* Header tetap di atas */
}

.footer-item {
    align-self: end; /* Footer tetap di bawah */
}
```

## Kesalahan yang Harus Dihindari

### 1. Menggunakan align-items tanpa Display Grid
```css
/* ❌ Salah: tidak ada display: grid */
.container {
    align-items: center; /* Tidak akan bekerja */
}

/* ✅ Benar */
.container {
    display: grid;
    align-items: center;
}
```

### 2. Konflik dengan Height yang Sama dengan Grid Area
```css
/* ❌ Tidak efektif jika item tingginya sama dengan area */
.container {
    display: grid;
    grid-template-rows: 100px;
    align-items: center;
}

.item {
    height: 100px; /* Sama dengan grid area, center tidak terlihat */
}

/* ✅ Lebih baik */
.item {
    height: 60px; /* Lebih kecil, sehingga center terlihat */
}
```

### 3. Salah Memahami Stretch Behavior
```css
/* ❌ Salah: menggunakan height dengan stretch */
.container {
    display: grid;
    align-items: stretch;
}

.item {
    height: 100px; /* Mengoverride stretch behavior */
}

/* ✅ Benar: biarkan stretch bekerja */
.item {
    /* Tidak perlu height, biarkan stretch mengatur */
    min-height: 50px; /* Gunakan min-height jika perlu */
}
```

## Debugging align-items

### 1. Visualisasi dengan Border
```css
.debug-container {
    display: grid;
    align-items: center;
    
    /* Border untuk melihat grid area */
    background: 
        linear-gradient(to right, #ff000020 1px, transparent 1px),
        linear-gradient(to bottom, #ff000020 1px, transparent 1px);
    background-size: 50px 50px;
}

.debug-item {
    border: 2px solid blue;
    background: rgba(0, 0, 255, 0.1);
}
```

### 2. Test dengan Nilai Berbeda
```css
.test-grid {
    display: grid;
    grid-template-columns: repeat(3, 150px);
    grid-template-rows: 120px;
    gap: 10px;
    
    /* Ganti nilai untuk testing */
    align-items: start;    /* Test 1 */
    /* align-items: center; */  /* Test 2 */
    /* align-items: end; */     /* Test 3 */
    /* align-items: stretch; */ /* Test 4 */
}
```

`align-items` adalah properti penting untuk mengontrol alignment vertikal dalam CSS Grid. Memahaminya dengan baik akan membantu Anda membuat layout yang rapi dan profesional dengan kontrol penuh atas posisi vertikal elemen.