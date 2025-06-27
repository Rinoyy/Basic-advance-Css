# CSS Grid FR Units - Panduan Lengkap

## Apa itu FR Units?

**FR (Fractional Unit)** adalah unit pengukuran khusus dalam CSS Grid yang mewakili **"fraction"** atau bagian dari ruang kosong yang tersedia dalam grid container. Unit `fr` secara otomatis mendistribusikan ruang yang tersisa setelah semua item dengan ukuran tetap (seperti `px`, `em`, `%`) telah dialokasikan.

**Note terjemahan:** Fractional = Pecahan

## Cara Kerja FR Units

FR units bekerja dengan prinsip **pembagian proporsional**:

1. **Hitung ruang tersedia**: Grid menghitung sisa ruang setelah elemen dengan ukuran tetap
2. **Jumlahkan semua fr**: Semua nilai `fr` dijumlahkan untuk mendapat total bagian
3. **Bagi proporsional**: Setiap kolom/baris mendapat bagian sesuai rasio fr-nya

### Contoh Dasar

```css
.grid-container {
  display: grid;
  grid-template-columns: 1fr 2fr 1fr;
  gap: 16px;
  height: 100vh;
}
```

**Penjelasan:**
- Total fr = 1 + 2 + 1 = 4 bagian
- Kolom 1: 1/4 = 25% dari ruang tersedia
- Kolom 2: 2/4 = 50% dari ruang tersedia  
- Kolom 3: 1/4 = 25% dari ruang tersedia

## Jenis-Jenis Penggunaan FR Units

### 1. FR Murni (Pure FR)
```css
.grid-equal {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  /* Tiga kolom dengan lebar sama */
}
```

### 2. FR dengan Ukuran Tetap (Mixed Units)
```css
.grid-mixed {
  display: grid;
  grid-template-columns: 200px 1fr 100px;
  /* Kolom tetap 200px, tengah fleksibel, kanan tetap 100px */
}
```

### 3. FR dengan Rasio Berbeda
```css
.grid-ratio {
  display: grid;
  grid-template-columns: 1fr 3fr 2fr;
  /* Rasio 1:3:2 dari ruang tersedia */
}
```

### 4. FR untuk Rows
```css
.grid-rows {
  display: grid;
  grid-template-rows: auto 1fr auto;
  height: 100vh;
  /* Header otomatis, konten fleksibel, footer otomatis */
}
```

auto pada baris kode di atas akan sesuai dengan kontent, semisal pada contoh di bawah ini
Height: 1000PX
Header: memiliki kontent dengan height 200 (auto)
Footer: memiliki kontent 100Px (auto)
Total = 300Px jadi 1000px - 300px = 700 adalah nilai fr


## Perbedaan FR vs Unit Lain

| Unit | Perilaku | Kapan Gunakan |
|------|----------|---------------|
| `fr` | Relatif terhadap ruang tersisa | Layout responsif, pembagian proporsional |
| `%` | Relatif terhadap parent container | Persentase dari total lebar |
| `px` | Ukuran absolut tetap | Sidebar, header dengan lebar pasti |
| `auto` | Sesuai konten | Kolom yang menyesuaikan isi |

## Best Practices

### ✅ DO (Lakukan)

1. **Gunakan fr untuk layout responsif**
```css
.responsive-grid {
  grid-template-columns: 1fr 1fr 1fr;
  /* Otomatis responsif di semua ukuran layar */
}
```

2. **Kombinasi dengan minmax() untuk kontrol lebih baik**
```css
.controlled-grid {
  grid-template-columns: minmax(200px, 1fr) 2fr minmax(150px, 1fr);
  /* Kolom punya batas minimum tapi tetap fleksibel */
}
```

3. **Gunakan untuk area konten utama**
```css
.layout {
  grid-template-columns: 250px 1fr 200px;
  /* Sidebar tetap, konten fleksibel, widget tetap */
}
```

### ❌ DON'T (Hindari)

1. **Jangan gunakan fr jika butuh ukuran eksak**
```css
/* ❌ Salah untuk logo yang butuh ukuran pasti */
.logo-area {
  grid-template-columns: 1fr;
}

/* ✅ Benar */
.logo-area {
  grid-template-columns: 120px;
}
```

2. **Hindari terlalu banyak variasi fr**
```css
/* ❌ Sulit dipahami */
.confusing {
  grid-template-columns: 1.5fr 2.7fr 0.8fr 3.2fr;
}

/* ✅ Lebih jelas */
.clear {
  grid-template-columns: 1fr 2fr 1fr 3fr;
}
```

## Yang Perlu Diperhatikan

### 1. **Overflow Handling**
```css
.safe-grid {
  grid-template-columns: minmax(0, 1fr) minmax(0, 1fr);
  /* minmax(0, 1fr) mencegah overflow pada konten panjang */
}
```

### 2. **Performance dengan Grid Besar**
```css
/* Untuk grid dengan banyak item, pertimbangkan auto-fit/auto-fill */
.responsive-cards {
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
}
```

### 3. **Browser Support**
- FR units didukung semua browser modern (IE 10+)
- Untuk browser lama, sediakan fallback

```css
.grid-fallback {
  /* Fallback untuk browser lama */
  display: table;
  width: 100%;
}

.grid-fallback {
  /* Grid modern */
  display: grid;
  grid-template-columns: 1fr 2fr 1fr;
}
```

## Contoh Praktis Lengkap

```css
/* Layout Website Umum */
.website-layout {
  display: grid;
  grid-template-areas: 
    "header header header"
    "sidebar main ads"
    "footer footer footer";
  grid-template-columns: 200px 1fr 150px;
  grid-template-rows: auto 1fr auto;
  min-height: 100vh;
  gap: 16px;
}

.header { grid-area: header; }
.sidebar { grid-area: sidebar; }
.main { grid-area: main; }
.ads { grid-area: ads; }
.footer { grid-area: footer; }
```

**Penjelasan Layout:**
- **Header & Footer**: Tinggi otomatis sesuai konten
- **Sidebar**: Lebar tetap 200px untuk navigasi
- **Main**: Menggunakan 1fr - mengambil semua sisa ruang
- **Ads**: Lebar tetap 150px untuk iklan
- **Main Content**: Fleksibel dan responsif berkat 1fr

## Tips Advanced

### 1. **Nested FR Units**
```css
.nested-grid {
  grid-template-columns: 1fr 2fr;
}

.nested-grid .child {
  display: grid;
  grid-template-columns: 1fr 1fr; /* FR dalam FR tetap proporsional */
}
```

### 2. **FR dengan CSS Custom Properties**
```css
:root {
  --sidebar-ratio: 1fr;
  --content-ratio: 3fr;
}

.dynamic-grid {
  grid-template-columns: var(--sidebar-ratio) var(--content-ratio);
}
```

FR units adalah fondasi penting untuk membuat layout CSS Grid yang fleksibel dan responsif. Dengan memahami cara kerjanya, Anda bisa membuat layout yang adaptive tanpa media queries yang rumit!