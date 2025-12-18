---
title: Pernyataan Switch
aliases:
  - Branching with Switch Statements
  - Switch Statement
categories:
  - "[[Posts]]"
tags:
  - Java
  - Control Flow
  - Programming Fundamentals
author:
  - "[[Aes Saputra]]"
url: https://aessaputra.net/notes/pernyataan-switch/
created: 2025-12-18
published: 2025-12-18
date: 2025-12-18
topics:
  - "[[Java]]"
  - "[[Programming Fundamentals]]"
  - "[[Control Flow]]"
status: "[[Published]]"
feed: show
---

Pernyataan `switch` adalah salah satu dari lima pernyataan kontrol alur yang tersedia dalam bahasa Java. Artikel ini membahas penggunaan pernyataan `switch` secara mendalam berdasarkan panduan resmi dari [[Dev.java]].

## Menggunakan Pernyataan Switch untuk Mengontrol Alur

Pernyataan `switch` memungkinkan percabangan alur program ke sejumlah jalur eksekusi yang berbeda. Pernyataan ini mengambil variabel pemilih (*selector variable*) sebagai argumen dan menggunakan nilai variabel ini untuk memilih jalur yang akan dieksekusi.

### Tipe Data yang Didukung

Anda harus memilih tipe variabel pemilih dari salah satu tipe berikut:
*   Tipe data primitif: `byte`, `short`, `char`, dan `int`.
*   Tipe *wrapper*: `Character`, `Byte`, `Short`, dan `Integer`.
*   Tipe enumerasi (*enumerated types*).
*   Tipe `String`.

**Catatan Penting**: Tipe primitif berikut **tidak dapat** digunakan sebagai variabel pemilih: `boolean`, `long`, `float`, dan `double`.

### Contoh Dasar: Menentukan Kuartal

Berikut adalah contoh sederhana penggunaan pernyataan `switch` untuk menentukan label kuartal berdasarkan nilai integer:

```java
int quarter = 2; // Contoh nilai
String quarterLabel = null;

switch (quarter) {
    case 0: quarterLabel = "Q1 - Winter"; 
            break;
    case 1: quarterLabel = "Q2 - Spring"; 
            break;
    case 2: quarterLabel = "Q3 - Summer"; 
            break;
    case 3: quarterLabel = "Q3 - Summer"; 
            break;
    default: quarterLabel = "Unknown quarter";
};
System.out.println(quarterLabel);
```

Bagian tubuh dari pernyataan `switch` dikenal sebagai **blok switch**. Pernyataan dalam blok switch dapat diberi label dengan satu atau lebih label `case` atau `default`. Pernyataan `switch` mengevaluasi ekspresinya, kemudian mengeksekusi semua pernyataan yang mengikuti label `case` yang cocok.

## Kata Kunci `break` dan Perilaku "Fall Through"

Setiap pernyataan `break` mengakhiri pernyataan `switch` yang melingkupinya. Tanpa pernyataan `break`, pernyataan dalam blok switch akan mengalami **fall through** (jatuh ke bawah): semua pernyataan setelah label `case` yang cocok akan dieksekusi secara berurutan, terlepas dari label `case` berikutnya, sampai pernyataan `break` ditemui.

### Contoh Fall Through

Kode berikut menggunakan perilaku *fall through* untuk mengisi daftar bulan-bulan di masa depan (`futureMonths`) berdasarkan bulan saat ini:

```java
int month = 8;
java.util.List<String> futureMonths = new java.util.ArrayList<>();

switch (month) {
    case 1:  futureMonths.add("January");
    case 2:  futureMonths.add("February");
    case 3:  futureMonths.add("March");
    case 4:  futureMonths.add("April");
    case 5:  futureMonths.add("May");
    case 6:  futureMonths.add("June");
    case 7:  futureMonths.add("July");
    case 8:  futureMonths.add("August");
    case 9:  futureMonths.add("September");
    case 10: futureMonths.add("October");
    case 11: futureMonths.add("November");
    case 12: futureMonths.add("December");
             break;
    default: break;
}
```

Secara teknis, `break` terakhir tidak diperlukan karena alur akan keluar dari pernyataan `switch`. Namun, penggunaan `break` sangat disarankan untuk mempermudah modifikasi kode dan mengurangi risiko kesalahan. Bagian `default` menangani semua nilai yang tidak ditangani secara eksplisit oleh salah satu bagian `case`.

## Menggunakan Label `case` Ganda

Sebuah pernyataan dapat memiliki beberapa label `case`. Contoh kode berikut menghitung jumlah hari dalam bulan tertentu, di mana beberapa bulan memiliki jumlah hari yang sama:

```java
int month = 2;
int year = 2021;
int numDays = 0;

switch (month) {
    case 1: case 3: case 5:   // January March May
    case 7: case 8: case 10:  // July August October
    case 12:
        numDays = 31;
        break;
    case 4: case 6:   // April June
    case 9: case 11:  // September November
        numDays = 30;
        break;
    case 2: // February
        if (((year % 4 == 0) && !(year % 100 == 0)) || (year % 400 == 0))
            numDays = 29;
        else
            numDays = 28;
        break;
    default:
        System.out.println("Invalid month.");
        break;
}
System.out.println("Number of Days = " + numDays);
```

## Memilih Antara Switch dan If-Then-Else

Keputusan untuk menggunakan pernyataan `switch` atau `if-then-else` didasarkan pada keterbacaan kode dan jenis ekspresi yang diuji.

*   **If-Then-Else**: Dapat menguji ekspresi berdasarkan rentang nilai atau kondisi yang kompleks.
*   **Switch**: Hanya menguji ekspresi berdasarkan satu nilai integer, enumerasi, atau objek String.

Contoh yang cocok untuk `switch`:
```java
if (month == 1) { ... } else if (month == 2) { ... } // Bisa diubah menjadi switch
```

Contoh yang **tidak bisa** menggunakan `switch` (karena tipe boolean atau kondisi rentang):
```java
int temperature = 85;
if (temperature < 0) {
    System.out.println("Water is ice");
} else if (temperature < 100){
    System.out.println("Water is liquid");
} else {
    System.out.println("Water is vapor");
}
```

## Menggunakan String dalam Switch

Sejak Java SE 7, Anda dapat menggunakan objek `String` dalam ekspresi pernyataan `switch`. Contoh berikut menampilkan nomor bulan berdasarkan nama bulan:

```java
String month = "August";
int monthNumber = -1;

switch (month.toLowerCase()) {
    case "january":
        monthNumber = 1;
        break;
    // ... case lainnya ...
    case "august":
        monthNumber = 8;
        break;
    // ... case lainnya ...
    default: 
        monthNumber = 0;
        break;
}
```

Pernyataan `switch` membandingkan ekspresi String menggunakan metode `String.equals`.

**Peringatan NullPointerException**: Pernyataan `switch` akan melempar `NullPointerException` jika ekspresi yang dievaluasi bernilai `null`. Selalu pastikan ekspresi tidak null sebelum digunakan dalam switch.

## Referensi

*   [Branching with Switch Statements - Dev.java](https://dev.java/learn/language-basics/switch-statement/)
*   Topik terkait: [[Pernyataan Kontrol Alur]], [[If-Else]], [[Enum]], [[Numbers and Strings]].
