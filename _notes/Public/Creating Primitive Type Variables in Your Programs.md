---
title: Creating Primitive Type Variables in Your Programs - Rak Bahan Kering
aliases:
  - Creating Primitive Type Variables in Your Programs
categories:
  - "[[Posts]]"
tags:
  - programming-language
  - java
  - primitive-types
author:
  - "[[Aes Saputra]]"
url:
created: 2025-12-18
published: 2025-12-18
date: 2025-12-18
topics: []
status: "[[Published]]"
feed: show
---

## Pengantar: Rak Bahan Kering
- Bayangkan tipe primitif sebagai bahan kering di rak dapur: ukurannya tetap, tidak saling memengaruhi, dan siap dipakai langsung untuk resep.
- Java adalah bahasa statically-typed: setiap wadah (variabel) harus dideklarasikan dengan tipe. Lihat [[Creating Variables and Naming Them]] untuk relasi antara field dan variabel.
- Untuk eksekusi dan default value level mesin, rujuk [[JVM]]. Untuk desain tipe dan enkapsulasi, lihat [[Object-Oriented Programming|OOP]]. Ikhtisar umumnya ada di [[Java Language Basics]].
- Break Point Analysis: tidak seperti bahan basah, tipe primitif tidak menyimpan state bersama; literal merepresentasikan nilai langsung tanpa objek.

```mermaid
graph TD
  A[Rak Bahan Kering] --> B[Primitive Types]
  B --> B1[byte]
  B --> B2[short]
  B --> B3[int]
  B --> B4[long]
  B --> B5[float]
  B --> B6[double]
  B --> B7[boolean]
  B --> B8[char]
  A --> C[Unsigned (Java 8+)]
  C --> C1[int (Integer)]
  C --> C2[long (Long)]
  A --> D[Default Values]
  A --> E[Literals]
```

- Diagram memperlihatkan hierarki: delapan tipe primitif sebagai bahan kering, dukungan unsigned di Java 8+, serta simpul untuk default values dan literals. Baca dari atas ke bawah untuk memahami cakupan dan keterkaitan.

## Jenis Bahan: Delapan Tipe Primitif
### byte (8-bit, two's complement)
- Rentang: -128 hingga 127 (inklusif).
- Gunaan: hemat memori pada array besar; memperjelas batas nilai.

### short (16-bit, two's complement)
- Rentang: -32,768 hingga 32,767.
- Gunaan: mirip `byte`, hemat memori untuk kumpulan besar.

### int (32-bit, two's complement)
- Rentang: -2^31 hingga 2^31-1.
- Gunaan: bilangan bulat umum; default untuk perhitungan integral.

### long (64-bit, two's complement)
- Rentang: -2^63 hingga 2^63-1.
- Gunaan: bilangan bulat lebar; gunakan saat `int` tidak cukup.

### float (32-bit, IEEE 754)
- Gunaan: angka pecahan, hemat memori pada array besar.
- Catatan: jangan untuk nilai presisi (mis. mata uang); gunakan `java.math.BigDecimal`.

### double (64-bit, IEEE 754)
- Gunaan: angka pecahan; pilihan default untuk desimal.
- Catatan: hindari untuk presisi finansial; gunakan `BigDecimal`.

### boolean
- Nilai: `true` atau `false`; ukuran tidak didefinisikan presisi.
- Gunaan: flags kondisi sederhana.

### char (16-bit Unicode)
- Rentang: `\u0000` hingga `\uffff` (0..65,535).
- Gunaan: karakter UTF-16 tunggal.

## Unsigned di Java 8+
### Unsigned int (32-bit)
- Rentang: 0 hingga 2^32-1.
- Dukungan: metode statis pada `Integer` seperti `compareUnsigned`.

### Unsigned long (64-bit)
- Rentang: 0 hingga 2^64-1.
- Dukungan: metode pada `Long` seperti `compareUnsigned`, `divideUnsigned`.

## Strings dan Arrays (bukan primitif)
### String
- `java.lang.String` mendapatkan dukungan khusus; objek immutable (nilainya tidak berubah setelah dibuat).
- Contoh literal: `"this is a string"`.

### Arrays
- Menyimpan kumpulan nilai bertipe sama; default value berlaku untuk field bertipe array dan elemennya sesuai tipe elemen.
- Untuk koleksi dinamis, lihat [[Java Collections]].

## Default Values (fields) dan Local Variables
### Default untuk fields
- `byte`: `0`
- `short`: `0`
- `int`: `0`
- `long`: `0L`
- `float`: `0.0f`
- `double`: `0.0d`
- `char`: `\u0000`
- `String`/objek: `null`
- `boolean`: `false`

### Local variables
- Tidak memiliki default value; wajib diinisialisasi sebelum digunakan.
- Akses variabel lokal yang belum diinisialisasi memicu compile-time error.

## Literals: Membuat Nilai
### Integer literals
- `int` default; akhiran `L`/`l` untuk `long` (gunakan `L` agar tidak mirip `1`).
- Basis: desimal (`10`), heksadesimal (`0x`), biner (`0b`, Java 7+).

### Floating-point literals
- `double` default; akhiran `F`/`f` untuk `float`, `D`/`d` opsional.
- Mendukung notasi ilmiah `E`/`e`.

### Character dan String literals
- Gunakan `'` untuk `char`, `"` untuk `String`; dukungan escape: `\b`, `\t`, `\n`, `\f`, `\r`, `\"`, `\'`, `\\`.
- Unicode escape dapat digunakan di berbagai konteks.

### null literal dan class literal
- `null` untuk reference types (bukan primitif); sering dipakai sebagai penanda ketiadaan objek.
- Class literal: `TypeName.class`, mis. `String.class` bertipe `Class`.

### Underscore pada numeric literals (Java 7+)
- Boleh di antara digit untuk keterbacaan (mis. `1_000_000`).
- Larangan: awal/akhir angka, bersebelahan dengan titik desimal, sebelum akhiran `F`/`L`, atau pada posisi yang mengharuskan deret digit utuh.

## Tabel Ringkas: Pemilihan Tipe

| Tipe | Lebar | Rentang Singkat | Default (field) | Gunaan Umum | Catatan |
|---|---|---|---|---|---|
| byte | 8-bit | -128..127 | 0 | Array besar | Dokumentasi batas |
| short | 16-bit | -32,768..32,767 | 0 | Array besar | Hemat memori |
| int | 32-bit | -2^31..2^31-1 | 0 | Bilangan bulat | Default integral |
| long | 64-bit | -2^63..2^63-1 | 0L | Bilangan lebar | Saat `int` tak cukup |
| float | 32-bit | IEEE 754 | 0.0f | Pecahan hemat memori | Bukan presisi finansial |
| double | 64-bit | IEEE 754 | 0.0d | Pecahan umum | Default desimal |
| boolean | — | true/false | false | Flag kondisi | Ukuran tak pasti |
| char | 16-bit | \u0000..\uffff | \u0000 | Karakter UTF-16 | Satu karakter |

## Refleksi: Rak yang Tertata
- Dengan metafora rak bahan kering, tiap tipe primitif diperlakukan sebagai bahan standar: ukurannya tetap, jelas batasnya, dan mudah dipilih untuk kebutuhan resep (program).
- Untuk desain menyeluruh, kembali ke [[Java Language Basics]] dan relasi dengan [[Creating Variables and Naming Them]]; untuk operasi tingkat mesin rujuk [[JVM]]; untuk penyimpanan koleksi, gunakan [[Java Collections]].
- Batas metafora: bahan kering di Java tidak berubah kualitas dan dapat direpresentasikan langsung sebagai literal; berbeda dengan dunia nyata yang penuh variasi.
