# E-Presensi

Aplikasi presensi siswa berbasis Google Apps Script + Google Spreadsheet.
Repositori ini berisi dua bagian:

| Folder / file | Fungsi |
|---|---|
| `apps-script/` | Kode aplikasi (`Code.gs`, `Index.html`, `appsscript.json`) yang dipasang di Apps Script |
| `index.html`, `config.js`, `manifest.webmanifest`, `icons/` | Halaman peluncur di GitHub Pages: alamat yang lebih rapi dan bisa dipasang di layar utama HP |

Data siswa, akun, dan absensi tersimpan di Google Spreadsheet Anda, **bukan** di repositori ini.

## 1. Pasang aplikasi di Apps Script

1. Buat Google Spreadsheet baru, lalu buka **Extensions → Apps Script**.
2. Tempel isi `apps-script/Code.gs`. Tambahkan file HTML bernama `Index` dan tempel isi `apps-script/Index.html`. Ganti isi manifest dengan `apps-script/appsscript.json` (aktifkan *Show appsscript.json* di Project Settings).
3. Muat ulang spreadsheet, jalankan menu **E-Presensi → Siapkan / perbaiki semua sheet**, lalu setujui izin yang diminta.
4. **Deploy → New deployment → Web app**: *Execute as* **Me**, *Who has access* **Anyone**. Salin alamat yang berakhiran `/exec`.

Akun awal: `admin` / `admin123`. Ganti segera di sheet `USER_MANAJEMEN`, lalu jalankan menu **Amankan password**.

## 2. Pasang di GitHub Pages

1. Buka `config.js`, ganti `appUrl` dengan alamat `/exec` dari langkah 1.
2. Buat repositori baru di GitHub dan unggah seluruh isi folder ini.
3. Di repositori: **Settings → Pages → Build and deployment → Source: Deploy from a branch**, pilih branch `main` dan folder `/ (root)`, lalu **Save**.
4. Tunggu 1–2 menit. Aplikasi tersedia di `https://<username>.github.io/<nama-repositori>/`.

GitHub Pages gratis hanya untuk repositori **publik**. Repositori publik ikut menampilkan kode di folder `apps-script/`; kode itu tidak berisi data siswa maupun kata sandi sungguhan.

Mode tampilan di `config.js`:

- `"embed"` (bawaan): aplikasi tampil di dalam halaman GitHub Pages.
- `"redirect"`: pengunjung langsung dibuka ke alamat Apps Script. Pakai ini bila tampilan di dalam halaman bermasalah.

## 3. Pasang di layar utama HP

- **Android (Chrome):** menu ⋮ → *Install app* / *Add to Home screen*.
- **iPhone (Safari):** tombol Bagikan → *Add to Home Screen*.

## 4. Memperbarui aplikasi

Ubah kode, tempel ulang di Apps Script, lalu **Deploy → Manage deployments → Edit → New version**. Alamat `/exec` tidak berubah, jadi `config.js` tidak perlu disentuh.

Bila ingin sinkron otomatis dari repositori, gunakan [clasp](https://github.com/google/clasp):

```bash
npm i -g @google/clasp
clasp login
cp .clasp.json.example .clasp.json   # isi scriptId (Project Settings di Apps Script)
clasp push                            # unggah isi apps-script/
```

## Catatan

- Di akun Google biasa, Apps Script menampilkan pita peringatan kecil di bagian atas aplikasi. Ini bawaan Google dan tidak bisa dihilangkan; akun Google Workspace tidak menampilkannya.
- Akses kamera untuk scan bisa diblokir browser pada halaman Apps Script. Bila terjadi, gunakan tab *Input / Scanner USB* atau *Foto QR* di halaman Scan.
- Menu Pengaturan di aplikasi (nama sekolah, alamat, logo) mengubah isi aplikasi, bukan ikon dan nama di halaman peluncur ini. Untuk mengganti ikon layar utama, ganti file di folder `icons/`.
