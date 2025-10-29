---
title: Panduan Markdown
feed: show
date: 2024-01-15
---

Panduan ini menampilkan format Markdown penting yang dapat kamu gunakan dalam catatan.

## Judul

```markdown
# Judul Utama
## Judul Bagian
### Judul Subbagian
```

## Pemformatan Teks

```markdown
*Teks miring* atau _teks miring_
**Teks tebal** atau __teks tebal__
`kode inline`
~~coret~~
```

## Daftar

```markdown
- Item daftar tak berurut
- Item lainnya
  - Item bertingkat

1. Item daftar berurut
2. Item lainnya
```

## Tautan

```markdown
[Teks tautan](https://example.com)
[[Tautan Wiki ke catatan lain]]
[[Tautan eksternal::https://example.com]]
```

## Blok Kode

```markdown
```javascript
function halo() {
    console.log("Halo, Dunia!");
}
```
```

## Kutip Blok

```markdown
> Ini adalah kutipan blok.
> Dapat mencakup beberapa baris.
```

## Tabel

```markdown
| Header 1 | Header 2 |
|----------|----------|
| Konten   | Konten   |
```

## Matematika (jika diaktifkan)

```markdown
math inline: $x = y$
math blok: $$\int_{-\infty}^{\infty} e^{-x^2} dx = \sqrt{\pi}$$
```

## Gambar

```markdown
![Teks alternatif](/assets/img/image.jpg)
```

## Garis Horisontal

```markdown
---
```

## Tips

- Gunakan judul yang jelas dan deskriptif
- Buat paragraf singkat dan fokus
- Pakai [[Wiki Links]] untuk menghubungkan catatan terkait
- Jangan berlebihan dalam pemformatan — utamakan keterbacaan

---

*Ini mencakup fitur Markdown paling umum yang kamu perlukan untuk catatan.*
