---
title: Java Language Basics
aliases:
  - Java Language Basics
categories:
  - "[[Posts]]"
tags:
  - programming-language
  - learn
  - java
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

Artikel ini merangkum dasar-dasar bahasa pemrograman Java berdasarkan dokumentasi resmi **Dev.java**. Materi ini mencakup komponen fundamental yang membentuk struktur program Java, mulai dari variabel, operator, ekspresi, pernyataan, blok, hingga pernyataan alur kontrol.

Pemahaman yang kuat tentang konsep-konsep ini sangat penting sebelum melangkah ke topik yang lebih lanjut seperti [[Object-Oriented Programming|OOP]] atau pengelolaan memori oleh [[JVM]].

## 1. Variabel dan Tipe Data

Bagian ini menjelaskan bagaimana data disimpan, diberi nama, dan dikelola dalam memori program.

### Pembuatan dan Penamaan Variabel
Variabel adalah unit dasar penyimpanan dalam program Java. Agar kode dapat dikompilasi dan mudah dibaca, pengembang harus mematuhi aturan penamaan (*naming conventions*) yang ketat.
*   Panduan lengkap: [[Creating Variables and Naming Them]]

### Variabel Tipe Primitif
Java merupakan bahasa *strongly-typed* yang menyediakan sekumpulan tipe data primitif sebagai blok bangunan dasar. Tipe ini menyimpan nilai data sederhana secara langsung.
*   Sintaks dan inisialisasi: [[Creating Primitive Type Variables in Your Programs]]

### Array (Larik)
Array adalah objek kontainer yang menampung sejumlah nilai dengan tipe tunggal dalam ukuran yang tetap (*fixed-length*). Panjang array ditetapkan saat pembuatan dan tidak dapat diubah setelahnya.
*   Implementasi: [[Creating Arrays in Your Programs]]

### Identifiers Tipe Var
Diperkenalkan pada Java SE 10, kata kunci `var` memungkinkan deklarasi variabel lokal dengan inferensi tipe otomatis. Hal ini memungkinkan penulisan kode yang lebih ringkas tanpa mengorbankan keamanan tipe statis (*static type safety*).
*   Penggunaan `var`: [[Using the Var Type Identifier]]

## 2. Operator

Operator adalah simbol khusus yang melakukan operasi spesifik pada satu, dua, atau tiga operan, dan kemudian mengembalikan hasilnya.

*   **Penggunaan Operator**: Mencakup operator aritmatika, unari, penugasan, dan relasional untuk melakukan komputasi data. Lihat [[Using Operators in Your Programs]].
*   **Ringkasan Operator**: Daftar referensi lengkap mengenai semua operator yang tersedia beserta aturan presedensinya. Lihat [[Summary of Operators]].

## 3. Struktur Program: Ekspresi, Pernyataan, dan Blok

Kode Java tersusun dari tiga elemen struktural utama:

1.  **Ekspresi (*Expressions*)**: Konstruksi yang terdiri dari variabel, operator, dan pemanggilan metode yang dievaluasi menjadi sebuah nilai tunggal.
2.  **Pernyataan (*Statements*)**: Unit eksekusi terkecil dalam program yang menyatakan suatu tindakan (setara dengan kalimat dalam bahasa manusia).
3.  **Blok (*Blocks*)**: Sekumpulan nol atau lebih pernyataan yang dikelompokkan di dalam kurung kurawal `{ ... }`.

*   Pembahasan mendalam: [[Expressions, Statements and Blocks]]

## 4. Pernyataan Alur Kontrol (*Control Flow Statements*)

Secara default, pernyataan dalam program dieksekusi secara berurutan dari atas ke bawah. Pernyataan alur kontrol memutus aliran eksekusi tersebut, memungkinkan program untuk membuat keputusan, melakukan perulangan, dan percabangan kode.

### Jenis Alur Kontrol
Java mendukung berbagai mekanisme kontrol, termasuk:
*   **Decision-making**: `if`, `if-else`, `switch`.
*   **Looping**: `for`, `while`, `do-while`.
*   **Branching**: `break`, `continue`, `return`.

Pelajari detail implementasinya di: [[Control Flow Statements]].

### Percabangan dengan Switch
Pernyataan `switch` menyediakan cara yang efisien untuk mengalihkan alur eksekusi ke berbagai bagian kode berdasarkan nilai variabel.

1.  **Switch Statement**: Bentuk tradisional dari `switch` yang digunakan untuk mengontrol alur program secara imperatif.
    *   Panduan: [[Branching with Switch Statements]]
2.  **Switch Expressions**: Fitur modern yang memungkinkan `switch` digunakan sebagai ekspresi yang menghasilkan nilai, mendukung sintaks panah (`->`) yang lebih aman dan ringkas.
    *   Panduan: [[Branching with Switch Expressions]]

## Referensi

*   [Java Language Basics - Dev.java](https://dev.java/learn/language-basics/) - Dokumentasi dan tutorial resmi untuk dasar-dasar bahasa Java.
