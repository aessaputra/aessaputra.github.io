---
title: Ekspresi, Pernyataan, dan Blok
aliases:
  - Java Code Structure
  - Expressions, Statements and Blocks
categories:
  - "[[Posts]]"
tags:
  - Java
  - Programming
  - Fundamental
author:
  - "[[Aes Saputra]]"
url: https://aessaputra.github.io/notes/expresi-pernyataan-dan-block/
created: 2025-12-18
published: 2025-12-18
date: 2025-12-18
topics:
  - "[[Java]]"
  - "[[Programming Fundamentals]]"
status: "[[Published]]"
feed: show
---

Memahami struktur dasar kode Java sangat penting untuk menulis program yang efektif. Tiga komponen utama yang membentuk kerangka logika dalam bahasa pemrograman Java adalah [[Ekspresi|ekspresi]], [[Pernyataan|pernyataan]], dan [[Blok|blok]]. Artikel ini menjelaskan definisi, karakteristik, dan penggunaan masing-masing komponen tersebut berdasarkan panduan resmi dari [[Dev.java]].

## Ekspresi

**Ekspresi** adalah konstruksi yang terdiri dari [[Variabel|variabel]], [[Operator|operator]], dan pemanggilan metode yang disusun menurut sintaks bahasa pemrograman, yang kemudian dievaluasi menjadi **satu nilai tunggal**.

Anda mungkin sudah sering melihat contoh ekspresi, seperti:

```java
int cadence = 0;
anArray[0] = 100;
System.out.println("Element 1 at index 0: " + anArray[0]);

int result = 1 + 2;
if (value1 == value2) 
    System.out.println("value1 == value2");
```

### Nilai Balikan (Return Value)

Tipe data dari nilai yang dikembalikan oleh ekspresi bergantung pada elemen yang digunakan dalam ekspresi tersebut.
*   Ekspresi `cadence = 0` mengembalikan nilai `int` karena operator penugasan mengembalikan nilai yang ditugaskan.
*   Ekspresi `value1 == value2` mengembalikan nilai `boolean` (`true` atau `false`).
*   Metode yang mengembalikan `void` tidak menghasilkan nilai dan tidak dapat digunakan sebagai bagian dari ekspresi yang membutuhkan nilai.

### Ekspresi Majemuk (Compound Expressions)

Bahasa pemrograman Java memungkinkan Anda untuk menyusun ekspresi majemuk dari berbagai ekspresi yang lebih kecil selama tipe data yang dibutuhkan oleh satu bagian ekspresi sesuai dengan tipe data yang dihasilkan oleh bagian lainnya.

Contoh ekspresi majemuk:
```java
1 * 2 * 3
```

Dalam contoh di atas, urutan evaluasi tidak menjadi masalah karena hasil perkalian tidak bergantung pada urutan. Namun, perhatikan ekspresi berikut:

```java
x + y / 100
// Apakah ambigu?
```

Ekspresi ini tidak ambigu karena aturan **preseden operator** (operator precedence). Operator pembagian (`/`) memiliki preseden lebih tinggi daripada operator penjumlahan (`+`). Oleh karena itu, `y / 100` dievaluasi terlebih dahulu, dan hasilnya kemudian ditambahkan ke `x`.

Untuk kejelasan dan menghindari kesalahan logika, disarankan menggunakan tanda kurung:
```java
(x + y) / 100 
// Tidak ambigu, penjumlahan dilakukan sebelum pembagian
```

## Pernyataan

Jika ekspresi diibaratkan sebagai frasa, maka **Pernyataan** (statement) adalah kalimat lengkap dalam bahasa pemrograman. Sebuah pernyataan membentuk unit eksekusi yang lengkap.

Pernyataan diakhiri dengan titik koma (`;`).

### Jenis-Jenis Pernyataan

1.  **Pernyataan Ekspresi (Expression Statements)**
    Tidak semua ekspresi dapat menjadi pernyataan. Berikut adalah jenis ekspresi yang dapat dijadikan pernyataan dengan menambahkan titik koma:
    *   Ekspresi penugasan (assignment).
    *   Penggunaan `++` atau `--` (pre-increment/decrement).
    *   Pemanggilan metode.
    *   Ekspresi pembuatan objek.

    Contoh:
    ```java
    // Pernyataan penugasan
    aValue = 8933.234;
    // Pernyataan increment
    aValue++;
    // Pernyataan pemanggilan metode
    System.out.println("Hello World!");
    // Pernyataan pembuatan objek
    Bicycle myBike = new Bicycle();
    ```

2.  **Pernyataan Deklarasi (Declaration Statements)**
    Pernyataan ini digunakan untuk mendeklarasikan variabel.
    ```java
    // Pernyataan deklarasi
    double aValue = 8933.234;
    ```

3.  **Pernyataan Kontrol Alur (Control Flow Statements)**
    Pernyataan ini mengatur urutan eksekusi program, seperti [[Pernyataan If-Else|if-else]], loops, dan lainnya.

## Blok

**Blok** adalah kelompok yang terdiri dari nol atau lebih pernyataan yang diapit oleh kurung kurawal seimbang (`{` dan `}`). Blok dapat digunakan di mana saja satu pernyataan tunggal diizinkan.

### Contoh Blok

Berikut adalah contoh penggunaan blok dalam pernyataan `if-else`:

```java
class BlockDemo {
     public static void main(String[] args) {
          boolean condition = true;
          if (condition) { // Awal blok 1
               System.out.println("Condition is true.");
          } // Akhir blok 1
          else { // Awal blok 2
               System.out.println("Condition is false.");
          } // Akhir blok 2
     }
}
```

Dalam contoh di atas, blok mendefinisikan cakupan (scope) eksekusi untuk kondisi `if` dan `else`. Memahami blok sangat penting untuk pengelolaan variabel dan alur logika yang kompleks.

## Referensi

*   [Expressions, Statements, and Blocks - Dev.java](https://dev.java/learn/language-basics/expressions-statements-blocks/)
*   [The Java™ Language Specification](https://docs.oracle.com/javase/specs/)
