---
title: Wiki Links
feed: show
date: 2024-01-15
---

Wiki links memungkinkan kamu menghubungkan catatan dengan tanda kurung ganda seperti `[[Judul Catatan]]`. Fungsinya sama persis seperti menautkan catatan di Obsidian.

## Cara Menggunakan

Cukup ketik `[[Judul Catatan]]` di dalam catatan. Jika catatan dengan judul tersebut ada, ia akan menjadi tautan yang bisa diklik. Jika belum ada, kamu akan melihat placeholder yang menandakan catatan belum dibuat.

Kamu juga bisa menautkan situs eksternal: `[[Google::https://google.com]]`.

## Contoh

```markdown
Catatan ini terhubung ke [[Getting Started]] dan [[Markdown Guide]].

Untuk informasi lebih lanjut, kunjungi [[Jekyll::https://jekyllrb.com]].
```

## Backlink Otomatis

Saat kamu membuat Wiki Link ke catatan lain, catatan tersebut otomatis menampilkan bagian "Backlinks". Misalnya, ketika membuka [[Getting Started]], kamu akan melihat catatan ini tercantum di sana karena kita menautkannya.


## Pemecahan Masalah

Jika sebuah Wiki Link tampak rusak:
1. Periksa penulisan judul catatan dengan tepat
2. Pastikan catatan berada di folder `_notes`
3. Verifikasi catatan memiliki `feed: "show"` pada front matter

---

*Wiki links mengubah catatanmu dari dokumen terpisah menjadi basis pengetahuan yang saling terhubung.*
