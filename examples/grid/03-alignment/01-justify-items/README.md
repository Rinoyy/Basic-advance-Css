# Panduan CSS Grid justify-items

## Penjelasan justify-items

**`justify-items`** adalah properti CSS Grid yang mengatur **alignment horizontal** (kiri-kanan) dari **semua item grid** di dalam grid container. Properti ini diterapkan pada **grid container** dan mempengaruhi semua grid items sekaligus.

### Konsep Dasar:
- **Justify** = Horizontal alignment (sumbu X)
- **Items** = Semua grid items dalam container
- Mengatur posisi item di dalam **grid area** masing-masing
- Berbeda dengan `justify-content` yang mengatur posisi seluruh grid

## Sintaks

```css
.grid-container {
    justify-items: start | end | center | stretch;
}
```

## Nilai-nilai justify-items

### 1. `start` (Default)
Item disejajarkan ke **kiri** (start) dari grid area.

```css
.container {
    display: grid;
    grid-template-columns: repeat(3, 150px);
    grid-template-rows: repeat(2, 100px);
    justify-items: start;
    gap: 10px;
    border: 2px solid #333;
}

.item {
    background: #3498db;
    color: white;
    padding: 10px;
    width: 80px; /* Lebih kecil dari grid area */
}
```

**Hasil:** Semua item akan menempel di sisi kiri grid area masing-masing.

### 2. `end`
Item disejajarkan ke **kanan** (end) dari grid area.

```css
.container {
    display: grid;
    grid-template-columns: repeat(3, 150px);
    grid-template-rows: repeat(2, 100px);
    justify-items: end;
    gap: 10px;
}

.item {
    background: #e74c3c;
    color: white;
    padding: 10px;
    width: 80px;
}
```

**Hasil:** Semua item akan menempel di sisi kanan grid area masing-masing.

### 3. `center`
Item disejajarkan ke **tengah** horizontal dari grid area.

```css
.container {
    display: grid;
    grid-template-columns: repeat(3, 150px);
    grid-template-rows: repeat(2, 100px);
    justify-items: center;
    gap: 10px;
}

.item {
    background: #2ecc71;
    color: white;
    padding: 10px;
    width: 80px;
}
```

**Hasil:** Semua item akan berada di tengah horizontal grid area masing-masing.

### 4. `stretch` 
Item akan **meregang** untuk mengisi seluruh lebar grid area.

```css
.container {
    display: grid;
    grid-template-columns: repeat(3, 150px);
    grid-template-rows: repeat(2, 100px);
    justify-items: stretch;
    gap: 10px;
}

.item {
    background: #9b59b6;
    color: white;
    padding: 10px;
    /* Tidak perlu width, akan otomatis stretch */
}
```

**Hasil:** Semua item akan mengisi penuh lebar grid area masing-masing.

## Contoh Praktis dengan Visualisasi

```css
/* Container dengan border untuk melihat grid area */
.demo-container {
    display: grid;
    grid-template-columns: repeat(3, 200px);
    grid-template-rows: repeat(2, 120px);
    gap: 15px;
    padding: 20px;
    background: #ecf0f1;
    border: 3px solid #34495e;
}

/* Item dengan ukuran lebih kecil untuk melihat efek alignment */
.demo-item {
    background: linear-gradient(45deg, #ff6b6b, #4ecdc4);
    color: white;
    padding: 15px;
    border-radius: 8px;
    width: 120px; /* Lebih kecil dari grid area (200px) */
    height: 80px;  /* Lebih kecil dari grid area (120px) */
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: bold;
}

/* Berbagai pilihan justify-items */
.justify-start { justify-items: start; }
.justify-end { justify-items: end; }
.justify-center { justify-items: center; }
.justify-stretch { justify-items: stretch; }

/* Untuk stretch, hilangkan width agar bisa meregang */
.justify-stretch .demo-item {
    width: auto;
}
```

## Perbedaan dengan Properti Lain

### justify-items vs justify-content

```css
/* justify-items: mengatur posisi ITEM di dalam grid area */
.container-items {
    display: grid;
    grid-template-columns: repeat(3, 150px);
    justify-items: center; /* Item di tengah area masing-masing */
}

/* justify-content: mengatur posisi SELURUH GRID di dalam container */
.container-content {
    display: grid;
    grid-template-columns: repeat(3, 150px);
    justify-content: center; /* Seluruh grid di tengah container */
    width: 100%;
}
```

### justify-items vs justify-self

```css
/* justify-items: diterapkan pada CONTAINER, mempengaruhi SEMUA item */
.container {
    display: grid;
    grid-template-columns: repeat(3, 150px);
    justify-items: center; /* Semua item ke tengah */
}

/* justify-self: diterapkan pada ITEM INDIVIDUAL, override justify-items */
.item-special {
    justify-self: end; /* Hanya item ini ke kanan, yang lain tetap center */
}
```

## Kombinasi dengan align-items

```css
.container {
    display: grid;
    grid-template-columns: repeat(3, 150px);
    grid-template-rows: repeat(2, 120px);
    
    /* Kombinasi alignment */
    justify-items: center;  /* Horizontal: tengah */
    align-items: center;    /* Vertical: tengah */
    
    /* Atau gunakan shorthand */
    /* place-items: center center; */
    
    gap: 10px;
}

.item {
    background: #f39c12;
    color: white;
    padding: 10px;
    width: 80px;
    height: 60px;
}
```

**Hasil:** Item akan berada di tengah-tengah (horizontal dan vertikal) dari grid area masing-masing.

## Contoh Real-World: Card Layout

```css
.card-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 20px;
    padding: 20px;
    justify-items: center; /* Card di tengah area masing-masing */
}

.card {
    background: white;
    border-radius: 12px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    padding: 20px;
    width: 220px; /* Lebih kecil dari minmax minimum */
    text-align: center;
    transition: transform 0.3s ease;
}

.card:hover {
    transform: translateY(-5px);
}

.card img {
    width: 100%;
    height: 150px;
    object-fit: cover;
    border-radius: 8px;
    margin-bottom: 15px;
}

.card h3 {
    color: #2c3e50;
    margin-bottom: 10px;
}

.card p {
    color: #7f8c8d;
    line-height: 1.6;
}
```

## Responsive dengan justify-items

```css
.responsive-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 15px;
    padding: 15px;
}

/* Mobile: item stretch untuk mengisi ruang */
.responsive-grid {
    justify-items: stretch;
}

/* Tablet: item di tengah */
@media (min-width: 768px) {
    .responsive-grid {
        justify-items: center;
    }
}

/* Desktop: item start untuk alignment konsisten */
@media (min-width: 1024px) {
    .responsive-grid {
        justify-items: start;
        grid-template-columns: repeat(4, 1fr);
    }
}
```

## Tips dan Best Practices

### 1. Gunakan justify-items untuk Konsistensi
```css
/* ✅ Baik: semua item aligned konsisten */
.gallery {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    justify-items: center;
    gap: 20px;
}
```

### 2. Kombinasikan dengan CSS Custom Properties
```css
:root {
    --grid-justify: center;
}

.container {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    justify-items: var(--grid-justify);
}

/* Ubah alignment dengan JavaScript */
/* document.documentElement.style.setProperty('--grid-justify', 'end'); */
```

### 3. Override Individual dengan justify-self
```css
.container {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    justify-items: center; /* Default untuk semua */
}

.featured-item {
    justify-self: stretch; /* Override untuk item khusus */
}
```

## Kesalahan yang Harus Dihindari

### 1. Menggunakan justify-items pada Non-Grid Container
```css
/* ❌ Salah: tidak ada display: grid */
.container {
    justify-items: center; /* Tidak akan bekerja */
}

/* ✅ Benar */
.container {
    display: grid;
    justify-items: center;
}
```

### 2. Confusing dengan Flexbox Properties
```css
/* ❌ Salah: ini property flexbox */
.grid-container {
    display: grid;
    justify-content: center; /* Ini mengatur seluruh grid */
    align-items: center;     /* Ini mengatur seluruh grid */
}

/* ✅ Benar: untuk mengatur individual items */
.grid-container {
    display: grid;
    justify-items: center;   /* Mengatur posisi items */
    align-items: center;     /* Mengatur posisi items */
}
```

### 3. Tidak Mempertimbangkan Ukuran Item
```css
/* ❌ Tidak efektif jika item sudah mengisi penuh */
.container {
    display: grid;
    grid-template-columns: repeat(3, 200px);
    justify-items: center;
}

.item {
    width: 200px; /* Sama dengan grid area, center tidak terlihat */
}

/* ✅ Lebih baik */
.item {
    width: 150px; /* Lebih kecil, sehingga center terlihat */
}
```

## Shorthand: place-items

```css
/* Shorthand untuk justify-items dan align-items */
.container {
    display: grid;
    
    /* Cara panjang */
    justify-items: center;
    align-items: center;
    
    /* Cara singkat - sama hasilnya */
    place-items: center center;
    
    /* Atau jika nilai sama */
    place-items: center;
}
```

## Debugging justify-items

### 1. Tambahkan Border untuk Visualisasi
```css
.container {
    display: grid;
    justify-items: center;
}

/* Tambahkan border untuk melihat grid area */
.container > * {
    border: 2px dashed red;
    background: rgba(255, 0, 0, 0.1);
}
```

### 2. Gunakan Developer Tools
- Buka DevTools browser
- Aktifkan Grid overlay
- Lihat posisi item dalam grid area

### 3. Test dengan Nilai Berbeda
```css
.test-container {
    display: grid;
    grid-template-columns: repeat(3, 150px);
    gap: 10px;
    
    /* Test dengan nilai berbeda */
    justify-items: start;    /* Test 1 */
    /* justify-items: center; */ /* Test 2 */
    /* justify-items: end; */    /* Test 3 */
    /* justify-items: stretch; */ /* Test 4 */
}
```

`justify-items` adalah properti fundamental dalam CSS Grid yang memberikan kontrol mudah atas alignment horizontal semua grid items. Memahami properti ini dengan baik akan membantu Anda membuat layout yang rapi dan konsisten.