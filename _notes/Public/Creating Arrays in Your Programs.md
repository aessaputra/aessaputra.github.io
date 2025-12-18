---
title: Creating Arrays in Your Programs
aliases:
  - Java Arrays
  - Creating Arrays in Your Programs
categories:
  - "[[Posts]]"
tags:
  - programming-language
  - java
  - arrays
author:
  - "[[Aes Saputra]]"
url: https://aessaputra.net/notes/creating-arrays-in-your-programs
created: 2025-12-18
published: 2025-12-18
date: 2025-12-18
topics: []
status: "[[Published]]"
feed: show
---

## Pengantar

Dalam [[Java]], *array* adalah objek kontainer yang menampung sejumlah nilai tetap dari satu tipe tunggal. Panjang array ditetapkan ketika array tersebut dibuat. Setelah pembuatan, panjangnya menjadi tetap (*fixed*).

Setiap item dalam array disebut *elemen*, dan setiap elemen diakses melalui *indeks* numeriknya. Penomoran dimulai dari 0. Sebagai contoh, elemen ke-9 akan diakses pada indeks 8.

## Mendeklarasikan Variabel yang Merujuk ke Array

Program berikut mendeklarasikan array (bernama `anArray`) dengan baris kode berikut:

```java
// mendeklarasikan array integer
int[] anArray;
```

Seperti deklarasi variabel tipe lainnya, deklarasi array memiliki dua komponen: tipe array dan nama array. Tipe array ditulis sebagai `type[]`, di mana `type` adalah tipe data dari elemen yang dikandungnya; tanda kurung siku `[]` adalah simbol khusus yang menunjukkan bahwa variabel ini memegang array. Ukuran array bukan bagian dari tipenya (itulah sebabnya kurung sikunya kosong).

Nama array bisa apa saja, asalkan mengikuti aturan dan konvensi penamaan variabel. Seperti variabel tipe lainnya, deklarasi ini tidak benar-benar membuat array; ini hanya memberitahu kompilator bahwa variabel ini akan memegang array dari tipe yang ditentukan.

Anda juga dapat mendeklarasikan array dari tipe lain:

```java
byte[] anArrayOfBytes;
short[] anArrayOfShorts;
long[] anArrayOfLongs;
float[] anArrayOfFloats;
double[] anArrayOfDoubles;
boolean[] anArrayOfBooleans;
char[] anArrayOfChars;
String[] anArrayOfStrings;
```

Anda juga dapat menempatkan kurung siku setelah nama array:

```java
// bentuk ini tidak disarankan
float anArrayOfFloats[];
```

Namun, konvensi tidak menyarankan bentuk ini; kurung siku mengidentifikasi tipe array dan sebaiknya muncul bersama dengan penunjuk tipe.

## Membuat, Menginisialisasi, dan Mengakses Array

Salah satu cara untuk membuat array adalah dengan operator `new`. Pernyataan berikut mengalokasikan array dengan memori yang cukup untuk 10 elemen integer dan menetapkan array tersebut ke variabel `anArray`.

```java
// membuat array integer
anArray = new int[10];
```

Jika pernyataan ini hilang, maka kompilator akan mencetak kesalahan dan kompilasi gagal.

Baris-baris berikutnya memberikan nilai ke setiap elemen array:

```java
anArray[0] = 100; // inisialisasi elemen pertama
anArray[1] = 200; // inisialisasi elemen kedua
anArray[2] = 300; // dan seterusnya
```

Setiap elemen array diakses melalui indeks numeriknya:

```java
System.out.println("Element at index 0: " + anArray[0]);
```

## Contoh Program

Program berikut, `ArrayDemo`, membuat array integer, memasukkan beberapa nilai ke dalam array, dan mencetak setiap nilai ke output standar.

```java
class ArrayDemo {
    public static void main(String[] args) {
        // mendeklarasikan array integer
        int[] anArray;

        // mengalokasikan memori untuk 10 integer
        anArray = new int[10];

        // inisialisasi elemen pertama
        anArray[0] = 100;
        // inisialisasi elemen kedua
        anArray[1] = 200;
        // dan seterusnya
        anArray[2] = 300;
        anArray[3] = 400;
        anArray[4] = 500;
        anArray[5] = 600;
        anArray[6] = 700;
        anArray[7] = 800;
        anArray[8] = 900;
        anArray[9] = 1000;

        System.out.println("Element at index 0: "
                           + anArray[0]);
        System.out.println("Element at index 1: "
                           + anArray[1]);
        System.out.println("Element at index 2: "
                           + anArray[2]);
        System.out.println("Element at index 3: "
                           + anArray[3]);
        System.out.println("Element at index 4: "
                           + anArray[4]);
        System.out.println("Element at index 5: "
                           + anArray[5]);
        System.out.println("Element at index 6: "
                           + anArray[6]);
        System.out.println("Element at index 7: "
                           + anArray[7]);
        System.out.println("Element at index 8: "
                           + anArray[8]);
        System.out.println("Element at index 9: "
                           + anArray[9]);
    }
}
```

Output dari program ini adalah:

```shell
Element at index 0: 100
Element at index 1: 200
Element at index 2: 300
Element at index 3: 400
Element at index 4: 500
Element at index 5: 600
Element at index 6: 700
Element at index 7: 800
Element at index 8: 900
Element at index 9: 1000
```

Dalam situasi pemrograman dunia nyata, Anda mungkin akan menggunakan salah satu konstruksi perulangan yang didukung untuk melakukan iterasi melalui setiap elemen array, daripada menulis setiap baris secara individual seperti pada contoh sebelumnya. Anda dapat mempelajari tentang berbagai konstruksi perulangan (for, while, dan do-while) di bagian [[Control Flow]].

## Referensi

*   [Creating Arrays in Your Programs - Dev.java](https://dev.java/learn/language-basics/arrays/)
    *   *Catatan*: Situs sumber menyediakan latihan interaktif untuk "Practice Array Basics" dan "Practice Array Loops" yang dapat Anda coba langsung di browser.
*   Topik terkait: [[Tipe Data Primitif]] untuk jenis data yang disimpan, [[Loop For]] untuk iterasi, dan [[Var]] untuk inferensi tipe variabel lokal.
