# Form Stock Take Asset — Upload Excel (v1.2)

Aplikasi web **single‑file (HTML + CSS + JS)** untuk membantu proses **stock take asset**: unggah **Excel/CSV** master asset, **scan QR/kamera** atau ketik **Kode Asset**, catat hasil per item, lalu **ekspor CSV**. Seluruh pemrosesan berjalan **di browser** (client‑side), tanpa server.

> File utama: `form_stock_take_asset_upload_v1_2.html`

---

## ✨ Fitur Utama

- **Unggah Excel/CSV**  
  - Pilih **Sheet** untuk file Excel.  
  - **Auto‑mapping header** (toleran variasi nama kolom).
- **Input / Scan Kode Asset**  
  - Ketik manual atau **scan QR** via kamera (webkit/Chrome/Edge/Firefox yang mendukung).
- **Perhitungan otomatis**  
  - Tampilkan **Master Unit**, **Qty Dihitung**, **Sisa**, dan **Delta**.
- **Pencatatan ke List (LocalStorage)**  
  - Simpan data **lokal** (tidak terkirim ke server).  
  - Hapus baris per item, **Reset List** bila diperlukan.
- **Tabel “Belum Distock”**  
  - Otomatis menampilkan item master yang **belum masuk List**.  
  - **Filter Lokasi** dan **Filter Type**.
- **Ekspor**  
  - **Export CSV** hasil pencatatan.  
  - **Export Belum Distock** untuk daftar yang belum disentuh.
- **Tanggal Stock**  
  - Tersimpan di **LocalStorage**, default ke tanggal hari ini.
- **Antarmuka Dark Theme**, ringan, responsif.

> **Kamera/QR butuh HTTPS** agar `getUserMedia()` aktif di browser. GitHub Pages sudah HTTPS dan bisa **Enforce HTTPS** di pengaturan.  
> Referensi: [GitHub Pages HTTPS](https://docs.github.com/en/pages/getting-started-with-github-pages/securing-your-github-pages-site-with-https), [MDN getUserMedia() (Secure Context)](https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices/getUserMedia).

---

## 🧩 Teknologi yang Digunakan

- **[SheetJS (xlsx)](https://docs.sheetjs.com/docs/solutions/input/)** — baca Excel di browser.  
- **[Papa Parse](https://www.papaparse.com/)** — parsing CSV cepat (dukungan file besar & web worker).  
- **[jsQR](https://www.jsdelivr.com/package/npm/jsqr)** — pemindaian QR dari frame video (kamera).  
- **Vanilla JS + DOM API** — tanpa framework.

---

## 🚀 Menjalankan

### 1) Buka Lokal
Cukup **double‑click** `form_stock_take_asset_upload_v1_2.html`.

> Catatan: akses **kamera** biasanya **TIDAK** aktif di file `file:///` (non‑HTTPS). Untuk uji kamera, gunakan **server lokal** dengan HTTPS atau deploy ke **GitHub Pages**.

### 2) Deploy ke **GitHub Pages**
1. Commit & push file HTML ke repo.  
2. Buka **Settings → Pages**, pilih **Source** (mis. `main` / root atau `/docs`), **Save**.  
3. Aktifkan **Enforce HTTPS**.  
4. Akses:  
   - **User/Org site**: `https://<username>.github.io/form_stock_take_asset_upload_v1_2.html`  
   - **Project site**: `https://<username>.github.io/<repo>/form_stock_take_asset_upload_v1_2.html`

Panduan resmi: [Creating a GitHub Pages site](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site) • [Enforce HTTPS](https://docs.github.com/en/pages/getting-started-with-github-pages/securing-your-github-pages-site-with-https)

---

## 📄 Format Data Master (Header yang Didukung)

Aplikasi melakukan **normalisasi header** secara otomatis. Gunakan salah satu variasi di bawah:

- **Kode Asset**: `Kode Asset`, `Kode`, `Asset Code`, `Code`, `Kode Aset`  
- **Nama**: `Asset Name`, `Nama Asset`, `Nama Aset`, `Item Name`, `Name`  
- **Jumlah Unit (Master)**: `Jumlah Unit`, `Master Unit`, `Qty`, `Quantity`, `Qty Master`  
- **Lokasi**: `Location`, `Lokasi`  
- **Ruang**: `Room`, `Ruang`  
- **Type/Kategori**: `Type`, `Tipe`, `Kategori`, `Category`  
- **Status**: `Status`  
- **Model**: `Model`  
- **Serial**: `Serial`, `Serial Number`, `SN`

> Minimal kolom yang disarankan: **Kode Asset**, **Asset Name**, **Jumlah Unit (Master)**.  
> Parsing Excel/CSV: [SheetJS Input](https://docs.sheetjs.com/docs/solutions/input/), [Papa Parse](https://www.papaparse.com/).

**Contoh CSV**:


Kode Asset,Asset Name,Jumlah Unit,Location,Room,Type,Status,Model,Serial
AST-000123,Laptop Lenovo,1,Office,IT Room,IT,Ada,ThinkPad X1,SN12345
AST-000124,Printer HP,2,Office,Printing,Office,Ada,HP 402d,SN98765
