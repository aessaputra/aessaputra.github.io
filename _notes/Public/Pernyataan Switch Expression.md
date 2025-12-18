---
title: Pernyataan Switch Expression - Papan Catur Strategi
aliases:
  - Switch Expression
  - Branching with Switch Expressions
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
topics: ["[[Java]]", "[[Programming Fundamentals]]", "[[Control Flow]]"]
status: "[[Published]]"
feed: show
---

## Pengantar: Papan Catur Strategi dalam Kode

Dalam evolusi [[Pemrograman Java]], `switch statement` tradisional telah menjadi alat yang andal untuk mengarahkan alur program. Namun, seiring berjalannya waktu, kebutuhan akan ekspresi yang lebih ringkas dan aman muncul. Di sinilah `switch expression` hadir, seperti "Papan Catur Strategi" yang baru dan lebih efisien. Ia memungkinkan kita untuk tidak hanya memilih jalur, tetapi juga menghasilkan nilai secara langsung, mengubah cara kita menyusun logika percabangan menjadi lebih elegan dan fungsional.

## Evolusi Strategi: Mengapa `switch expression`?

`switch expression`, yang diperkenalkan di Java SE 14, adalah sintaks yang lebih nyaman dan kuat dibandingkan `switch statement` tradisional. Motivasi di balik pengembangannya meliputi:

1.  **Mengatasi `fall-through`**: Perilaku `fall-through` default pada `switch statement` seringkali menjadi sumber bug. `switch expression` menghilangkan masalah ini dengan sintaks baru.
2.  **Blok yang lebih fleksibel**: `switch statement` memperlakukan seluruh blok sebagai satu kesatuan. `switch expression` memungkinkan definisi variabel lokal dalam setiap `case`.
3.  **Menghasilkan nilai**: `switch statement` adalah pernyataan (statement), yang berarti ia melakukan tindakan. `switch expression` adalah ekspresi (expression), yang berarti ia mengevaluasi menjadi sebuah nilai, menghasilkan kode yang lebih ringkas dan mudah dibaca.

`switch statement` tradisional masih tersedia dan semantiknya tidak berubah. `switch expression` adalah tambahan yang memberikan fleksibilitas lebih.

## Langkah-Langkah Strategis: Sintaks Baru `case L ->`

Sintaks `switch expression` memodifikasi cara label `switch` ditulis. Mari kita bandingkan dengan `switch statement` tradisional:

### `switch statement` Tradisional

```java
Day day = Day.MONDAY; // hari apa pun
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
System.out.println("len = " + len);
```

### `switch expression` (Java SE 14+)

```java
Day day = Day.MONDAY; // hari apa pun
int len =
    switch (day) {
        case MONDAY, FRIDAY, SUNDAY -> 6;
        case TUESDAY                -> 7;
        case THURSDAY, SATURDAY     -> 8;
        case WEDNESDAY              -> 9;
    };
System.out.println("len = " + len);
```

Sintaks label `switch` sekarang adalah `case L ->`. Hanya kode di sebelah kanan `->` yang dieksekusi jika label cocok. Kode ini bisa berupa ekspresi tunggal, blok kode, atau pernyataan `throw`. Karena setiap `case` adalah bloknya sendiri, Anda dapat mendefinisikan variabel lokal di dalamnya. Sintaks ini juga mendukung beberapa konstanta per `case`, dipisahkan dengan koma.

## Buah dari Strategi: Menghasilkan Nilai

Salah satu fitur paling kuat dari `switch expression` adalah kemampuannya untuk menghasilkan nilai. Ini berarti Anda dapat menetapkan hasil dari `switch expression` langsung ke sebuah variabel.

```java
int quarter = 0; // nilai apa pun

String quarterLabel =
    switch (quarter) {
        case 0  -> "Q1 - Winter";
        case 1  -> "Q2 - Spring";
        case 2  -> "Q3 - Summer";
        case 3  -> "Q3 - Summer";
        default -> "Unknown quarter";
    };
System.out.println("Label kuartal: " + quarterLabel);
```

Jika hanya ada satu pernyataan dalam blok `case`, nilai yang dihasilkan oleh pernyataan ini akan menjadi nilai yang dikembalikan oleh `switch expression`.

### Mengatasi Ambiguitas dengan `yield`

Ketika blok kode dalam `case` lebih kompleks, penggunaan `return` tradisional dapat menimbulkan ambiguitas. Untuk mengatasi ini, Java memperkenalkan pernyataan `yield`.

**Contoh Kode yang Tidak Kompilasi (untuk ilustrasi ambiguitas `return`):**
```java
{% raw %}
// Hati-hati, kode ini TIDAK akan kompilasi!
public String convertToLabel(int quarter) {
    String quarterLabel =
        switch (quarter) {
            case 0  -> {
                System.out.println("Q1 - Winter");
                return "Q1 - Winter"; // Ambiguitas: return method atau switch?
            }
            default -> "Unknown quarter";
        };
    return quarterLabel;
}
{% endraw %}
```

**Menggunakan `yield` untuk Kejelasan:**
```java
{% raw %}
public String convertToLabel(int quarter) {
    String quarterLabel =
        switch (quarter) {
            case 0  -> {
                System.out.println("Q1 - Winter");
                yield "Q1 - Winter"; // Jelas: menghasilkan nilai untuk switch expression
            }
            default -> "Unknown quarter";
        };
    return quarterLabel;
}
{% endraw %}
```

Pernyataan `yield` digunakan dalam blok `case` dari `switch expression` untuk secara eksplisit menyatakan nilai yang akan dihasilkan oleh `switch expression` tersebut.

## Strategi Pertahanan: Klausa `default` dan Exhaustiveness

Klausa `default` memungkinkan kode Anda menangani kasus di mana nilai pemilih tidak cocok dengan konstanta `case` mana pun. Dalam `switch expression`, semua `case` harus bersifat *exhaustive*, artinya untuk semua nilai yang mungkin, harus ada label `switch` yang cocok. `switch statement` tradisional tidak memiliki persyaratan ini.

Untuk `enum`, jika semua konstanta `enum` telah dicakup oleh `case`, klausa `default` tidak diperlukan. Namun, jika ada nilai `enum` baru ditambahkan dan `switch expression` tidak diperbarui, kompiler akan menambahkan klausa `default` secara otomatis yang akan melempar `IncompatibleClassChangeError` saat runtime, membantu mendeteksi potensi bug.

## Fleksibilitas Strategi: `case L:` dalam `switch expression`

`switch expression` juga dapat menggunakan blok `case` tradisional dengan sintaks `case L:`. Dalam kasus ini, perilaku `fall-through` masih berlaku, dan nilai dihasilkan menggunakan pernyataan `yield`.

```java
{% raw %}
String result = switch (someValue) {
    case 1: 
        System.out.println("Case 1");
        yield "One";
    case 2: 
        System.out.println("Case 2");
        yield "Two";
    default: 
        System.out.println("Default");
        yield "Other";
};
System.out.println(result);
{% endraw %}
```

## Ancaman Tersembunyi: Menangani Nilai `null`

Secara default, `switch statement` dan `switch expression` tidak menerima nilai pemilih `null`. Mencoba `switch` pada nilai `null` akan menghasilkan `NullPointerException`. Namun, Java SE 17 memperkenalkan fitur pratinjau yang memungkinkan `switch expression` untuk menangani nilai `null`, menunjukkan evolusi berkelanjutan dalam bahasa ini.

## Peta Strategi `switch expression`

Berikut adalah visualisasi bagaimana `switch expression` bekerja sebagai "Papan Catur Strategi" yang menghasilkan nilai:

```mermaid
graph TD
    A[Mulai Program] --> B{Variabel Pemilih};
    B --> C{Nilai Variabel Pemilih?};
    C -- Cocok dengan Case 1 --> D[Jalur Case 1 (-> Nilai 1)];
    C -- Cocok dengan Case 2 --> E[Jalur Case 2 (-> Nilai 2)];
    C -- Tidak Cocok --> F[Jalur Default (-> Nilai Default)];
    D --> G(Hasil: Nilai 1);
    E --> H(Hasil: Nilai 2);
    F --> I(Hasil: Nilai Default);
    G --> J[Lanjutkan Program dengan Hasil];
    H --> J;
    I --> J;
```
**Penjelasan Diagram:**
Diagram ini menggambarkan alur kerja `switch expression`. Program dimulai, dan "Variabel Pemilih" dievaluasi. Berdasarkan nilai tersebut, `switch expression` akan memilih salah satu "Jalur Case" yang sesuai. Setiap jalur ini secara langsung "menghasilkan" sebuah nilai. Jika tidak ada `case` yang cocok, "Jalur Default" akan menghasilkan nilai default. Akhirnya, program akan "Lanjutkan Program dengan Hasil" yang telah dihasilkan oleh `switch expression`.

## Refleksi: Master Catur Kode

`switch expression` adalah langkah maju yang signifikan dalam [[Pemrograman Java]], memberikan [[Pengembang Perangkat Lunak|developer]] kemampuan untuk menulis kode yang lebih ringkas, aman, dan ekspresif. Ini seperti seorang master catur yang tidak hanya merencanakan gerakan, tetapi juga memprediksi hasil dari setiap langkah dengan presisi. Dengan menguasai "Papan Catur Strategi" ini, kita dapat membangun [[Aplikasi]] yang lebih kuat dan mudah dipelihara, di mana setiap keputusan percabangan tidak hanya mengarahkan alur, tetapi juga secara aktif berkontribusi pada nilai yang dihasilkan oleh program.
