---
title: Java Fundamentals
categories:
  - "[[Posts]]"
tags:
  - java
  - programming
  - backend
  - jvm
author:
  - "[[Aes Saputra]]"
url: https://aessaputra.net/notes/java-fundamentals
created: "2025-12-18"
published: "2025-12-18"
date: "2025-12-18"
topics:
  - "[[Programming Language]]"
  - "[[Software Development]]"
status: "[[Published]]"
feed: show
aliases:
  - java-basics
  - java-intro
  - java fundamentals
contentType: concept
---

**Java** adalah bahasa pemrograman tingkat tinggi, berbasis kelas, dan berorientasi objek yang dirancang untuk memiliki ketergantungan implementasi seminimal mungkin. Awalnya dikembangkan oleh **James Gosling** di **Sun Microsystems** (sekarang diakuisisi oleh [[Oracle]]) dan dirilis pada tahun 1995, Java telah menjadi salah satu bahasa pemrograman paling populer di dunia, digunakan untuk segala hal mulai dari aplikasi seluler hingga sistem perusahaan berskala besar.

## Filosofi Utama: Write Once, Run Anywhere

Prinsip inti Java adalah **WORA** (*Write Once, Run Anywhere*). Artinya, kode Java yang dikompilasi (bytecode) dapat berjalan di semua platform yang mendukung Java tanpa perlu dikompilasi ulang. Hal ini dimungkinkan berkat adanya [[JVM]] (*Java Virtual Machine*).

## Arsitektur Java

Memahami arsitektur Java sangat penting untuk pengembang. Terdapat tiga komponen utama yang sering membingungkan pemula:

### 1. JDK (Java Development Kit)
[[JDK]] adalah paket pengembangan perangkat lunak lengkap yang digunakan untuk mengembangkan aplikasi Java. Ini mencakup **JRE** (Java Runtime Environment), serta alat pengembangan seperti *compiler* (`javac`), *debugger*, dan *archiver* (`jar`).
*   **Fungsi**: Untuk *menulis* dan *mengompilasi* kode Java.

### 2. JRE (Java Runtime Environment)
[[JRE]] adalah bagian dari JDK yang menyediakan perpustakaan kelas standar, JVM, dan komponen lain yang diperlukan untuk *menjalankan* aplikasi Java. JRE tidak menyertakan alat pengembangan seperti compiler.
*   **Fungsi**: Untuk *menjalankan* aplikasi Java (User Environment).

### 3. JVM (Java Virtual Machine)
[[JVM]] adalah mesin abstrak yang menjadi jantung dari portabilitas Java. JVM membaca dan mengeksekusi *bytecode* (`.class`) yang dihasilkan oleh compiler. JVM menerjemahkan bytecode tersebut ke dalam bahasa mesin (*native code*) yang spesifik untuk sistem operasi tempat ia berjalan.
*   **Fungsi**: Jembatan antara bytecode dan perangkat keras (Hardware).

## Konsep Object-Oriented Programming (OOP)

Java adalah bahasa yang murni berorientasi objek (kecuali tipe data primitif). Empat pilar utama [[OOP]] dalam Java adalah:

1.  **Encapsulation (Enkapsulasi)**: Membungkus data (variabel) dan kode yang beroperasi pada data (metode) menjadi satu unit (kelas). Ini juga melibatkan penyembunyian detail internal dan hanya mengekspos fungsionalitas melalui metode publik (*getters/setters*).
2.  **Inheritance (Pewarisan)**: Mekanisme di mana satu kelas (subclass/child) dapat mewarisi fitur (field dan method) dari kelas lain (superclass/parent). Ini mempromosikan penggunaan kembali kode (*code reusability*).
3.  **Polymorphism (Polimorfisme)**: Kemampuan objek untuk mengambil banyak bentuk. Dalam Java, ini sering terlihat melalui *Method Overloading* (nama sama, parameter beda) dan *Method Overriding* (implementasi ulang metode parent di child class).
4.  **Abstraction (Abstraksi)**: Menyembunyikan kompleksitas implementasi dan hanya menampilkan fitur-fitur penting dari suatu objek. Ini dicapai menggunakan `abstract class` dan `interface`.

## Manajemen Memori

Java mengelola memori secara otomatis, berbeda dengan bahasa seperti C++ di mana pengembang harus mengalokasikan dan menghapus memori secara manual.

*   **Stack Memory**: Digunakan untuk eksekusi *thread*. Berisi nilai primitif yang spesifik untuk metode dan referensi ke objek di Heap. Bersifat LIFO (*Last-In-First-Out*).
*   **Heap Memory**: Area memori runtime tempat objek dialokasikan. Semua objek Java (instance dari kelas) disimpan di sini.
*   **Garbage Collection (GC)**: Proses otomatis di latar belakang yang mengidentifikasi dan membuang objek yang tidak lagi digunakan (tidak memiliki referensi aktif) untuk membebaskan memori di Heap.

## Sintaks Dasar

Setiap aplikasi Java dimulai dari metode `main`. Berikut adalah struktur dasar program Java:

```java
public class HelloWorld {
    // Entry point aplikasi
    public static void main(String[] args) {
        System.out.println("Halo, Dunia!");
    }
}
```

### Tipe Data
Java memiliki dua kategori tipe data:
1.  **Primitif**: Tipe data dasar yang menyimpan nilai aktual (`int`, `double`, `boolean`, `char`, `byte`, `short`, `long`, `float`).
2.  **Non-Primitif (Reference)**: Merujuk pada objek (`String`, `Array`, `Class`, `Interface`).

## Evolusi Modern Java (LTS Versions)

Java terus berkembang dengan siklus rilis 6 bulanan. Versi *Long-Term Support* (LTS) adalah versi yang paling stabil dan direkomendasikan untuk produksi.

*   **[[Java 8]] (LTS)**: Memperkenalkan perubahan revolusioner seperti **Lambda Expressions**, **Stream API**, dan **Optional**. Ini membawa paradigma pemrograman fungsional ke dalam Java.
*   **[[Java 11]] (LTS)**: Memperkenalkan `var` untuk inferensi tipe variabel lokal, HTTP Client baru, dan penghapusan modul Java EE dan CORBA.
*   **[[Java 17]] (LTS)**: Memperkenalkan **Records** (kelas data ringkas), **Sealed Classes** (kontrol pewarisan), dan *Pattern Matching* untuk `instanceof`.
*   **[[Java 21]] (LTS)**: Fitur mutakhir seperti **Virtual Threads** ([[Project Loom]]) untuk konkurensi skala tinggi, *Sequenced Collections*, dan *String Templates* (Preview).

## Ekosistem

Ekosistem Java sangat luas dan matang:
*   **Build Tools**: [[Maven]] dan [[Gradle]] adalah standar industri untuk manajemen dependensi dan otomatisasi build.
*   **Frameworks**: [[Spring Boot]] adalah framework paling populer untuk pengembangan aplikasi enterprise dan microservices. [[Jakarta EE]] (sebelumnya Java EE) menyediakan standar untuk aplikasi server-side.
*   **IDE**: [[IntelliJ IDEA]], [[Eclipse]], dan [[VS Code]] adalah lingkungan pengembangan utama.

## Catatan Terkait

Berikut adalah topik terkait yang tersedia di dalam knowledge base ini:
*   [[Head First Java]]
*   [[Thinking in Java]]
*   [[Effective Java]]
*   [[Java: A Beginners Guide]]
*   [[Java: The Complete Reference]]

### Referensi
*   [Oracle Java Documentation](https://docs.oracle.com/en/java/)
*   [Baeldung - Java Guides](https://www.baeldung.com/)
*   [GeeksforGeeks - Java](https://www.geeksforgeeks.org/java/)
