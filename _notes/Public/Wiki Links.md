---
title: Wiki Links
feed: show
date: 2024-01-15
---
Wiki links memungkinkan kamu menghubungkan catatan dengan tanda kurung ganda seperti `[[Judul Catatan]]`. Fungsinya sama persis seperti menautkan catatan di Obsidian.

## Cara Menggunakan

Cukup ketik `[[Judul Catatan]]` di dalam catatan. Jika catatan dengan judul tersebut ada, ia akan menjadi tautan yang bisa diklik. Jika belum ada, kamu akan melihat placeholder yang menandakan catatan belum dibuat.

Kamu juga bisa menautkan situs eksternal: `[[Google::https://google.com]]`.

### Alias Tampilan

- Gunakan format `[[Nama Catatan|Teks Tampilan]]` untuk menampilkan label berbeda.
- Resolusi tautan akan mencari judul catatan dan daftar `aliases` pada front matter (case-insensitive).
- Jika label hanya ingin memanggil alias yang sudah didefinisikan, cukup tulis `[[Alias Catatan]]`; sistem otomatis mengarah ke catatan aslinya.

## Contoh

```markdown
Catatan ini terhubung ke [[Getting Started]] dan [[Markdown Guide]].

Untuk informasi lebih lanjut, kunjungi [[Jekyll::https://jekyllrb.com]].

Alias tampilan: [[InterPlanetary File System|IPFS]] menjelaskan teknologi.
```

## Backlink Otomatis

Saat kamu membuat Wiki Link ke catatan lain, catatan tersebut otomatis menampilkan bagian "Backlinks". Misalnya, ketika membuka [[Getting Started]], kamu akan melihat catatan ini tercantum di sana karena kita menautkannya.

## Best Practice: Gunakan Aliases

Jika judul catatan panjang, tambahkan `aliases` di front matter agar wikilink tetap sederhana:

```yaml
---
title: JSON - Bahasa Diplomatik Data
aliases:
  - JSON
  - json
feed: show
---
```

Dengan cara ini:
- `[[JSON]]` akan terhubung ke catatan "JSON - Bahasa Diplomatik Data"
- Backlinks akan terdeteksi dengan benar
- Lebih mudah menulis wikilink

## Pemecahan Masalah

Jika sebuah Wiki Link tampak rusak:
1. Periksa penulisan judul catatan dengan tepat
2. Pastikan catatan berada di folder `_notes`
3. Verifikasi catatan memiliki `feed: "show"` pada front matter
4. Untuk alias tampilan, pastikan bagian sebelum `|` adalah target catatan yang valid
5. Jika tampilan alias berubah menjadi tabel saat build, pastikan baris daftar tidak diawali spasi ganda; cukup tulis `- [[Target|Alias]] ...`

---

*Wiki links mengubah catatanmu dari dokumen terpisah menjadi basis pengetahuan yang saling terhubung.*
