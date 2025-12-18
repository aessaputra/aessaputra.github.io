---
title: Creating Primitive Type Variables in Your Programs
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

## Pengantar

Bahasa pemrograman Java bersifat *statically-typed*, yang berarti semua variabel harus dideklarasikan terlebih dahulu sebelum dapat digunakan. Hal ini melibatkan penyebutan tipe variabel dan namanya.

```java
int gear = 1;
```

Mendeklarasikan variabel memberitahu program bahwa ada *field* bernama `gear`, memegang data numerik, dan memiliki nilai awal `1`. Tipe data variabel menentukan nilai yang mungkin dikandungnya, serta operasi yang dapat dilakukan padanya. Selain `int`, bahasa pemrograman Java mendukung tujuh tipe data primitif lainnya. Tipe primitif didefinisikan oleh bahasa dan dinamai dengan kata kunci yang dipesan (*reserved keyword*).

Untuk pemahaman lebih lanjut tentang variabel, lihat [[Creating Variables and Naming Them]].

## Tipe Data Primitif

Java mendukung delapan tipe data primitif:

### 1. byte
*   **Spesifikasi**: Integer 8-bit *signed two's complement*.
*   **Rentang**: -128 hingga 127 (inklusif).
*   **Kegunaan**: Berguna untuk menghemat memori dalam array besar di mana penghematan memori benar-benar penting. Batasannya juga dapat berfungsi sebagai dokumentasi kode.

### 2. short
*   **Spesifikasi**: Integer 16-bit *signed two's complement*.
*   **Rentang**: -32,768 hingga 32,767 (inklusif).
*   **Kegunaan**: Sama seperti `byte`, digunakan untuk menghemat memori pada array besar.

### 3. int
*   **Spesifikasi**: Integer 32-bit *signed two's complement*.
*   **Rentang**: -2^31 hingga 2^31-1.
*   **Kegunaan**: Tipe data default untuk nilai integral.

### 4. long
*   **Spesifikasi**: Integer 64-bit *two's complement*.
*   **Rentang**: -2^63 hingga 2^63-1.
*   **Kegunaan**: Digunakan ketika rentang nilai `int` tidak cukup luas.

### 5. float
*   **Spesifikasi**: *Single-precision* 32-bit IEEE 754 floating point.
*   **Kegunaan**: Menghemat memori dalam array besar angka *floating point*.
*   **Peringatan**: Jangan gunakan untuk nilai presisi seperti mata uang. Gunakan `java.math.BigDecimal` sebagai gantinya.

### 6. double
*   **Spesifikasi**: *Double-precision* 64-bit IEEE 754 floating point.
*   **Kegunaan**: Pilihan default untuk nilai desimal.
*   **Peringatan**: Sama seperti `float`, jangan gunakan untuk mata uang.

### 7. boolean
*   **Nilai**: Hanya memiliki dua kemungkinan nilai: `true` dan `false`.
*   **Kegunaan**: Untuk *flag* sederhana yang melacak kondisi benar/salah. Ukurannya tidak didefinisikan secara presisi.

### 8. char
*   **Spesifikasi**: Karakter Unicode 16-bit tunggal.
*   **Rentang**: `\u0000` (atau 0) hingga `\uffff` (atau 65,535 inklusif).

## Dukungan Unsigned (Java SE 8+)

Mulai Java SE 8, Anda dapat menggunakan tipe data `int` untuk merepresentasikan *unsigned 32-bit integer* (0 hingga 2^32-1) dan `long` untuk *unsigned 64-bit integer* (0 hingga 2^64-1).

*   Gunakan kelas `Integer` dan `Long` untuk melakukan operasi aritmatika pada nilai *unsigned* ini, seperti `Integer.compareUnsigned()`, `Long.divideUnsigned()`, dll.

## String dan Array

Meskipun bukan tipe primitif, `java.lang.String` mendapatkan dukungan khusus dari bahasa. String adalah objek yang tidak dapat diubah (*immutable*).

```java
String s = "this is a string";
```

Array adalah objek kontainer yang memegang sejumlah nilai dengan tipe tunggal. Untuk struktur data yang lebih dinamis, Anda mungkin ingin mempelajari [[Java Collections]].

## Nilai Default

Tidak selalu perlu memberikan nilai saat variabel dideklarasikan. Field yang dideklarasikan tetapi tidak diinisialisasi akan diset ke nilai default yang wajar oleh kompilator.

| Tipe Data | Nilai Default (untuk Field) |
| :--- | :--- |
| byte | `0` |
| short | `0` |
| int | `0` |
| long | `0L` |
| float | `0.0f` |
| double | `0.0d` |
| char | `\u0000` |
| String (atau objek apapun) | `null` |
| boolean | `false` |

**Catatan Penting tentang Variabel Lokal**:
Nilai default di atas **tidak** berlaku untuk variabel lokal. Variabel lokal harus diinisialisasi sebelum digunakan. Mengakses variabel lokal yang belum diinisialisasi akan menyebabkan kesalahan waktu kompilasi (*compile-time error*).

## Literals

Literal adalah representasi kode sumber dari nilai tetap.

### Integer Literals
*   Defaultnya bertipe `int`.
*   Tambahkan akhiran `L` atau `l` untuk tipe `long`.
*   Sistem bilangan:
    *   Desimal: `10`
    *   Heksadesimal: `0x1a`
    *   Biner: `0b11010` (Java SE 7+)

### Floating-Point Literals
*   Defaultnya bertipe `double`.
*   Tambahkan akhiran `F` atau `f` untuk tipe `float`.
*   Tambahkan akhiran `D` atau `d` untuk tipe `double` (opsional).
*   Mendukung notasi ilmiah (E notation).

### Character dan String Literals
*   `char` menggunakan tanda kutip tunggal: `'a'`.
*   `String` menggunakan tanda kutip ganda: `"Hello"`.
*   Mendukung *escape sequences* seperti `\n` (baris baru), `\t` (tab), `\'`, `\"`, `\\`.

### Underscore pada Numeric Literals
Sejak Java SE 7, karakter garis bawah (`_`) dapat muncul di mana saja di antara digit dalam literal numerik untuk meningkatkan keterbacaan.

```java
long creditCardNumber = 1234_5678_9012_3456L;
long socialSecurityNumber = 999_99_9999L;
```

## Referensi
*   [Creating Primitive Type Variables in Your Programs - Dev.java](https://dev.java/learn/language-basics/primitive-types/) - Dokumentasi resmi mengenai tipe data primitif di Java.
*   Topik terkait: [[JVM]] untuk representasi memori, [[Object-Oriented Programming|OOP]] untuk konsep objek.
