---
title: Creating Variables and Naming Them
aliases:
  - Creating Variables and Naming Them
categories:
  - "[[Posts]]"
tags:
  - programming-language
  - java
  - variables
  - naming
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

Dalam bahasa pemrograman Java, objek menyimpan statusnya di dalam **field**. Seringkali istilah "field" dan "variable" digunakan secara bergantian, yang dapat membingungkan pengembang baru. Artikel ini menjelaskan perbedaan teknis antara jenis-jenis variabel yang ada di Java serta aturan penamaannya.

Pemahaman tentang variabel sangat fundamental sebelum mempelajari pengelolaan memori di [[JVM]] atau struktur data kompleks di [[Java Collections]].

## Jenis-Jenis Variabel

Bahasa pemrograman Java mendefinisikan kategori variabel sebagai berikut:

### 1. Instance Variables (Non-Static Fields)
Secara teknis, objek menyimpan status individualnya dalam "non-static fields". Variabel ini dideklarasikan tanpa kata kunci `static`.
*   **Karakteristik**: Nilainya unik untuk setiap *instance* dari kelas (setiap objek).
*   **Konteks**: Berkaitan erat dengan konsep enkapsulasi dalam [[Object-Oriented Programming|OOP]].

```java
class Bicycle {
    int cadence = 0;   // instance variable
    int speed = 0;     // instance variable
    int gear = 1;      // instance variable
}
```

### 2. Class Variables (Static Fields)
Variabel kelas adalah field yang dideklarasikan dengan modifier `static`.
*   **Karakteristik**: Hanya ada satu salinan variabel ini yang eksis, terlepas dari berapa banyak objek yang dibuat dari kelas tersebut.
*   **Penggunaan**: Kata kunci `final` sering ditambahkan untuk mendefinisikan konstanta.

```java
class Bicycle {
    static int numGears = 6;    // class variable
}
```

### 3. Local Variables
Metode sering kali menyimpan status sementaranya dalam variabel lokal.
*   **Deklarasi**: Terletak di antara kurung kurawal pembuka dan penutup dari sebuah metode.
*   **Lingkup (Scope)**: Hanya terlihat oleh metode tempat mereka dideklarasikan; tidak dapat diakses dari bagian lain kelas.
*   **Inisialisasi**: Tidak memiliki nilai default; harus diinisialisasi sebelum digunakan.

```java
void bake() {
    int count = 0; // local variable
    count = count + 1;
}
```

### 4. Parameters
Parameter adalah variabel yang digunakan dalam deklarasi metode, konstruktor, atau penanganan pengecualian (*exception handler*).
*   **Penting**: Parameter selalu diklasifikasikan sebagai "variabel", bukan "field".

```java
public static void main(String[] args) { // args adalah parameter
    // ...
}
```

## Penamaan Variabel

Setiap bahasa pemrograman memiliki aturan dan konvensi penamaan. Di Java, hal ini sangat penting untuk keterbacaan kode.

### Aturan (Rules)
Aturan ini bersifat wajib; jika dilanggar, kode akan gagal dikompilasi.
1.  **Case-sensitive**: Nama variabel membedakan huruf besar dan kecil (`speed` berbeda dengan `Speed`).
2.  **Karakter Legal**: Boleh terdiri dari huruf Unicode, angka, simbol dolar (`$`), atau garis bawah (`_`).
3.  **Karakter Awal**: Harus dimulai dengan huruf, `$`, atau `_` (tidak boleh dimulai dengan angka).
4.  **Spasi**: Tidak boleh mengandung spasi (*white space*).

### Konvensi (Conventions)
Konvensi ini tidak dipaksakan oleh *compiler*, namun diikuti oleh komunitas pengembang Java untuk standar kualitas kode.
1.  **Karakter Awal**: Selalu mulai dengan huruf. Hindari penggunaan `$` dan `_` di awal nama, meskipun secara teknis legal.
2.  **Nama Lengkap**: Gunakan kata penuh alih-alih singkatan kriptik (misalnya, `cadence` lebih baik daripada `c`). Ini membuat kode bersifat *self-documenting*.
3.  **Gaya Penulisan**:
    *   **Variabel**: Gunakan `camelCase` (misalnya: `currentSpeed`, `gearRatio`).
    *   **Konstanta**: Gunakan huruf kapital semua dengan pemisah garis bawah (misalnya: `NUM_GEARS`, `MAX_WIDTH`).

## Baca Juga
*   Untuk detail tentang tipe data yang dapat disimpan dalam variabel, lihat [[Creating Primitive Type Variables in Your Programs]].

## Referensi
*   [Creating Variables and Naming Them - Dev.java](https://dev.java/learn/language-basics/variables/) - Dokumentasi resmi mengenai variabel dan aturan penamaan di Java.
