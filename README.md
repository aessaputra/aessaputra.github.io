# Dokumentasi Teknis

Repositori ini menyajikan catatan Obsidian ke dalam situs statis berbasis Jekyll Garden. Dokumen ini merangkum informasi teknis untuk setup lokal, struktur konten, penyesuaian tampilan, serta proses build dan deploy.

## Ringkasan Proyek

- Theme Jekyll yang mengubah catatan markdown (`_notes`) menjadi halaman web dengan dukungan wiki-style link `[[...]]`.
- Fitur utama: pencarian instan, backlinks, preview halaman, dukungan KaTeX, dan mode terang/gelap.
- Situs diatur melalui `_config.yml` dan memanfaatkan koleksi Jekyll (`collections`) untuk catatan.
- Output statis dihasilkan ke `_site/` baik secara lokal (`bundle exec jekyll serve`) maupun saat build CI/CD.

## Prasyarat Lingkungan

- Ruby 3.1+ dan Bundler (`gem install bundler`) untuk menjalankan Jekyll.
- Paket build-essential dan dependensi Ruby (di Debian/Ubuntu: `sudo apt install build-essential ruby-dev`).
- Opsional: Node.js/NPM bila ingin menambah pipeline build asset.
- Browser modern untuk memeriksa hasil build lokal.

## Menjalankan Secara Lokal

```bash
# 1. Pasang dependensi Ruby
bundle install

# 2. Jalankan server pengembangan (localhost:4000)
bundle exec jekyll serve --livereload

# 3. Hentikan server dengan Ctrl+C
```

Gunakan flag `--baseurl ''` ketika mengakses situs dari folder lokal tanpa struktur direktori GitHub Pages. Setiap perubahan pada markdown langsung tercermin setelah reload, kecuali `_config.yml` yang memerlukan restart server.

## Struktur Direktori

```
.
├── _config.yml          # Konfigurasi global situs, menu, plugin, preferensi
├── _includes/           # Komponen HTML untuk di-include (mis. Content.html)
├── _layouts/            # Template layout (Post.html dsb)
├── _notes/              # Sumber catatan publik yang dipublikasikan
├── _posts/              # Tulisan blog standar (format YYYY-MM-DD-judul.md)
├── assets/              # CSS, font, dan aset statis lain
├── pages/               # Halaman statis seperti /notes, /writing, /about
├── utilities/           # Skrip/helper tambahan terkait konten
├── SearchData.json      # Index pencarian yang dibuat saat build
└── autocomplete.txt     # Sumber data untuk fitur autocomplete pencarian
```

Direktori `_site/` dibuat otomatis saat proses build; isi folder ini tidak perlu dikomit karena bersifat artifact.

## Penulisan Konten

### Catatan (`_notes/`)

- Setiap file markdown wajib memiliki front matter YAML minimal `title`.
- Gunakan `[[Nama Catatan]]` untuk membuat tautan internal; ketika build, sistem akan membuat relasi dan backlink otomatis.
- Front matter tambahan:
  - `aliases`: array string untuk nama alternatif catatan.
  - `date` dan `updated`: membantu menyinkronkan catatan dengan penulisan manual.
  - `permalink`: override URL default jika diperlukan.

### Tulisan Blog (`_posts/`)

- Ikuti penamaan Jekyll: `YYYY-MM-DD-judul.md`.
- Front matter default memanfaatkan `layout: Post` dan `content-type: post` sehingga tampil dengan gaya blog.
- URL hasil sesuai pola `_config.yml` → `/writing/:title/`.

### Halaman Statis (`pages/`)

- Digunakan untuk halaman khusus (`/notes`, `/writing`, `/about`, dsb).
- Front matter `layout` dapat disesuaikan dengan layout yang tersedia atau custom layout baru.
- Konten mendukung Liquid tags dan include komponen (\_includes).

## Kustomisasi Tampilan

- CSS utama berada di `assets/css/style.css`. Gunakan file ini untuk override warna, tipografi, spacing, dan layout.
- `assets/css/ie-target.css` disertakan untuk kompatibilitas IE lama; bisa diabaikan bila tidak dibutuhkan.
- Komponen HTML modular berada di `_includes/` (misal `Content.html` dan `Head.html`). Modifikasi komponen di sini agar perubahan reuse antar halaman.
- Layout `Post.html` menentukan struktur artikel. Tambahkan blok Liquid di sini bila perlu menampilkan metadata tambahan.

## Konfigurasi Utama (`_config.yml`)

- `preferences`: mengaktifkan/menonaktifkan fitur (homepage khusus, pencarian, backlinks, dsb).
- `menu`: mengatur tautan navigasi utama.
- `collections.notes`: memastikan catatan dirender ke `/notes/<nama>`.
- `katex: true`: mengaktifkan rendering matematika; jika tidak perlu, set ke false.
- `plugins`: default `jekyll-feed` (RSS) dan `jekyll-sitemap`. Tambah plugin lain dengan menambah daftar dan memperbarui `Gemfile`.

Setiap perubahan plugin atau dependensi wajib diikuti dengan `bundle install`.

## Build & Deploy

### GitHub Pages

1. Push branch utama ke GitHub.
2. Aktifkan GitHub Pages dari pengaturan repository, sumber branch `main` / folder `/ (root)`.
3. Pastikan `baseurl` di `_config.yml` sesuai (misal kosong untuk situs utama, atau `/notes` untuk subdirektori).

### Build Manual

```bash
bundle exec jekyll build
# hasil build tersedia di _site/
```

Salin isi `_site/` ke layanan hosting statis lain (Netlify, Vercel, Cloudflare Pages). Sesuaikan environment variable `JEKYLL_ENV=production` saat build jika ingin mengaktifkan optimisasi tertentu.

## Pencarian & Autocomplete

- `SearchData.json` dan `autocomplete.txt` dihasilkan selama proses build; file ini digunakan oleh JavaScript pencarian untuk menyediakan hasil instan.
- Jika menambah field metadata khusus, perbarui generator search (lihat `_includes` terkait pencarian) agar indeks memuat data baru.
- Hapus file-file tersebut sebelum commit apabila ingin memaksa rebuild indeks pada server.

## Troubleshooting

- `bundle exec jekyll serve` gagal karena ketergantungan Ruby → jalankan `bundle install` atau periksa versi Ruby (`ruby -v`).
- Perubahan CSS tidak muncul → bersihkan cache browser atau pakai `jekyll serve --livereload`.
- Broken link `[[...]]` → pastikan nama file target publik dan cocok dengan nama catatan tanpa ekstensi.
- Build GitHub Pages gagal → cek log Actions, pastikan `Gemfile.lock` tersinkronisasi dengan environment Ruby 3.x.

## Lisensi

Konten kode berada di bawah lisensi MIT (lihat `LICENSE`). Konten catatan dapat menggunakan lisensi berbeda sesuai pernyataan hak cipta pada `_config.yml`.
