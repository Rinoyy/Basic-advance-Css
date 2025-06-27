# Panduan CSS Grid justify-content

## Penjelasan justify-content

**`justify-content`** adalah properti CSS Grid yang mengatur **alignment horizontal** dari **seluruh grid** di dalam grid container. Berbeda dengan `justify-items` yang mengatur posisi individual items, `justify-content` mengatur posisi keseluruhan grid sebagai satu kesatuan.

### Konsep Dasar:
- **Justify** = Horizontal alignment (sumbu X)
- **Content** = Seluruh grid sebagai satu blok
- Bekerja ketika **total lebar grid lebih kecil** dari container
- Mengatur distribusi ruang kosong di sekitar grid

### Kapan justify-content Bekerja?
```css
.container {
    width: 800px; /* Container 800px */
    display: grid;
    grid-template-columns: 150px 150px 150px; /* Total grid: 450px */
    /* Sisa ruang: 800px - 450px = 350px */
    justify-content: center; /* 350px dibagi rata kiri-kanan */
}
```

## Sintaks

```css
.grid-container {
    justify-content: start | end | center | stretch | space-around | space-between | space-evenly;
}
```

## Nilai-nilai justify-content

### 1. `start` (Default)
Grid disejajarkan ke **kiri** (start) dari container.

```css
.container {
    display: grid;
    grid-template-columns: repeat(3, 120px);
    grid-template-rows: repeat(2, 100px);
    justify-content: start;
    gap: 10px;
    width: 500px; /* Lebih lebar dari total grid */
    background: #ecf0f1;
    border: 2px solid #34495e;
}

.item {
    background: #3498db;
    color: white;
    padding: 15px;
    text-align: center;
}
```

**Penjelasan:** Grid akan menempel di sisi kiri container, menyisakan ruang kosong di sebelah kanan.

### 2. `end`
Grid disejajarkan ke **kanan** (end) dari container.

```css
.container {
    display: grid;
    grid-template-columns: repeat(3, 120px);
    grid-template-rows: repeat(2, 100px);
    justify-content: end;
    gap: 10px;
    width: 500px;
    background: #ecf0f1;
    border: 2px solid #34495e;
}

.item {
    background: #e74c3c;
    color: white;
    padding: 15px;
    text-align: center;
}
```

**Penjelasan:** Grid akan menempel di sisi kanan container, menyisakan ruang kosong di sebelah kiri.

### 3. `center`
Grid disejajarkan ke **tengah** horizontal dari container.

```css
.container {
    display: grid;
    grid-template-columns: repeat(3, 120px);
    grid-template-rows: repeat(2, 100px);
    justify-content: center;
    gap: 10px;
    width: 500px;
    background: #ecf0f1;
    border: 2px solid #34495e;
}

.item {
    background: #2ecc71;
    color: white;
    padding: 15px;
    text-align: center;
}
```

**Penjelasan:** Grid akan berada di tengah container, dengan ruang kosong yang sama di kiri dan kanan.

### 4. `stretch`
Grid columns akan **meregang** untuk mengisi seluruh lebar container.

```css
.container {
    display: grid;
    grid-template-columns: repeat(3, 1fr); /* Gunakan fr untuk stretch */
    grid-template-rows: repeat(2, 100px);
    justify-content: stretch;
    gap: 10px;
    width: 500px;
    background: #ecf0f1;
    border: 2px solid #34495e;
}

.item {
    background: #9b59b6;
    color: white;
    padding: 15px;
    text-align: center;
}
```

**Penjelasan:** Grid columns akan meregang mengisi seluruh lebar container. Biasanya digunakan dengan unit `fr`.

### 5. `space-between`
Ruang kosong didistribusikan **di antara** grid columns.

```css
.container {
    display: grid;
    grid-template-columns: repeat(3, 100px);
    grid-template-rows: repeat(2, 100px);
    justify-content: space-between;
    gap: 0; /* Hilangkan gap untuk melihat efek space-between */
    width: 500px;
    background: #ecf0f1;
    border: 2px solid #34495e;
}

.item {
    background: #f39c12;
    color: white;
    padding: 15px;
    text-align: center;
}
```

**Penjelasan:** Column pertama menempel kiri, column terakhir menempel kanan, ruang kosong dibagi rata di antara columns.

### 6. `space-around`
Ruang kosong didistribusikan **di sekitar** setiap grid column.

```css
.container {
    display: grid;
    grid-template-columns: repeat(3, 100px);
    grid-template-rows: repeat(2, 100px);
    justify-content: space-around;
    gap: 0;
    width: 500px;
    background: #ecf0f1;
    border: 2px solid #34495e;
}

.item {
    background: #e67e22;
    color: white;
    padding: 15px;
    text-align: center;
}
```

**Penjelasan:** Setiap column mendapat ruang yang sama di kiri dan kanannya. Ruang di ujung container setengah dari ruang antar-column.

### 7. `space-evenly`
Ruang kosong didistribusikan **sama rata** di semua tempat.

```css
.container {
    display: grid;
    grid-template-columns: repeat(3, 100px);
    grid-template-rows: repeat(2, 100px);
    justify-content: space-evenly;
    gap: 0;
    width: 500px;
    background: #ecf0f1;
    border: 2px solid #34495e;
}

.item {
    background: #8e44ad;
    color: white;
    padding: 15px;
    text-align: center;
}
```

**Penjelasan:** Ruang di ujung container sama dengan ruang antar-column. Distribusi paling merata.

## Visualisasi Perbedaan Space Values

```css
/* Demo container untuk membandingkan space values */
.demo-wrapper {
    margin-bottom: 30px;
}

.demo-title {
    margin-bottom: 10px;
    font-weight: bold;
    color: #2c3e50;
}

.demo-container {
    display: grid;
    grid-template-columns: repeat(4, 80px);
    grid-template-rows: 60px;
    width: 400px;
    background: linear-gradient(90deg, #ff000020 1px, transparent 1px);
    background-size: 50px 100%;
    border: 2px solid #34495e;
    margin-bottom: 10px;
}

.demo-item {
    background: #3498db;
    color: white;
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: bold;
    font-size: 12px;
}

/* Different space distributions */
.space-between { justify-content: space-between; }
.space-around { justify-content: space-around; }
.space-evenly { justify-content: space-evenly; }
.center { justify-content: center; }
.start { justify-content: start; }
.end { justify-content: end; }
```

## Perbedaan dengan justify-items

```css
/* justify-content: mengatur posisi SELURUH GRID */
.container-content {
    display: grid;
    grid-template-columns: repeat(3, 100px); /* Total: 300px */
    width: 500px; /* Container: 500px */
    justify-content: center; /* Grid 300px di tengah container 500px */
}

/* justify-items: mengatur posisi INDIVIDUAL ITEMS dalam area */
.container-items {
    display: grid;
    grid-template-columns: repeat(3, 150px);
    justify-items: center; /* Item di tengah area masing-masing */
}

/* Kombinasi keduanya */
.container-both {
    display: grid;
    grid-template-columns: repeat(3, 100px);
    width: 500px;
    justify-content: center; /* Grid di tengah container */
    justify-items: center;   /* Item di tengah area masing-masing */
}
```

## Contoh Praktis: Responsive Navigation

```css
.nav-container {
    display: grid;
    grid-template-columns: repeat(5, auto);
    gap: 20px;
    padding: 15px 30px;
    background: #2c3e50;
    width: 100%;
}

.nav-item {
    background: #3498db;
    color: white;
    padding: 10px 20px;
    border-radius: 6px;
    text-decoration: none;
    transition: background 0.3s ease;
}

.nav-item:hover {
    background: #2980b9;
}

/* Mobile: center navigation */
@media (max-width: 768px) {
    .nav-container {
        justify-content: center;
        grid-template-columns: repeat(3, auto);
    }
    
    .nav-item:nth-child(4),
    .nav-item:nth-child(5) {
        display: none;
    }
}

/* Tablet: space around */
@media (min-width: 769px) and (max-width: 1024px) {
    .nav-container {
        justify-content: space-around;
    }
}

/* Desktop: space between */
@media (min-width: 1025px) {
    .nav-container {
        justify-content: space-between;
    }
}
```

**Penjelasan kode:**
- Mobile: items di-center, beberapa item disembunyikan
- Tablet: space-around untuk distribusi seimbang
- Desktop: space-between untuk mengisi penuh lebar

## Contoh Layout: Card Gallery

```css
.gallery-container {
    display: grid;
    grid-template-columns: repeat(auto-fit, 250px);
    gap: 25px;
    padding: 30px;
    background: #f8f9fa;
    min-height: 100vh;
}

.gallery-card {
    background: white;
    border-radius: 12px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    overflow: hidden;
    transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.gallery-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15);
}

.card-image {
    width: 100%;
    height: 200px;
    object-fit: cover;
}

.card-content {
    padding: 20px;
}

.card-title {
    color: #2c3e50;
    margin-bottom: 10px;
    font-size: 1.1em;
    font-weight: 600;
}

.card-description {
    color: #7f8c8d;
    line-height: 1.6;
    font-size: 0.9em;
}

/* Responsive justify-content */
@media (max-width: 600px) {
    .gallery-container {
        grid-template-columns: 1fr;
        justify-content: stretch;
    }
}

@media (min-width: 601px) and (max-width: 900px) {
    .gallery-container {
        justify-content: center;
    }
}

@media (min-width: 901px) and (max-width: 1200px) {
    .gallery-container {
        justify-content: space-around;
    }
}

@media (min-width: 1201px) {
    .gallery-container {
        justify-content: space-between;
    }
}
```

## Advanced: Dynamic justify-content

```css
:root {
    --grid-justify-content: center;
    --grid-columns: repeat(4, 150px);
}

.dynamic-grid {
    display: grid;
    grid-template-columns: var(--grid-columns);
    gap: 20px;
    padding: 20px;
    width: 100%;
    background: #ecf0f1;
    justify-content: var(--grid-justify-content);
    transition: all 0.3s ease;
}

.dynamic-item {
    background: linear-gradient(135deg, #667eea, #764ba2);
    color: white;
    padding: 20px;
    border-radius: 10px;
    text-align: center;
    font-weight: bold;
}

.controls {
    margin-bottom: 20px;
    text-align: center;
}

.control-btn {
    margin: 5px;
    padding: 10px 15px;
    border: none;
    border-radius: 6px;
    background: #3498db;
    color: white;
    cursor: pointer;
    font-size: 14px;
    transition: background 0.3s ease;
}

.control-btn:hover {
    background: #2980b9;
}

.control-btn.active {
    background: #e74c3c;
}
```

```javascript
// JavaScript untuk mengubah justify-content secara dinamis
function changeJustifyContent(value) {
    document.documentElement.style.setProperty('--grid-justify-content', value);
    
    // Update active button
    document.querySelectorAll('.control-btn').forEach(btn => {
        btn.classList.remove('active');
    });
    event.target.classList.add('active');
}

// HTML untuk controls:
/*
<div class="controls">
    <button class="control-btn" onclick="changeJustifyContent('start')">Start</button>
    <button class="control-btn" onclick="changeJustifyContent('center')">Center</button>
    <button class="control-btn" onclick="changeJustifyContent('end')">End</button>
    <button class="control-btn" onclick="changeJustifyContent('space-between')">Space Between</button>
    <button class="control-btn" onclick="changeJustifyContent('space-around')">Space Around</button>
    <button class="control-btn" onclick="changeJustifyContent('space-evenly')">Space Evenly</button>
</div>
*/
```

## Kombinasi dengan align-content

```css
.full-center-grid {
    display: grid;
    grid-template-columns: repeat(3, 120px);
    grid-template-rows: repeat(2, 80px);
    gap: 15px;
    
    /* Container lebih besar dari grid */
    width: 500px;
    height: 300px;
    
    /* Center horizontal dan vertical */
    justify-content: center; /* Horizontal center */
    align-content: center;   /* Vertical center */
    
    background: #f8f9fa;
    border: 2px solid #dee2e6;
}

/* Shorthand untuk justify-content dan align-content */
.place-content-center {
    display: grid;
    grid-template-columns: repeat(3, 120px);
    grid-template-rows: repeat(2, 80px);
    width: 500px;
    height: 300px;
    
    /* Shorthand: align-content justify-content */
    place-content: center center;
    /* atau jika nilai sama: */
    /* place-content: center; */
}
```

## Tips dan Best Practices

### 1. Gunakan dengan Auto-Fit untuk Responsive
```css
.responsive-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 20px;
    justify-content: center; /* Center ketika tidak ada cukup ruang */
}
```

### 2. Kombinasikan dengan CSS Custom Properties
```css
:root {
    --content-alignment: space-between;
    --grid-gap: 20px;
}

.flexible-grid {
    display: grid;
    grid-template-columns: repeat(4, 150px);
    gap: var(--grid-gap);
    justify-content: var(--content-alignment);
}

/* Ubah alignment untuk breakpoint berbeda */
@media (max-width: 768px) {
    :root {
        --content-alignment: center;
        --grid-gap: 15px;
    }
}
```

### 3. Perhatikan Total Width Grid
```css
/* ✅ Baik: ada ruang kosong untuk justify-content bekerja */
.good-example {
    display: grid;
    grid-template-columns: repeat(3, 200px); /* Total: 600px */
    width: 800px; /* Container: 800px */
    justify-content: center; /* 200px ruang kosong dibagi rata */
}

/* ❌ Tidak efektif: grid sama lebar dengan container */
.ineffective-example {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    justify-content: center; /* Tidak ada efek karena grid mengisi penuh */
}
```

## Kesalahan yang Harus Dihindari

### 1. Menggunakan justify-content tanpa Ruang Kosong
```css
/* ❌ Salah: grid mengisi penuh, tidak ada ruang untuk justify-content */
.container {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    justify-content: center; /* Tidak ada efek */
}

/* ✅ Benar: ada ruang kosong */
.container {
    display: grid;
    grid-template-columns: 150px 150px 150px;
    width: 600px;
    justify-content: center; /* Ada efek */
}
```

### 2. Confusing dengan justify-items
```css
/* ❌ Salah konsep: menggunakan justify-content untuk item alignment */
.wrong-approach {
    display: grid;
    grid-template-columns: repeat(3, 200px);
    justify-content: center; /* Ini mengatur posisi grid, bukan item */
}

/* ✅ Jika ingin center items dalam area masing-masing */
.correct-approach {
    display: grid;
    grid-template-columns: repeat(3, 200px);
    justify-items: center; /* Ini mengatur posisi item */
}
```

### 3. Tidak Mempertimbangkan Responsive
```css
/* ❌ Buruk: fixed width tidak responsive */
.fixed-grid {
    display: grid;
    grid-template-columns: repeat(4, 200px);
    justify-content: space-between;
    width: 800px; /* Tetap di semua screen size */
}

/* ✅ Baik: responsive dengan max-width */
.responsive-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    justify-content: center;
    max-width: 1200px;
    margin: 0 auto;
}
```

## Debugging justify-content

### 1. Visualisasi dengan Background
```css
.debug-container {
    display: grid;
    justify-content: center;
    
    /* Background untuk melihat container boundary */
    background: linear-gradient(90deg, #ff000020 1px, transparent 1px);
    background-size: 50px 100%;
    border: 3px solid red;
    
    /* Grid background */
    position: relative;
}

.debug-container::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(0, 255, 0, 0.1);
    pointer-events: none;
}
```

### 2. Console Log untuk Debugging
```javascript
// JavaScript untuk debug grid dimensions
function debugGrid(containerSelector) {
    const container = document.querySelector(containerSelector);
    const containerWidth = container.offsetWidth;
    const gridColumns = getComputedStyle(container).gridTemplateColumns;
    
    console.log('Container width:', containerWidth + 'px');
    console.log('Grid columns:', gridColumns);
    console.log('Justify content:', getComputedStyle(container).justifyContent);
}

// Usage: debugGrid('.my-grid-container');
```

`justify-content` adalah properti powerful untuk mengontrol distribusi dan alignment seluruh grid dalam container. Memahami kapan dan bagaimana menggunakannya akan membantu Anda membuat layout yang fleksibel dan responsif.