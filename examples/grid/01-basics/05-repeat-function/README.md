# CSS Grid - Repeat Function

## Penjelasan

`repeat()` adalah fungsi CSS Grid yang memungkinkan kita untuk mengulangi pola track (baris atau kolom) secara efisien tanpa perlu menulis kode yang berulang-ulang. Fungsi ini sangat berguna ketika kita ingin membuat grid dengan pola yang berulang.

**Sintaks dasar:**
```css
repeat(jumlah_pengulangan, ukuran_track)
```

## Contoh Dasar dan Penjelasan

### 1. Pengulangan Sederhana

```css
.container {
  display: grid;
  /* Membuat 4 kolom dengan lebar 100px masing-masing */
  grid-template-columns: repeat(4, 100px);
  
  /* Sama dengan menulis: */
  /* grid-template-columns: 100px 100px 100px 100px; */
}
```

### 2. Pengulangan dengan Unit Fleksibel

```css
.container {
  display: grid;
  /* Membuat 3 kolom yang sama lebar menggunakan fr unit */
  grid-template-columns: repeat(3, 1fr);
  
  /* Membuat 4 baris dengan tinggi 50px */
  grid-template-rows: repeat(4, 50px);
}
```

### 3. Pengulangan Pola Kompleks

```css
.container {
  display: grid;
  /* Mengulangi pola: 200px 100px sebanyak 3 kali */
  grid-template-columns: repeat(3, 200px 100px);
  
  /* Hasil: 200px 100px 200px 100px 200px 100px */
}
```

## Jenis-jenis Repeat Function

### 1. `repeat()` dengan Angka Tetap
```css
.grid {
  grid-template-columns: repeat(5, 1fr);
}
```

### 2. `auto-fit` - Menyesuaikan Jumlah Kolom
```css
.grid {
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
}
```
- Membuat kolom sebanyak mungkin yang muat dalam container
- Kolom kosong akan "collapsed" (disembunyikan)

### 3. `auto-fill` - Mengisi Ruang Kosong
```css
.grid {
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
}
```
- Membuat kolom sebanyak mungkin yang muat dalam container
- Kolom kosong tetap ada (tidak collapsed)

## Contoh Praktis

### Responsive Grid Card Layout
```css
.card-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 20px;
  padding: 20px;
}

.card {
  background: #f0f0f0;
  padding: 20px;
  border-radius: 8px;
}
```

### Grid dengan Pola Berulang
```css
.pattern-grid {
  display: grid;
  grid-template-columns: repeat(4, 50px 100px 150px);
  gap: 10px;
}
```

## Kesalahan yang Harus Dihindari

### ❌ Kesalahan 1: Menggunakan Nilai Negatif
```css
/* SALAH */
.grid {
  grid-template-columns: repeat(-3, 100px);
}
```

### ❌ Kesalahan 2: Mencampur auto-fit/auto-fill dengan Angka Spesifik
```css
/* SALAH */
.grid {
  grid-template-columns: repeat(auto-fit, 100px) 200px;
}
```

### ❌ Kesalahan 3: Menggunakan Persentase Tanpa Konteks yang Jelas
```css
/* BERMASALAH - bisa menyebabkan overflow */
.grid {
  grid-template-columns: repeat(5, 25%);
  gap: 20px; /* Gap akan menyebabkan total lebih dari 100% */
}
```

### ❌ Kesalahan 4: Tidak Mempertimbangkan Responsivitas
```css
/* KURANG BAIK - tidak responsif */
.grid {
  grid-template-columns: repeat(4, 300px);
}

/* LEBIH BAIK */
.grid {
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
}
```

## Best Practices

### 1. Gunakan `minmax()` untuk Responsivitas
```css
.responsive-grid {
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
}
```

### 2. Kombinasikan dengan `gap` untuk Spacing
```css
.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
}
```

### 3. Gunakan Custom Properties untuk Fleksibilitas
```css
.grid {
  --columns: 4;
  --min-width: 200px;
  
  display: grid;
  grid-template-columns: repeat(var(--columns), 1fr);
}

@media (max-width: 768px) {
  .grid {
    --columns: 2;
  }
}
```

### 4. Pertimbangkan Performa dengan Banyak Item
```css
/* Untuk grid dengan banyak item */
.large-grid {
  grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
  grid-auto-rows: 150px;
}
```

## Perbedaan `auto-fit` vs `auto-fill`

### auto-fit
```css
.grid-fit {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 20px;
}
```
- Kolom kosong akan collapse
- Item akan stretch untuk mengisi ruang kosong

### auto-fill
```css
.grid-fill {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 20px;
}
```
- Kolom kosong tetap ada
- Item tidak akan stretch ke kolom kosong

## Kasus Penggunaan Umum

### 1. Photo Gallery
```css
.photo-gallery {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 15px;
}
```

### 2. Dashboard Layout
```css
.dashboard {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  gap: 20px;
}

.widget {
  grid-column: span 4; /* Mengambil 4 kolom */
}
```

### 3. Form Layout
```css
.form-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 20px;
}

.full-width {
  grid-column: 1 / -1; /* Mengambil semua kolom */
}
```

## Tips Debugging

1. **Gunakan Firefox Grid Inspector** untuk visualisasi
2. **Tambahkan border sementara** untuk melihat layout
3. **Gunakan `grid-auto-flow: dense`** untuk mengisi gap otomatis
4. **Periksa total ukuran** saat menggunakan unit tetap dengan gap

## Kesimpulan

`repeat()` function adalah alat yang sangat powerful dalam CSS Grid yang memungkinkan kita membuat layout yang fleksibel dan responsif dengan kode yang lebih bersih. Kombinasikan dengan `auto-fit`, `auto-fill`, dan `minmax()` untuk hasil yang optimal.

Ingat untuk selalu mempertimbangkan responsivitas dan user experience saat menggunakan repeat function dalam project Anda.