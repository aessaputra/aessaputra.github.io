---
title: Switch Expression di Java
categories:
  - "[[Posts]]"
tags:
  - Java
  - Programming Fundamentals
  - Control Flow
author:
  - "[[Aes Saputra]]"
url: https://aessaputra.net/notes/pernyataan-switch-expression/
created: 2025-12-18
published: 2025-12-18
date: 2025-12-18
topics:
  - "[[Java]]"
  - "[[Programming Fundamentals]]"
  - "[[Control Flow]]"
status: "[[Published]]"
feed: show
aliases:
  - Switch Expression
  - Branching with Switch Expressions
contentType: concept
---

**Switch Expression** adalah fitur yang diperkenalkan secara resmi di [[Java]] SE 14 yang memperbarui cara kita menangani percabangan kode. Fitur ini menawarkan sintaks yang lebih ringkas, aman, dan fleksibel dibandingkan `switch statement` tradisional, serta memungkinkan blok `switch` untuk dievaluasi menjadi sebuah nilai secara langsung.

## Motivasi Perubahan

Sebelum adanya Switch Expression, pengembang [[Java]] sering menghadapi beberapa keterbatasan dengan `switch statement` klasik:

1.  **Perilaku *Fall-through***: Secara default, eksekusi kode akan "jatuh" ke `case` berikutnya jika tidak ada pernyataan `break`. Ini sering menjadi sumber *bug* yang sulit dideteksi.
2.  **Cakupan Variabel (*Scope*)**: Blok `switch` tradisional dianggap sebagai satu blok cakupan tunggal. Ini menyulitkan jika kita ingin mendefinisikan variabel lokal dengan nama yang sama di `case` yang berbeda.
3.  **Pernyataan vs Ekspresi**: `switch` tradisional adalah sebuah pernyataan (*statement*), yang berarti ia hanya melakukan aksi tetapi tidak menghasilkan nilai. Ini sering memaksa pengembang untuk mendeklarasikan variabel di luar blok `switch` dan mengisinya di dalam setiap `case`, yang kurang elegan dan rentan kesalahan.

## Sintaks Baru: `case L ->`

Switch Expression memperkenalkan sintaks label baru `case L ->`. Dengan sintaks ini, hanya kode di sebelah kanan tanda panah (`->`) yang akan dieksekusi jika label cocok. Tidak ada perilaku *fall-through*, sehingga kita tidak lagi memerlukan pernyataan `break`.

### Contoh Perbandingan

Berikut adalah perbandingan antara sintaks lama dan baru:

**Switch Statement Tradisional:**

```java
Day day = Day.MONDAY;
int len = 0;
switch (day) {
    case MONDAY:
    case FRIDAY:
    case SUNDAY:
        len = 6;
        break;
    case TUESDAY:
        len = 7;
        break;
    case THURSDAY:
    case SATURDAY:
        len = 8;
        break;
    case WEDNESDAY:
        len = 9;
        break;
}
```

**Switch Expression:**

```java
Day day = Day.MONDAY;
int len = switch (day) {
    case MONDAY, FRIDAY, SUNDAY -> 6;
    case TUESDAY                -> 7;
    case THURSDAY, SATURDAY     -> 8;
    case WEDNESDAY              -> 9;
};
```

Perhatikan bahwa kita dapat menggunakan beberapa konstanta dalam satu `case` dengan memisahkannya menggunakan koma, dan seluruh ekspresi `switch` dapat langsung ditugaskan ke variabel `len`.

## Menghasilkan Nilai dengan `yield`

Salah satu fitur utama Switch Expression adalah kemampuannya untuk mengembalikan nilai. Jika blok kode di sebelah kanan `->` adalah ekspresi tunggal, nilai ekspresi tersebut otomatis dikembalikan. Namun, jika kita memerlukan blok kode penuh (menggunakan kurung kurawal `{}`), kita harus menggunakan kata kunci `yield` untuk mengembalikan nilai.

### Mengapa `yield`, bukan `return`?

Penggunaan `return` di dalam blok `switch` dapat menimbulkan ambiguitas: apakah kita ingin mengembalikan nilai dari `switch` atau menghentikan eksekusi *method* pembungkusnya? Untuk mengatasi ini, [[Java]] memperkenalkan `yield`.

**Contoh Penggunaan `yield`:**

```java
int quarter = 0;
String quarterLabel = switch (quarter) {
    case 0 -> {
        System.out.println("Menghitung Q1...");
        yield "Q1 - Winter";
    }
    case 1 -> "Q2 - Spring"; // Ekspresi tunggal tidak butuh yield
    default -> "Unknown quarter";
};
```

Kata kunci `yield` berfungsi mirip dengan `return`, tetapi khusus untuk mengembalikan nilai dari dalam blok `switch expression`.

## Kelengkapan (*Exhaustiveness*)

Berbeda dengan `switch statement`, Switch Expression mewajibkan **kelengkapan** (*exhaustiveness*). Artinya, semua kemungkinan nilai dari variabel penentu harus ditangani.

*   Untuk tipe data primitif (seperti `int` atau `String`), kita biasanya wajib menyertakan klausa `default`.
*   Untuk tipe **[[Enum]]**, jika kita telah menangani semua konstanta enum yang ada, kita tidak perlu menambahkan `default`.

Jika di kemudian hari ada konstanta baru yang ditambahkan ke [[Enum]] dan kode `switch` tidak diperbarui, [[Compiler]] akan mendeteksi ketidaklengkapan ini (jika dikompilasi ulang) atau melempar kesalahan saat *runtime*, menjaga keamanan kode.

## Kesimpulan

Switch Expression di [[Java]] bukan hanya sekadar pemanis sintaks (*syntactic sugar*). Ia membawa perbaikan fundamental pada alur kontrol program dengan:
*   Menghilangkan risiko *fall-through*.
*   Memungkinkan penulisan kode fungsional yang lebih bersih dengan pengembalian nilai.
*   Menjamin keamanan tipe melalui pengecekan kelengkapan (*exhaustiveness*).

Dengan mengadopsi fitur ini, pengembang dapat menulis kode yang lebih ekspresif, ringkas, dan bebas dari *bug* umum yang terkait dengan percabangan.

---
**Referensi:**
*   [Branching with Switch Expressions - Dev.java](https://dev.java/learn/language-basics/switch-expression/)
