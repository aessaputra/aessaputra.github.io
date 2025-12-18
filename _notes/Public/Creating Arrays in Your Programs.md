---
title: Creating Arrays in Your Programs - Rak Perpustakaan
aliases:
  - Java Arrays
  - Creating Arrays in Your Programs
categories:
  - "[[Posts]]"
tags:
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

## Pengantar: Rak Perpustakaan
Di [[Java]], sebuah *array* bisa dibayangkan seperti **rak perpustakaan** yang punya jumlah kompartemen (slot) tetap. Begitu rak itu dibuat, jumlah slotnya tidak bisa ditambah atau dikurangi—kita hanya bisa menaruh dan mengambil buku di slot yang sudah ada. Cara berpikir ini membantu mengingat dua sifat kunci: **tipe tunggal** (semua buku sejenis) dan **panjang tetap** (jumlah slot sudah dipatok sejak awal).

## Peta Konsep: Jalur Buku dari Deklarasi ke Akses
```mermaid
graph TD
  A[Deklarasi variabel array\ncontoh: int[] anArray;] --> B[Alokasi memori\ncontoh: anArray = new int[10];]
  B --> C[Inisialisasi elemen\ncontoh: anArray[0] = 100;]
  C --> D[Akses dengan indeks\ncontoh: anArray[5] untuk elemen ke-6]
  D --> E[Iterasi\nfor / while / do-while]
```
- Diagram ini menggambarkan “alur rak”: mulai dari menyebut raknya (deklarasi), membeli raknya (alokasi), menaruh buku (inisialisasi), mengambil buku (akses), lalu berjalan menyusuri slot (iterasi).
- Cara membaca: ikuti panah dari kiri/atas ke kanan/bawah; setiap simpul adalah tahap yang biasanya terjadi saat kita memakai array dalam program.

## Arrays: Slot, Elemen, dan Indeks
### Definisi Rak
- Array adalah *container object* yang menyimpan **jumlah nilai tetap** dari **satu tipe**; panjangnya ditentukan saat dibuat dan setelah itu **tidak berubah**.
- Setiap nilai di dalam array disebut **element**.

### Indeks: Nomor Slot
- Elemen diakses lewat **index** numerik yang dimulai dari `0`.
- Konsekuensi “mulai dari nol”: elemen ke-6 berada di indeks `5`.
- Pengingat graf: indeks adalah “label slot” pada rak; salah label berarti salah ambil buku.

## Deklarasi & Alokasi: Menyebut Rak vs Membeli Rak
### Deklarasi (Variabel Mengarah ke Rak)
- Bentuk umum: `type[] name;` misalnya `int[] anArray;`.
- Deklarasi hanya menyatakan “akan ada rak”, belum ada rak fisik di memori.
- Ukuran array **bukan** bagian dari tipe; itulah mengapa ditulis `type[]` (tanpa angka) dan panjang ditentukan saat alokasi.

### Alokasi (Membuat Rak dengan Jumlah Slot)
- Membuat array memakai `new`, misalnya `anArray = new int[10];`.
- Jika alokasi tidak dilakukan, kompilasi bisa gagal karena variabel array “belum diinisialisasi”.

## Inisialisasi & Akses: Menaruh dan Mengambil Buku
### Mengisi Slot
- Pengisian elemen dilakukan dengan indeks: `anArray[0] = 100;`, `anArray[1] = 200;`, dan seterusnya.

### Mengambil Slot
- Membaca elemen juga lewat indeks: `anArray[0]`, `anArray[9]`, dan seterusnya.
- Di dunia nyata, pengambilan biasanya dibungkus [[Control Flow]] lewat [[Loop For|perulangan for]] atau `while`, bukan ditulis satu per satu.

## Contoh Utama: ArrayDemo sebagai Rak yang Diisi Berurutan
### Program
```java
class ArrayDemo {
    public static void main(String[] args) {
        // declares an array of integers
        int[] anArray;

        // allocates memory for 10 integers
        anArray = new int[10];

        // initialize first element
        anArray[0] = 100;
        // initialize second element
        anArray[1] = 200;
        // and so forth
        anArray[2] = 300;
        anArray[3] = 400;
        anArray[4] = 500;
        anArray[5] = 600;
        anArray[6] = 700;
        anArray[7] = 800;
        anArray[8] = 900;
        anArray[9] = 1000;

        IO.println("Element at index 0: "
                           + anArray[0]);
        IO.println("Element at index 1: "
                           + anArray[1]);
        IO.println("Element at index 2: "
                           + anArray[2]);
        IO.println("Element at index 3: "
                           + anArray[3]);
        IO.println("Element at index 4: "
                           + anArray[4]);
        IO.println("Element at index 5: "
                           + anArray[5]);
        IO.println("Element at index 6: "
                           + anArray[6]);
        IO.println("Element at index 7: "
                           + anArray[7]);
        IO.println("Element at index 8: "
                           + anArray[8]);
        IO.println("Element at index 9: "
                           + anArray[9]);
    }
}
```

### Output
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

### Catatan Implementasi
- `IO.println` adalah utilitas pada playground/lingkungan contoh; pada program Java “biasa”, pola yang umum adalah `System.out.println(...)`.
- Contoh ini sengaja “berisik” (print satu per satu) untuk menonjolkan sintaks array; dalam praktik, gunakan loop dari [[Control Flow]].

## Ragam Tipe Array: Banyak Rak, Satu Jenis Buku per Rak
### Contoh Deklarasi untuk Berbagai Tipe
- `byte[] anArrayOfBytes;`
- `short[] anArrayOfShorts;`
- `long[] anArrayOfLongs;`
- `float[] anArrayOfFloats;`
- `double[] anArrayOfDoubles;`
- `boolean[] anArrayOfBooleans;`
- `char[] anArrayOfChars;`
- `String[] anArrayOfStrings;`

### Konvensi Penulisan
- Bentuk yang disarankan: `float[] anArrayOfFloats;` (kurung siku melekat pada tipe).
- Bentuk alternatif yang tidak direkomendasikan: `float anArrayOfFloats[];`.

## Trade-off: Rak Tetap vs Wadah yang Bisa Mengembang
| Kebutuhan | Array (rak slot tetap) | List/Collection (wadah elastis) |
|---|---|---|
| Panjang data | Tetap sejak dibuat | Dapat berubah (tambah/kurang) |
| Akses elemen | Cepat via indeks `O(1)` | Umumnya cepat juga, tapi tergantung implementasi |
| Keterbacaan intent | Menekankan “ukuran pasti” | Menekankan “ukuran dinamis” |
| Risiko kesalahan | Mudah salah indeks (off-by-one) | Risiko tetap ada, tapi operasi tambah/hapus lebih idiomatis |

## Refleksi: Menata Rak agar Mudah Ditemukan
Di ujungnya, array mengajarkan disiplin seperti pustakawan: sebelum menata buku, tentukan dulu ukuran raknya. Jika rak slot tetap ini terasa membatasi, catatan ini bisa ditautkan ke [[Control Flow]] untuk teknik iterasi yang rapi, ke [[Tipe Data Primitif]] untuk memahami jenis “buku” yang boleh masuk, dan ke [[Var|var]] sebagai tetangga materi berikutnya dalam seri.

## Sumber
### Referensi Utama
- https://dev.java/learn/language-basics/arrays/
