# Furnid Static Structure Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Rapikan struktur situs statis Furnid dan perbaiki referensi lokal tanpa mengubah isi atau tampilan halaman.

**Architecture:** Pertahankan tiga file HTML di root dan seluruh aset di `assets/`. Pindahkan CSS ke `css/`, ekstrak aturan bersama yang benar-benar sama ke `css/base.css`, dan pertahankan CSS khusus halaman. Situs tetap tanpa build tool; JavaScript tidak ditambahkan tanpa perilaku yang membutuhkannya.

**Tech Stack:** HTML5, CSS3, browser statis; tanpa dependency atau build step baru.

**Spec:** [docs/superpowers/specs/2026-11-07-furnid-static-structure-design.md](../specs/2026-11-07-furnid-static-structure-design.md)

## Global Constraints

- Tampilan dan isi situs dipertahankan.
- Situs harus tetap dapat dibuka sebagai situs statis tanpa proses build.
- Aset tetap berada di `assets/`.
- Tidak menambah fitur atau dependensi.
- JavaScript tidak ditambahkan hanya sebagai placeholder.

## Review Focus

- Urutan pemuatan CSS dapat mengubah cascade; bandingkan tampilan ketiga halaman dengan screenshot sebelum perubahan pada viewport yang sama.
- Pemindahan CSS dapat memutus URL relatif; pastikan background CSS masih dimuat.
- Jalur gambar yang memakai `asset/` harus diperbaiki; pastikan seluruh gambar lokal tampil.
- Logo tidak boleh menuju `home.html` yang tidak tersedia; pastikan semua logo kembali ke `index.html`.
- Struktur dokumen yang belum lengkap dapat mengubah parsing browser; pastikan ketiga halaman terbuka tanpa masalah markup yang terlihat dan label persetujuan terkait dengan input-nya.

---

### Task 1: Susun CSS Bersama dan Khusus Halaman

**Files:**
- Create: `css/base.css`
- Move: `home.css` to `css/home.css`
- Move: `shop.css` to `css/shop.css`
- Move: `register.css` to `css/register.css`
- Modify: `index.html`, `shop.html`, `register.html`

**Interfaces:**
- Menghasilkan stylesheet dasar bersama `css/base.css`, dimuat sebelum stylesheet khusus halaman.
- Ketiga stylesheet khusus halaman mempertahankan aturan yang tidak dibagi.

- [ ] **Step 1: Catat tampilan sebelum perubahan**

  Buka `index.html`, `shop.html`, dan `register.html` pada browser. Simpan screenshot tiap halaman pada viewport desktop dan mobile yang sama untuk dibandingkan setelah refactor. Catat asset yang memang belum tampil akibat referensi `asset/` yang sudah ada.

- [ ] **Step 2: Identifikasi aturan CSS yang benar-benar bersama**

  Bandingkan `home.css`, `shop.css`, dan `register.css`. Tentukan aturan reset, tipografi, header/navigasi, dan footer yang sama secara semantik; jangan satukan aturan yang nilainya berbeda atau hanya kebetulan memiliki selector yang sama.

- [ ] **Step 3: Pindahkan aturan dan stylesheet**

  Pindahkan aturan bersama ke `css/base.css`, pertahankan aturan halaman di masing-masing stylesheet, lalu pindahkan ketiga file CSS ke `css/`. Pertahankan urutan impor font yang ada dengan memuatnya satu kali di `base.css`. Untuk setiap `url(...)` di CSS yang dipindahkan, sesuaikan jalur relatif agar menunjuk ke aset yang sama di `../assets/`.

- [ ] **Step 4: Perbarui urutan stylesheet di HTML**

  Di tiap halaman, muat `css/base.css` sebelum stylesheet halamannya (`css/home.css`, `css/shop.css`, atau `css/register.css`).

- [ ] **Step 5: Verifikasi CSS dan tampilan**

  Pastikan keempat stylesheet ada dan seluruh tautan stylesheet di HTML menunjuk ke file yang ada. Buka kembali ketiga halaman dan bandingkan screenshot desktop/mobile dengan baseline; pastikan tidak ada pergeseran gaya yang tidak diinginkan serta background CSS tetap tampil.

### Task 2: Betulkan Markup dan Referensi Lokal

**Files:**
- Modify: `index.html`, `shop.html`, `register.html`

**Interfaces:**
- Semua jalur aset menggunakan root direktori `assets/` yang sudah ada.
- Semua tautan logo menuju `index.html`.

- [ ] **Step 1: Betulkan jalur aset dan tautan logo**

  Di tiga file HTML, ganti referensi aset `asset/...` menjadi jalur yang cocok dengan `assets/...` tanpa memindahkan atau mengganti nama file aset. Ganti tautan logo `home.html` menjadi `index.html`.

- [ ] **Step 2: Lengkapi struktur dokumen HTML**

  Pastikan setiap halaman memiliki penutup `</head>` sebelum `<body>`. Di `register.html`, samakan nilai `for` label persetujuan dengan `id="terms"` pada checkbox.

- [ ] **Step 3: Verifikasi halaman dan tautan lokal**

  Buka tiap halaman melalui `index.html`, lalu uji tautan navigasi dan logo. Periksa tampilan gambar produk, ikon, banner, serta gambar form; pastikan tak ada gambar atau stylesheet lokal yang gagal dimuat.

### Task 3: Selaraskan README dan Pemeriksaan Akhir

**Files:**
- Modify: `README.md`

**Interfaces:**
- README menjelaskan struktur file aktual dan cara membuka situs statis.
- README tidak menyatakan JavaScript sebagai teknologi yang digunakan selama belum ada skrip lokal.

- [ ] **Step 1: Perbarui panduan proyek**

  Dokumentasikan struktur root HTML, direktori `css/`, dan `assets/`; jelaskan bahwa `index.html` dapat dibuka langsung di browser. Hapus klaim JavaScript yang belum sesuai dengan proyek.

- [ ] **Step 2: Lakukan pemeriksaan penerimaan**

  Buka `index.html`, `shop.html`, dan `register.html` secara langsung di browser. Pastikan navigasi, seluruh gambar, stylesheet, dan background CSS tampil/mengarah dengan benar serta screenshot tetap konsisten dengan baseline. Pastikan tidak ada referensi HTML/CSS yang masih memakai `asset/` atau `home.html`.

- [ ] **Step 3: Tinjau diff akhir**

  Pastikan perubahan hanya mencakup pengorganisasian CSS, perbaikan struktur dan referensi HTML, serta pembaruan README. Jangan commit tanpa permintaan.