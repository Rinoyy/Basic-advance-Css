# Panduan CSS Grid place-shortcuts

## Penjelasan place-shortcuts

**Place-shortcuts** adalah kumpulan properti CSS Grid yang menyederhanakan penulisan alignment dan positioning. Ada tiga properti shorthand utama:

- **`place-items`** - shorthand untuk `align-items` + `justify-items`
- **`place-content`** - shorthand untuk `align-content` + `justify-content`
- **`place-self`** - shorthand untuk `align-self` + `justify-self`

### Keuntungan Menggunakan place-shortcuts:
- **Kode lebih ringkas** - satu properti menggantikan dua
- **Mudah dibaca** - intention lebih jelas
- **Konsisten** - format penulisan yang sama

## 1. place-items

### Sintaks
```css
.container {
    place-items: align-items justify-items;
    /* atau jika nilai sama */
    place-items: align-items;
}
```

### Contoh Penggunaan
```css
/* Cara panjang */
.container-long {
    display: grid;
    align-items: center;
    justify-items: center;
}

/* Cara singkat - hasil sama */
.container-short {
    display: grid;
    place-items: center center;
}

/* Jika nilai sama */
.container-simple {
    display: grid;
    place-items: center;
}
```

**Penjelasan:** `place-items: center` akan membuat semua grid items berada di tengah-tengah area masing-masing, baik horizontal maupun vertikal.

### Nilai Berbeda untuk Align dan Justify
```css
.mixed-alignment {
    display: grid;
    grid-template-columns: repeat(3, 150px);
    grid-template-rows: repeat(2, 120px);
    gap: 10px;
    
    /* align-items: start, justify-items: center */
    place-items: start center;
}
```

**Hasil:** Items akan menempel di bagian atas area (start) tapi di tengah horizontal (center).

## 2. place-content

### Sintaks
```css
.container {
    place-content: align-content justify-content;
    /* atau jika nilai sama */
    place-content: align-content;
}
```

### Contoh Penggunaan
```css
/* Cara panjang */
.container-long {
    display: grid;
    width: 500px;
    height: 400px;
    align-content: center;
    justify-content: center;
}

/* Cara singkat - hasil sama */
.container-short {
    display: grid;
    width: 500px;
    height: 400px;
    place-content: center center;
}

/* Jika nilai sama */
.container-simple {
    display: grid;
    width: 500px;
    height: 400px;
    place-content: center;
}
```

**Penjelasan:** `place-content: center` akan membuat seluruh grid berada di tengah-tengah container.

### Space Distribution
```css
.space-distribution {
    display: grid;
    grid-template-columns: repeat(3, 100px);
    grid-template-rows: repeat(2, 80px);
    width: 500px;
    height: 300px;
    
    /* align-content: space-around, justify-content: space-between */
    place-content: space-around space-between;
}
```

**Hasil:** Grid akan memiliki space-around secara vertikal dan space-between secara horizontal.

## 3. place-self

### Sintaks
```css
.item {
    place-self: align-self justify-self;
    /* atau jika nilai sama */
    place-self: align-self;
}
```

### Contoh Penggunaan
```css
.container {
    display: grid;
    grid-template-columns: repeat(3, 150px);
    grid-template-rows: repeat(2, 120px);
    place-items: start; /* Default untuk semua items */
}

/* Override individual item */
.special-item {
    place-self: center; /* Item ini di tengah area */
}

.another-item {
    place-self: end start; /* Bawah-kiri area */
}
```

**Penjelasan:** 
- Semua items mulai dari start (kiri atas)
- `.special-item` akan di tengah-tengah area
- `.another-item` akan di bawah-kiri area

## Contoh Praktis: Card Layout

```css
.card-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 20px;
    padding: 20px;
    min-height: 100vh;
    
    /* Center semua cards dan grid */
    place-items: start;    /* Cards mulai dari atas area */
    place-content: center; /* Grid di tengah container */
}

.card {
    background: white;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 2px 8px rgba(0,0,0,0.1);
}

.featured-card {
    place-self: center; /* Card unggulan di tengah area */
    background: #f0f8ff;
    border: 2px solid #007acc;
}
```

## Contoh Layout: Navigation Center

```css
.nav-container {
    display: grid;
    grid-template-columns: repeat(4, auto);
    gap: 30px;
    width: 100%;
    height: 80px;
    background: #2c3e50;
    
    /* Center navigation items */
    place-items: center;
    place-content: center;
}

.nav-item {
    color: white;
    text-decoration: none;
    padding: 10px 20px;
    border-radius: 4px;
    transition: background 0.3s;
}

.nav-item:hover {
    background: rgba(255,255,255,0.1);
}

.nav-logo {
    place-self: center start; /* Logo di tengah-kiri */
    font-weight: bold;
    font-size: 1.2em;
}
```

## Responsive dengan place-shortcuts

```css
.responsive-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 20px;
    min-height: 100vh;
}

/* Mobile: center everything */
@media (max-width: 768px) {
    .responsive-grid {
        place-items: center;
        place-content: center;
    }
}

/* Desktop: align to start */
@media (min-width: 769px) {
    .responsive-grid {
        place-items: start;
        place-content: start center;
    }
}
```

## Kombinasi Praktis

```css
/* Layout halaman dengan perfect centering */
.page-layout {
    display: grid;
    grid-template-areas:
        "header"
        "main"
        "footer";
    grid-template-rows: auto 1fr auto;
    min-height: 100vh;
    
    place-content: stretch; /* Grid mengisi penuh */
}

.header {
    grid-area: header;
    display: grid;
    place-items: center; /* Konten header di tengah */
    padding: 20px;
    background: #34495e;
    color: white;
}

.main {
    grid-area: main;
    display: grid;
    place-items: center; /* Konten main di tengah */
    padding: 40px;
}

.footer {
    grid-area: footer;
    display: grid;
    place-items: center start; /* Tengah vertikal, kiri horizontal */
    padding: 15px;
    background: #2c3e50;
    color: white;
}
```

## Tips dan Best Practices

### 1. Gunakan Single Value untuk Centering
```css
/* ✅ Simpel dan jelas */
.center-everything {
    display: grid;
    place-items: center;
    place-content: center;
}
```

### 2. Mixed Values untuk Kontrol Presisi
```css
/* ✅ Kontrol berbeda untuk setiap axis */
.precise-control {
    display: grid;
    place-items: start center;    /* Atas-tengah */
    place-content: center start; /* Tengah-kiri */
}
```

### 3. Override Individual Items
```css
.container {
    display: grid;
    place-items: start; /* Default untuk semua */
}

.special {
    place-self: center end; /* Override untuk item khusus */
}
```

## Kesalahan yang Harus Dihindari

### 1. Salah Urutan Nilai
```css
/* ❌ Salah: menukar posisi align dan justify */
.wrong-order {
    place-items: center start; /* Ini: align=center, justify=start */
    /* Bukan: align=start, justify=center */
}

/* ✅ Ingat: align (vertikal) dulu, justify (horizontal) kedua */
.correct-order {
    place-items: start center; /* align=start, justify=center */
}
```

### 2. Menggunakan place-self pada Container
```css
/* ❌ Salah: place-self untuk container */
.container {
    display: grid;
    place-self: center; /* Tidak akan bekerja */
}

/* ✅ Benar: place-self untuk item */
.item {
    place-self: center;
}
```

### 3. Confusing place-items dan place-content
```css
/* place-items: untuk positioning ITEMS dalam area */
.container {
    place-items: center; /* Items di tengah area masing-masing */
}

/* place-content: untuk positioning GRID dalam container */
.container {
    place-content: center; /* Seluruh grid di tengah container */
}
```

## Format Penulisan

```css
/* Format lengkap */
place-items: align-value justify-value;
place-content: align-value justify-value;
place-self: align-value justify-value;

/* Format singkat (nilai sama) */
place-items: value;
place-content: value;
place-self: value;

/* Contoh praktis */
.example {
    place-items: center start;     /* tengah-kiri */
    place-content: start center;   /* atas-tengah */
    place-self: end;              /* bawah-tengah (shorthand) */
}
```

## Debugging place-shortcuts

```css
/* Visualisasi untuk debugging */
.debug-container {
    display: grid;
    place-items: center;
    border: 2px solid red;        /* Lihat container boundary */
    background: rgba(255,0,0,0.1); /* Background container */
}

.debug-item {
    border: 2px solid blue;       /* Lihat item boundary */
    background: rgba(0,0,255,0.1); /* Background item */
}
```

## Kesimpulan

Place-shortcuts membuat kode CSS Grid lebih:
- **Ringkas** - satu properti untuk dua fungsi
- **Readable** - intention lebih jelas
- **Maintainable** - lebih mudah diubah dan dipelihara

**Ingat urutan:** `align` (vertikal) selalu ditulis **sebelum** `justify` (horizontal) dalam shorthand properties.