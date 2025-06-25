# Panduan Lengkap CSS Grid untuk Pemula

## 1. Apa itu CSS Grid?

CSS Grid adalah sistem layout 2 dimensi yang memungkinkan kita mengatur elemen dalam baris (rows) dan kolom (columns) secara bersamaan. Berbeda dengan Flexbox yang hanya 1 dimensi (horizontal ATAU vertikal), Grid bisa mengatur keduanya sekaligus.

## 2. Konsep Dasar

### Grid Container vs Grid Items
- **Grid Container**: Elemen parent yang menggunakan `display: grid`
- **Grid Items**: Elemen-elemen child di dalam grid container

### Terminologi Penting
- **Grid Lines**: Garis pembagi yang membentuk grid
- **Grid Tracks**: Ruang antara dua grid lines (baris atau kolom)
- **Grid Cells**: Pertemuan antara satu baris dan satu kolom
- **Grid Areas**: Kumpulan beberapa grid cells

## 3. Properti Dasar Grid Container

### Mengaktifkan Grid
```css
.container {
  display: grid;
}
```

### Membuat Kolom dan Baris
```css
.container {
  display: grid;
  
  /* Membuat 3 kolom dengan lebar yang sama */
  grid-template-columns: 1fr 1fr 1fr;
  /* atau singkatnya: */
  grid-template-columns: repeat(3, 1fr);
  
  /* Membuat 2 baris dengan tinggi 200px */
  grid-template-rows: 200px 200px;
}
```

### Unit dalam Grid
- **fr**: Fraction unit (bagian), sangat fleksibel
- **px**: Pixel, ukuran tetap
- **%**: Persentase dari container
- **auto**: Ukuran sesuai konten

## 4. Solusi untuk Kasus Anda: 10 Card, 3 per Baris

Untuk membuat layout 10 card dengan 3 card per baris yang otomatis turun ke baris berikutnya:

```css
.card-container {
  display: grid;
  grid-template-columns: repeat(3, 1fr); /* 3 kolom sama lebar */
  gap: 20px; /* Jarak antar card */
  padding: 20px;
}

.card {
  background: #f0f0f0;
  padding: 20px;
  border-radius: 8px;
  text-align: center;
}
```

## 5. Mengatur Posisi dan Alignment

### Alignment Horizontal (Justify)
```css
.container {
  display: grid;
  justify-items: center;    /* center, start, end, stretch */
  justify-content: center;  /* untuk seluruh grid */
}
```

### Alignment Vertikal (Align)
```css
.container {
  display: grid;
  align-items: center;      /* center, start, end, stretch */
  align-content: center;    /* untuk seluruh grid */
}
```

### Alignment Gabungan
```css
.container {
  display: grid;
  place-items: center;      /* shorthand untuk align-items + justify-items */
  place-content: center;    /* shorthand untuk align-content + justify-content */
}
```

## 6. Grid Gap (Jarak)

```css
.container {
  display: grid;
  gap: 20px;              /* jarak sama untuk baris dan kolom */
  /* atau: */
  row-gap: 20px;          /* jarak antar baris */
  column-gap: 15px;       /* jarak antar kolom */
}
```

## 7. Responsive Grid

### Auto-fit vs Auto-fill
```css
/* Auto-fit: kolom menyesuaikan ruang yang tersedia */
.container {
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
}

/* Auto-fill: membuat kolom sebanyak mungkin */
.container {
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
}
```

## 8. Contoh Praktis: Layout Card Responsif

```css
.card-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 20px;
  padding: 20px;
  max-width: 1200px;
  margin: 0 auto;
}

/* Untuk layar kecil, paksa 1 kolom */
@media (max-width: 768px) {
  .card-grid {
    grid-template-columns: 1fr;
  }
}
```

## 9. Tips Praktis

### Debugging Grid
Gunakan browser developer tools dan aktifkan grid overlay untuk melihat struktur grid.

### Grid Template Areas
Untuk layout yang lebih kompleks:
```css
.layout {
  display: grid;
  grid-template-areas: 
    "header header header"
    "sidebar main main"
    "footer footer footer";
  grid-template-columns: 200px 1fr 1fr;
  grid-template-rows: auto 1fr auto;
}

.header { grid-area: header; }
.sidebar { grid-area: sidebar; }
.main { grid-area: main; }
.footer { grid-area: footer; }
```

## 10. Perbedaan Grid vs Flexbox

| Grid | Flexbox |
|------|---------|
| 2 dimensi (baris + kolom) | 1 dimensi (baris ATAU kolom) |
| Layout dari container ke item | Layout dari item ke container |
| Cocok untuk layout halaman | Cocok untuk komponen |
| Explicit positioning | Content-based positioning |

## Kesimpulan

CSS Grid sangat powerful untuk membuat layout yang kompleks. Mulai dengan konsep dasar:
1. `display: grid` untuk mengaktifkan
2. `grid-template-columns` untuk kolom
3. `gap` untuk jarak
4. `place-items: center` untuk alignment

Dengan memahami dasar-dasar ini, Anda sudah bisa membuat layout card 3 per baris seperti yang Anda inginkan!