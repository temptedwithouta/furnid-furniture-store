# Desain Struktur Statis Furnid

## Tujuan

Rapikan struktur proyek HTML/CSS statis Furnid agar mudah dipahami dan dirawat, sekaligus memperbaiki referensi aset dan tautan lokal yang saat ini tidak cocok. Tampilan dan isi situs dipertahankan.

## Kondisi dan batasan

- Tiga halaman yang ada adalah `index.html`, `shop.html`, dan `register.html` di root.
- Aset sudah berada di `assets/`; banyak referensi HTML dan CSS menggunakan `asset/`.
- CSS tiap halaman berada di root dan memiliki aturan dasar yang berulang.
- Belum ada JavaScript lokal. Tidak ada fitur baru atau bundler yang diminta.
- Situs harus tetap dapat dibuka sebagai situs statis tanpa proses build.

## Pendekatan

1. **Struktur statis sederhana (dipilih):** pertahankan halaman di root, pindahkan aturan bersama ke `css/base.css`, letakkan stylesheet khusus halaman di `css/`, dan pertahankan aset di `assets/`. Perbaiki jalur aset, tautan logo, dan struktur dokumen HTML. Ini menambah keteraturan tanpa memperkenalkan toolchain.
2. **Proyek dengan proses build:** pindahkan kode ke `src/` dan gunakan bundler untuk menghasilkan `dist/`. Ini berguna jika proyek memerlukan proses build, tetapi tidak diperlukan untuk situs statis saat ini.

## Struktur tujuan

```text
Furnid/
  index.html
  shop.html
  register.html
  css/
    base.css
    home.css
    shop.css
    register.css
  assets/
    home/
    shop/
    form/
    footer/
    images/
  README.md
```

JavaScript tidak ditambahkan hanya sebagai placeholder: folder atau file JS dibuat ketika ada perilaku situs yang memang memerlukannya. README akan mencerminkan teknologi yang benar-benar digunakan.

## Cakupan

- Ekstrak aturan CSS dasar yang berulang ke stylesheet bersama dan sesuaikan urutan pemuatan CSS di setiap halaman.
- Perbarui semua referensi `asset/` menjadi jalur yang sesuai dengan `assets/`, termasuk URL relatif di CSS setelah pemindahan.
- Arahkan tautan logo ke `index.html` dan betulkan struktur dokumen yang tidak lengkap.
- Pertahankan konten, tampilan, dan aset; tidak menambah fitur atau dependensi.
- Perbarui README jika diperlukan agar sesuai dengan struktur dan cara membuka situs.

## Kriteria selesai

- Ketiga halaman dapat dibuka secara statis dan tautan navigasi lokal mengarah ke halaman yang tersedia.
- Semua referensi lokal ke gambar, ikon, dan stylesheet menunjuk ke berkas yang ada.
- CSS bersama hanya didefinisikan sekali, sedangkan gaya khusus halaman tetap terpisah.
- Tidak ada perubahan visual atau fitur di luar perbaikan struktur dan tautan.