---
title: Effective Java
categories:
  - "[[Posts]]"
tags:
  - java
  - best-practices
  - programming
  - software-engineering
author:
  - "[[Aes Saputra]]"
url: https://aessaputra.net/notes/effective-java
created: "2025-12-18"
published: "2025-12-18"
date: "2025-12-18"
topics:
  - "[[Java]]"
  - "[[Software Architecture]]"
status: "[[Published]]"
feed: show
aliases:
  - effective java
---

**Effective Java** karya Joshua Bloch dianggap sebagai salah satu buku paling penting dalam literatur [[Java]]. Buku ini tidak hanya mengajarkan sintaksis, tetapi juga memberikan panduan tentang cara menggunakan bahasa Java secara efektif untuk menulis kode yang jelas, benar, kuat, dan mudah dipelihara.

Artikel ini merangkum praktik terbaik (best practices) utama dari buku **Effective Java (3rd Edition)**, yang mencakup pembaruan hingga Java 9.

## Membuat dan Menghancurkan Objek

Bagian ini berfokus pada siklus hidup objek, mulai dari penciptaan hingga pemusnahan.

### Pertimbangkan Static Factory Methods daripada Konstruktor
Alih-alih menyediakan konstruktor publik, pertimbangkan untuk menyediakan *static factory method*.
*   **Keuntungan**: Memiliki nama yang deskriptif, tidak perlu membuat objek baru setiap kali dipanggil (caching), dapat mengembalikan subtipe apa pun, dan dapat menyesuaikan kelas objek yang dikembalikan berdasarkan parameter input.
*   **Contoh**: `Boolean.valueOf(boolean)` lebih baik daripada `new Boolean(boolean)`.

### Gunakan Builder Pattern untuk Konstruktor dengan Banyak Parameter
Ketika menghadapi kelas dengan banyak parameter konstruktor (terutama yang opsional), gunakan [[Builder Pattern]].
*   Ini lebih mudah dibaca dan ditulis daripada *telescoping constructor* (konstruktor bertingkat) dan lebih aman daripada pola JavaBeans (yang memungkinkan inkonsistensi keadaan objek).

### Tegakkan Properti Singleton dengan Enum
Cara terbaik untuk mengimplementasikan [[Singleton]] di Java adalah dengan tipe `enum` satu elemen. Ini memberikan jaminan serialisasi secara gratis dan perlindungan terhadap serangan refleksi.
```java
public enum Elvis {
    INSTANCE;
    public void leaveTheBuilding() { ... }
}
```

### Hindari Membuat Objek yang Tidak Perlu
Gunakan kembali objek yang mahal untuk dibuat jika memungkinkan.
*   Contoh: Gunakan `String` literal alih-alih `new String("...")`.
*   Hati-hati dengan *autoboxing* yang dapat membuat objek [[Wrapper Class]] yang tidak perlu dalam loop.

### Hilangkan Referensi Objek yang Usang
Java memiliki [[Garbage Collection]], tetapi memori leak masih bisa terjadi (misalnya dalam implementasi Stack sendiri atau Cache). Pastikan untuk menghapus referensi (`null` out) objek yang tidak lagi digunakan jika kelas mengelola memorinya sendiri.

### Hindari Finalizers dan Cleaners
Finalizers tidak dapat diprediksi, seringkali berbahaya, dan umumnya tidak diperlukan. Cleaners (Java 9) kurang berbahaya tetapi masih lambat dan tidak dapat diprediksi. Gunakan antarmuka `AutoCloseable` dan `try-with-resources` sebagai gantinya.

### Prefer `try-with-resources` daripada `try-finally`
Untuk sumber daya yang harus ditutup (seperti `InputStream`, `java.sql.Connection`), selalu gunakan `try-with-resources`. Ini menghasilkan kode yang lebih pendek, lebih jelas, dan penanganan pengecualian yang lebih baik.

## Metode Umum untuk Semua Objek

Setiap objek mewarisi metode dari `java.lang.Object`. Mengoverridenya dengan benar sangat krusial.

*   **Patuhi kontrak saat mengoverride `equals`**: Pastikan implementasi memenuhi sifat refleksif, simetris, transitif, konsisten, dan non-null.
*   **Selalu override `hashCode` saat mengoverride `equals`**: Objek yang sama harus memiliki kode hash yang sama. Jika tidak, koleksi berbasis hash seperti `HashMap` dan `HashSet` tidak akan berfungsi dengan benar.
*   **Selalu override `toString`**: Berikan representasi string yang ringkas dan informatif untuk memudahkan debugging.
*   **Pertimbangkan mengimplementasikan `Comparable`**: Jika kelas memiliki urutan alami (seperti angka atau tanggal), implementasikan antarmuka ini untuk memungkinkan pengurutan dan pencarian yang mudah dalam koleksi.

## Kelas dan Antarmuka

### Minimalkan Aksesibilitas
Buat setiap kelas dan anggota kelas se-privat mungkin. Ini adalah inti dari enkapsulasi ([[Encapsulation]]) untuk memisahkan API dari implementasi.

### Dalam Kelas Publik, Gunakan Metode Aksesor Bukan Field Publik
Field publik pada kelas publik tidak menawarkan enkapsulasi. Gunakan *getter* dan *setter* (jika mutabel).

### Minimalkan Mutabilitas
Buat kelas menjadi *immutable* jika memungkinkan (seperti `String`, `BigInteger`). Kelas immutable lebih mudah dirancang, diimplementasikan, dan digunakan; mereka juga aman untuk thread ([[Thread Safety]]) secara inheren.
*   Jangan sediakan metode yang memodifikasi state objek.
*   Pastikan kelas tidak dapat diperluas (final).
*   Buat semua field `final` dan `private`.

### Lebih Pilih Komposisi daripada Pewarisan
[[Inheritance]] (pewarisan) melanggar enkapsulasi jika tidak dirancang dengan hati-hati. Komposisi (membungkus objek lain di dalam kelas Anda) memberikan fleksibilitas lebih dan menghindari masalah kerapuhan subkelas.

### Desain dan Dokumentasikan untuk Pewarisan atau Larang Sama Sekali
Jika kelas dirancang untuk diwarisi, dokumentasikan efek dari mengoverride metode. Jika tidak, buat kelas menjadi `final` atau jadikan konstruktor privat.

### Lebih Pilih Antarmuka daripada Kelas Abstrak
[[Interfaces]] memungkinkan definisi tipe yang fleksibel dan *multiple inheritance* dari tipe. Sejak Java 8, antarmuka dapat memiliki implementasi metode default (`default methods`).

## Generics

[[Generics]] menambahkan keamanan tipe (type safety) pada waktu kompilasi.

*   **Jangan gunakan Raw Types**: Selalu gunakan parameter tipe (misal `List<String>`, bukan `List`). Raw types mengorbankan keamanan tipe generik.
*   **Eliminasi peringatan unchecked**: Setiap peringatan unchecked mewakili potensi `ClassCastException` di runtime.
*   **Lebih pilih List daripada Array**: Array bersifat *covariant* dan *reified*, sedangkan generics bersifat *invariant* dan *erased*. List lebih aman secara tipe.
*   **Gunakan Bounded Wildcards untuk fleksibilitas API**: Gunakan `<? extends T>` untuk produsen dan `<? super T>` untuk konsumen (PECS - *Producer Extends, Consumer Super*).

## Enums dan Anotasi

*   **Gunakan Enums daripada Konstanta Int**: Enum memberikan keamanan tipe, namespace, dan fitur yang kaya.
*   **Gunakan Anotasi daripada Pola Penamaan**: Anotasi (seperti `@Test`) lebih aman dan fleksibel daripada mengandalkan nama metode tertentu.
*   **Konsisten menggunakan anotasi `@Override`**: Ini mencegah kesalahan ketik dan memastikan Anda benar-benar mengoverride metode superkelas.

## Lambdas dan Streams

Fitur fungsional yang diperkenalkan di Java 8.

*   **Lebih pilih Lambdas daripada Anonymous Classes**: Lambdas lebih ringkas dan mudah dibaca untuk instance antarmuka fungsional.
*   **Lebih pilih Method References daripada Lambdas**: Jika lambda hanya memanggil metode yang sudah ada, gunakan referensi metode (misal `Integer::sum`) untuk kejelasan.
*   **Gunakan Streams dengan bijak**: [[Java Streams]] dapat membuat kode lebih ringkas, tetapi penggunaan yang berlebihan dapat mengurangi keterbacaan. Hindari efek samping (side effects) dalam operasi stream.

## Metode

*   **Validasi parameter**: Periksa validitas parameter di awal metode dan dokumentasikan persyaratannya.
*   **Buat salinan defensif**: Jika kelas Anda memiliki klien yang tidak terpercaya atau mengembalikan referensi ke struktur data internal yang mutabel, buat salinan defensif (defensive copy) sebelum mengembalikan atau menyimpan referensi tersebut.

## Pemrograman Umum

*   **Minimalkan ruang lingkup variabel lokal**: Deklarasikan variabel sedekat mungkin dengan tempat penggunaannya.
*   **Lebih pilih for-each loops daripada for loops tradisional**: Lebih bersih dan mengurangi kesalahan indeks.
*   **Ketahui dan gunakan pustaka standar**: Jangan menemukan kembali roda. Gunakan `java.util`, `java.io`, dan pustaka standar lainnya yang telah diuji dan dioptimalkan.
*   **Hindari float dan double untuk perhitungan moneter**: Gunakan `BigDecimal`, `int`, atau `long` untuk perhitungan yang membutuhkan presisi tepat.
*   **Lebih pilih tipe primitif daripada boxed primitives**: Primitif lebih efisien. Hati-hati dengan `NullPointerException` saat unboxing otomatis.

## Pengecualian (Exceptions)

*   **Gunakan pengecualian hanya untuk kondisi luar biasa**: Jangan gunakan pengecualian untuk kontrol alur program biasa.
*   **Gunakan Checked Exceptions untuk kondisi yang dapat dipulihkan** dan **Runtime Exceptions untuk kesalahan pemrograman**.
*   **Lebih pilih pengecualian standar**: Gunakan `IllegalArgumentException`, `IllegalStateException`, `NullPointerException`, dll., agar kode lebih mudah dipahami.

## Konkurensi

*   **Sinkronisasi akses ke data mutabel bersama**: Tanpa sinkronisasi yang tepat, perubahan yang dibuat oleh satu thread mungkin tidak terlihat oleh thread lain.
*   **Lebih pilih Eksekutor, Tugas, dan Stream daripada Thread**: Gunakan kerangka kerja `java.util.concurrent` (seperti `ExecutorService`) yang memisahkan manajemen thread dari pekerjaan yang harus dilakukan.
*   **Hindari sinkronisasi yang berlebihan**: Ini dapat menyebabkan penurunan kinerja, deadlock, dan perilaku nondeterministik.

## Referensi

*   Bloch, Joshua. *Effective Java, 3rd Edition*. Addison-Wesley Professional, 2017.
*   [Effective Java - 3rd Edition Notes](https://ekis.github.io/effective-java-3rd-edition/)
*   [The Ultimate Guide to Effective Java: Best Practices Explained](https://medium.com/@navarend/the-ultimate-guide-to-effective-java-best-practices-explained-6ec3616a52e7)
