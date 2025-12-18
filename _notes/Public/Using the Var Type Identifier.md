---
title: Using the Var Type Identifier
aliases:
  - Using the Var Type Identifier
categories:
  - "[[Posts]]"
tags:
  - java
  - var
  - local-variable-type-inference
author:
  - "[[Aes Saputra]]"
url: https://aessaputra.net/notes/using-the-var-type-identifier
created: 2025-12-18
published: 2025-12-18
date: 2025-12-18
topics: []
status: "[[Published]]"
feed: show
---

## Kata Kunci Var

Mulai dari Java SE 10, Anda dapat menggunakan pengenal tipe `var` untuk mendeklarasikan variabel lokal. Dengan melakukan ini, Anda membiarkan kompilator memutuskan apa tipe sebenarnya dari variabel yang Anda buat. Setelah dibuat, tipe ini tidak dapat diubah.

Perhatikan contoh berikut:

```java
String message = "Hello world!";
Path path = Path.of("debug.log");
InputStream stream = Files.newInputStream(path);
```

Dalam kasus tersebut, harus mendeklarasikan tipe eksplisit dari ketiga variabel `message`, `path`, dan `stream` adalah hal yang redundan.

Dengan pengenal tipe `var`, kode sebelumnya dapat ditulis sebagai berikut:

```java
var message = "Hello world!";
var path = Path.of("debug.log");
var stream = Files.newInputStream(path);
```

## Contoh Penggunaan Var

Contoh berikut menunjukkan bagaimana Anda dapat menggunakan `var` untuk membuat kode Anda lebih sederhana untuk dibaca. Di sini variabel `list` diberi tipe `List<String>` dan variabel `element` bertipe `String`.

```java
var list = List.of("one", "two", "three", "four");
for (var element: list) {
    System.out.println(element);
}
```

Pada contoh ini, variabel `path` bertipe `Path`, dan variabel `stream` bertipe `InputStream`.

```java
var path = Path.of("debug.log");
try (var stream = Files.newInputStream(path)) {
    // memproses file
}
```

Perhatikan bahwa pada dua contoh sebelumnya, Anda telah menggunakan `var` untuk mendeklarasikan variabel dalam pernyataan `for` dan dalam pernyataan `try-with-resources`. Kedua pernyataan ini biasanya dibahas lebih lanjut dalam topik [[Control Flow]] dan [[Exception Handling]].

## Batasan Penggunaan Var

Terdapat batasan dalam penggunaan pengenal tipe `var`.

1.  Anda hanya dapat menggunakannya untuk **variabel lokal** yang dideklarasikan dalam method, konstruktor, dan blok inisialisasi.
2.  `var` **tidak dapat** digunakan untuk *fields*, maupun untuk parameter method atau konstruktor.
3.  Kompilator harus dapat memilih tipe ketika variabel dideklarasikan. Karena `null` tidak memiliki tipe, variabel harus memiliki inisialisasi (*initializer*).

Mengikuti batasan tersebut, kelas berikut **tidak dapat dikompilasi**, karena menggunakan `var` sebagai pengenal tipe tidak dimungkinkan untuk *field* atau parameter method.

```java
public class User  {
    private var name = "Sue"; // COMPILER ERROR

    public void setName(var name) { // COMPILER ERROR
        this.name = name;
    }
}
```

Hal yang sama berlaku untuk kode berikut. Dalam kasus ini, kompilator tidak dapat menebak tipe sebenarnya dari `greetings` karena tidak memiliki *initializer*. Jadi kode ini juga tidak dapat dikompilasi.

```java
public String greetings(int message) {
    var greetings; // COMPILER ERROR
    if (message == 0) {
        greetings = "morning";
    } else {
        greetings = "afternoon";
    }
    return "Good " + greetings;
}
```

## Referensi

*   [Using the Var Type Identifier - Dev.java](https://dev.java/learn/language-basics/using-var/)
*   Topik terkait: [[Creating Arrays in Your Programs]] untuk deklarasi variabel lainnya, [[Using Operators in Your Programs]] untuk operasi pada variabel.
