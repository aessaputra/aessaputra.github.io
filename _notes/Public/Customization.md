---
title: Customization
feed: show
date: 2024-01-15
---

Kamu bisa melakukan customization pada situs Jekyll Garden dengan mengedit beberapa berkas penting.

## Pengaturan Dasar

Edit `_config.yml` untuk mengubah informasi situs:

```yaml
title: "My Digital Garden"
heading: "Your Name"
description: "A brief description of your site"
url: "https://yoursite.com"
```

## Menu Navigasi

Tambahkan atau ubah item menu navigasi:

```yaml
menu:
  - title: "Notes"
    url: "/notes"
  - title: "About"
    url: "/about"
  - title: "Blog"
    url: "/blog"
```

## Preferensi Tema

Atur fitur mana yang diaktifkan:

```yaml
preferences:
  homepage:
    enabled: true      # Show custom homepage
  search:
    enabled: true      # Enable search
  backlinks:
    enabled: true      # Show backlinks
```

## Warna dan Font

Ubah tampilan dengan mengedit `assets/css/style.css`:

```css
:root {
  --primary-color: #007acc;
  --text-color: #333;
  --background-color: #fff;
  --font-family: -apple-system, BlinkMacSystemFont, sans-serif;
}
```

## Mode Gelap

Tema sudah mendukung mode gelap otomatis. Pengguna dapat berganti antara tema terang dan gelap, dan preferensinya akan disimpan.

## Font Kustom

Tambahkan font kustom dengan mengimpornya di CSS:

```css
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;600&display=swap');

:root {
  --font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
}
```

## Perubahan Tata Letak

Untuk customization lanjutan, kamu bisa mengubah berkas di folder `_layouts/`. Namun tetap jaga agar sederhana—fokuslah pada konten ketimbang gaya yang rumit.

## Tips

- Mulai dari pengaturan dasar di `_config.yml`
- Uji perubahan secara lokal sebelum melakukan deploy
- Batasi customization agar performa tetap optimal
- Gunakan panduan [[Deployment]] saat siap memublikasikan

---

*Customization seharusnya mendukung kontenmu, bukan mengalihkan perhatian darinya.*
