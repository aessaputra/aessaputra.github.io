---
title: Source Code
categories:
  - "[[Posts]]"
tags:
  - programming
  - definition
  - legal
  - history
author:
  - "[[Aes Saputra]]"
url: https://aessaputra.net/notes/source-code
created: "2025-12-18"
published: "2025-12-18"
date: "2025-12-18"
status: "[[Published]]"
contentType: concept
feed: show
aliases:
  - Kode Sumber
  - source code
  - kode sumber
---

**Source Code** (kode sumber) adalah sekumpulan instruksi dan pernyataan yang ditulis oleh programmer menggunakan bahasa pemrograman komputer yang dapat dibaca oleh manusia. Kode ini berfungsi sebagai "cetak biru" atau resep utama yang mendefinisikan bagaimana sebuah perangkat lunak bekerja, mulai dari logika sederhana hingga sistem yang kompleks.

Secara teknis, source code adalah bentuk awal dari program sebelum diterjemahkan menjadi bahasa yang dipahami mesin. Secara hukum, source code sering kali dilindungi sebagai kekayaan intelektual (intellectual property).

## Sejarah Singkat

Pada masa awal komputasi (akhir 1940-an), komputer diprogram langsung menggunakan [[Machine Code|bahasa mesin]] (biner). Metode ini sangat sulit, rentan kesalahan, dan tidak portabel antar mesin.

Untuk mengatasi masalah ini, dikembangkanlah bahasa pemrograman tingkat tinggi (high-level programming languages) seperti Fortran pada pertengahan 1950-an. Bahasa ini memungkinkan programmer menulis instruksi dalam format yang lebih abstrak dan mirip bahasa manusia, yang kemudian menjadi cikal bakal konsep *source code* modern.

## Karakteristik Utama

*   **Human-Readable**: Ditulis menggunakan teks alphanumerik dan simbol yang dapat dipahami oleh manusia, berbeda dengan [[Machine Code|kode mesin]] yang hanya berupa angka biner.
*   **Input Proses Kompilasi**: Merupakan bahan mentah yang harus diproses oleh [[Compilation|kompiler]] (untuk bahasa seperti C++ atau [[Java]]) atau dijalankan oleh interpreter (untuk bahasa seperti Python atau JavaScript).
*   **Dokumentasi Logika**: Sering kali menyertakan *comments* (komentar) yang tidak dieksekusi oleh komputer tetapi berfungsi untuk menjelaskan logika kode kepada programmer lain.

## Jenis-Jenis Source Code

### Berdasarkan Lisensi

1.  **Proprietary (Closed Source)**
    Kode sumber yang dimiliki secara eksklusif oleh individu atau perusahaan. Akses ke kode ini dibatasi dan dilindungi secara ketat sebagai rahasia dagang. Pengguna hanya menerima versi *executable* (hasil kompilasi) dan tidak diizinkan melihat atau memodifikasi kode aslinya.
    *   *Contoh*: Microsoft Windows, Adobe Photoshop.

2.  **[[Open Source]]**
    Kode sumber yang tersedia secara bebas untuk publik. Siapa pun dapat melihat, memodifikasi, dan mendistribusikan ulang kode tersebut sesuai dengan lisensi yang berlaku (misalnya GPL, MIT, Apache).
    *   *Contoh*: Linux Kernel, Android, [[Java]] (OpenJDK).

### Berdasarkan Eksekusi

1.  **Compiled Code**
    Source code yang harus diterjemahkan secara keseluruhan menjadi [[Machine Code|kode mesin]] atau [[Bytecode|bytecode]] sebelum dapat dijalankan.
    *   *Contoh*: C++, [[Java]], Go.

2.  **Interpreted Code**
    Source code yang diterjemahkan dan dijalankan baris demi baris oleh program interpreter secara langsung saat *runtime*.
    *   *Contoh*: Python, JavaScript, PHP.

## Aspek Hukum

Source code memiliki nilai ekonomi yang tinggi dan dilindungi oleh hukum kekayaan intelektual:

*   **Hak Cipta (Copyright)**: Melindungi ekspresi literal dari kode tersebut dari penyalinan tanpa izin.
*   **Rahasia Dagang (Trade Secret)**: Melindungi logika, algoritma, dan metode unik yang terkandung di dalam kode agar tidak diketahui oleh kompetitor, terutama pada *proprietary software*.

## Pentingnya dalam Pengembangan Software

Akses ke source code sangat krusial untuk:
*   **Maintenance**: Memperbaiki *bug* atau kesalahan dalam program.
*   **Customization**: Menyesuaikan perangkat lunak dengan kebutuhan spesifik pengguna.
*   **Audit Keamanan**: Memeriksa apakah terdapat celah keamanan (*vulnerabilities*) atau kode berbahaya (*malware*) yang tersembunyi.

## Contoh

Contoh source code sederhana dalam bahasa [[Java]] yang menampilkan pesan ke layar:

```java
public class HelloWorld {
    // Ini adalah komentar: method main adalah titik awal eksekusi
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

### Referensi

*   Wikipedia. (n.d.). *Source code*. Diambil dari [https://en.wikipedia.org/wiki/Source_code](https://en.wikipedia.org/wiki/Source_code)
*   SonarSource. (n.d.). *What is Source Code? Definition Guide & Example Types*. Diambil dari [https://www.sonarsource.com/resources/library/source-code/](https://www.sonarsource.com/resources/library/source-code/)
*   LSD.Law. (n.d.). *Definition of source code*. Diambil dari [https://lsd.law/define/source-code](https://lsd.law/define/source-code)
