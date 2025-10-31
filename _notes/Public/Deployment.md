---
title: Deployment
feed: show
date: 2024-01-15
---
Setelah situs Jekyll Garden selesai disiapkan, berikut cara memublikasikannya secara daring.

## GitHub Pages (Gratis)

GitHub Pages adalah cara termudah untuk memulai:

1. **Unggah seluruh berkas** ke repositori GitHub
2. **Aktifkan GitHub Pages** di pengaturan repositori
3. **Atur sumber** ke "Deploy from a branch"
4. **Pilih branch utama** (biasanya `main` atau `master`)

Situsmu akan tersedia di `https://usernamekamu.github.io/nama-repositori`

## Netlify (Gratis)

Netlify menawarkan proses deploy otomatis:

1. **Hubungkan repositori GitHub** ke Netlify
2. **Atur perintah build**: `bundle exec jekyll build`
3. **Atur direktori hasil build**: `_site`
4. **Deploy otomatis** setiap kali kamu melakukan push

## Vercel (Gratis)

Vercel juga menjadi opsi yang baik:

1. **Impor repositorimu** ke Vercel
2. **Framework preset**: Jekyll
3. **Deploy otomatis** pada setiap push

## Pengujian Lokal

Uji situs sebelum melakukan deploy:

```bash
bundle install
bundle exec jekyll serve
```

Kunjungi `http://localhost:4000` untuk melihat situsmu.

## Domain Kustom

Tambahkan domain milikmu di `_config.yml`:

```yaml
url: 'https://yourdomain.com'
```

Lalu konfigurasikan domain tersebut pada penyedia hosting.

## Tips

- **Uji lokal terlebih dahulu**: Pastikan semuanya berjalan sebelum deploy
- **Periksa tautan**: Pastikan semua [[Wiki Links]] berfungsi
- **Optimalkan gambar**: Kompres gambar agar waktu muat lebih cepat
- **Gunakan HTTPS**: Sebagian besar penyedia hosting sudah menyediakannya otomatis

## Pemecahan Masalah

**Situs tidak memperbarui?**

- Periksa apakah perubahan sudah dipush ke repositori
- Pastikan proses build selesai tanpa error
- Hapus cache peramban

**Tautan rusak?**

- Pastikan seluruh judul catatan sama persis
- Pastikan catatan memiliki `feed: "show"` pada front matter
- Build ulang situs setelah menambahkan catatan baru

---

_Taman digitalmu siap dibagikan kepada dunia!_
