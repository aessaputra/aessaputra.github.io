---
title: Kompilasi di Java | JIT vs AOT
categories:
  - "[[Posts]]"
tags:
  - posts
author:
  - "[[Aes Saputra]]"
url: https://aessaputra.net/notes/kompilasi-di-java-jit-vs-aot
created: "2025-12-18"
published: "2025-12-18"
date: "2025-12-18"
topics: ["[[Java]]", "[[Kompilasi]]", "[[JIT]]", "[[AOT]]", "[[JVM]]", "[[GraalVM]]"]
status: "[[Published]]"
contentType: concept
feed: show
aliases:
  - JIT vs AOT Java
  - Kompilasi Java
  - Compilation in Java JIT vs AOT
---

Dalam pengembangan aplikasi [[Java]], proses kompilasi merupakan langkah krusial yang mengubah kode sumber menjadi instruksi yang dapat dieksekusi oleh komputer. Ada dua pendekatan utama dalam kompilasi Java yang memiliki karakteristik dan implikasi kinerja yang berbeda: [[Just-in-Time (JIT) Compilation]] dan [[Ahead-of-Time (AOT) Compilation]]. Artikel ini akan membahas perbedaan mendasar antara keduanya, kelebihan dan kekurangannya, serta skenario penggunaan yang optimal.

## Cara Kerja Kompilasi di Java

Secara umum, kompilasi adalah proses menerjemahkan program yang ditulis dalam bahasa tingkat tinggi (seperti Java) menjadi kode mesin tingkat rendah yang dapat dipahami oleh [[CPU]]. Kode mesin ini berisi instruksi biner yang dapat didekode dan dieksekusi. Proses ini dilakukan oleh sebuah [[Compiler]] yang juga dapat melakukan berbagai optimasi untuk mempercepat eksekusi program atau mengurangi konsumsi sumber daya.

Karena Java dirancang sebagai bahasa yang [[Platform Independent]], kode sumber Java pertama-tama dikonversi menjadi [[JVM Bytecode]]. Bytecode ini kemudian diinterpretasikan atau dikompilasi lebih lanjut oleh [[Java Virtual Machine (JVM)]] yang terinstal di komputer menjadi kode mesin yang spesifik untuk platform tersebut. Tahap tambahan inilah yang memungkinkan prinsip [[WORA (Write Once, Run Anywhere)]] pada Java.

Perbedaan utama antara JIT dan AOT terletak pada kapan terjemahan dari bytecode ke kode mesin ini terjadi: sebelum atau selama eksekusi program.

## Apa itu JIT Compiler?

[[Just-in-Time (JIT) Compilation]], atau kompilasi dinamis, adalah proses di mana [[JVM Bytecode]] dikonversi menjadi kode mesin oleh [[JVM]] setelah program dimulai, yaitu saat runtime.

Tujuan utama dari JIT compiler adalah menghasilkan kode yang sangat berkinerja. Prosesnya melibatkan beberapa tahapan:

1.  **Analisis Kode**: JIT compiler menganalisis kode untuk mengidentifikasi bagian-bagian yang sering digunakan (disebut "hotspots"). Ini juga mempertimbangkan sistem operasi tempat kode berjalan.
2.  **Optimasi**: Setelah mengidentifikasi hotspot, JIT compiler menerapkan berbagai optimasi yang dianggap perlu, seperti optimasi global, lokal, dan kontrol alur. Semakin banyak optimasi yang dilakukan, semakin baik kode yang dihasilkan, namun semakin lama pula "waktu pemanasan" (warmup time) yang merupakan penundaan dalam eksekusi program aktual.

Intensitas optimasi dapat bervariasi. [[HotSpot]], JVM paling populer, menyediakan dua compiler:

*   **C1 (Client Compiler)**: Memulai optimasi segera dengan optimasi sederhana. Menghasilkan startup yang lebih cepat tetapi kode kurang teroptimasi.
*   **C2 (Server Compiler)**: Mengamati kode yang berjalan untuk mengumpulkan data profil sebelum memulai optimasi yang lebih agresif. Ini meningkatkan waktu pemanasan tetapi menghasilkan kode yang lebih berkinerja.

Selain itu, JIT compiler dapat melakukan [[Adaptive Optimization]] dan secara dinamis mengkompilasi ulang bagian kode selama eksekusi aplikasi jika ada perubahan atau metode baru yang diperlukan.

JIT kompilasi menghasilkan kode yang berkinerja tinggi untuk kasus penggunaan dan lingkungan spesifik tempat ia berjalan. JIT juga mendukung berbagai [[Garbage Collector]], termasuk kolektor latensi rendah seperti [[ZGC]] di versi Java yang lebih baru, memungkinkan pengurangan latensi atau peningkatan throughput sesuai kebutuhan.

### Kelebihan JIT:

*   **Kode Berkinerja Tinggi**: Berkat berbagai teknik optimasi kinerja.
*   **Optimasi Kinerja Dinamis**: Dapat mengoptimalkan ulang saat aplikasi berjalan.
*   **Alat Debugging dan Pemantauan yang Familiar**.

### Kekurangan JIT:

*   **Periode Pemanasan yang Panjang**: Dapat memakan waktu beberapa menit, menyebabkan latensi lebih tinggi di awal. Proses ini berulang setiap kali aplikasi dimulai ulang.
*   **Overhead Lebih Tinggi di Awal**: Aplikasi menggunakan lebih banyak sumber daya selama pemanasan.
*   **Ukuran Image Container Lebih Besar**: Karena menyertakan kode yang dikompilasi ditambah JVM.

### Mitigasi Kekurangan JIT dengan Alpaquita Containers dan CRaC

Untuk mengatasi masalah waktu pemanasan dan konsumsi sumber daya, teknologi seperti [[Alpaquita Containers]] yang mendukung [[Coordinated Restore at Checkpoint (CRaC) API]] hadir. CRaC memungkinkan pengembang untuk mengambil snapshot dari aplikasi Java yang sedang berjalan, menyimpan keadaannya ke file, dan kemudian mengembalikannya dari file tersebut. Ini mengurangi waktu startup dan pemanasan dari menit menjadi milidetik, serta menghilangkan overhead memori karena keadaan aplikasi sudah stabil.

## HotSpot vs GraalVM

[[HotSpot]] bukanlah satu-satunya JIT compiler di ekosistem Java. Ada juga [[OpenJ9]] yang dikembangkan oleh IBM. Namun, yang menarik adalah [[GraalVM]], sebuah [[JDK]] yang ditulis dalam Java.

JIT compiler GraalVM menawarkan optimasi tambahan yang dalam beberapa kasus mengungguli HotSpot. GraalVM juga menyertakan teknologi [[Native Image]] yang memungkinkan kompilasi [[Ahead-of-Time (AOT)]] untuk aplikasi Java.

## Apa itu AOT Compiler?

[[Ahead-of-Time (AOT) Compilation]], atau kompilasi statis, terjadi sebelum eksekusi program, yaitu pada waktu build. AOT compiler GraalVM melakukan analisis statis kode di bawah asumsi "closed-world", yang berarti semua kelas yang akan dibutuhkan saat runtime diasumsikan dapat dijangkau pada waktu build.

Compiler ini menerjemahkan bytecode menjadi kode mesin yang spesifik untuk sistem operasi dan arsitektur target. Semua kelas yang diperlukan diinisialisasi, dan kodenya dimuat ke dalam satu executable native bersama dengan kelas pustaka yang diperlukan dan kode yang terhubung secara statis dari JDK.

Executable native yang dihasilkan memiliki waktu startup yang hampir instan karena tidak perlu mencari hotspot atau melakukan interpretasi bytecode saat runtime.

AOT compiler menghilangkan kode dan dependensi yang tidak terpakai, dan karena file executable tidak memerlukan JVM untuk berjalan, ini membantu:

*   **Mengurangi Konsumsi Memori secara Drastis**.
*   **Mempercepat Startup** hingga 1/10 detik.
*   **Mencapai Kinerja Puncak Segera** tanpa pemanasan.
*   **Meningkatkan Keamanan** berkat permukaan serangan yang lebih kecil.

Keuntungan signifikan lainnya dari kompilasi AOT adalah kode executable native yang dihasilkan sangat sulit untuk di-reverse engineer, terutama jika melalui [[Obfuscator]] sebelum kompilasi. Ini menambah tingkat perlindungan [[IP Protection]] ekstra.

### Kekurangan AOT:

*   **Pembangunan Image Native yang Sangat Membutuhkan Sumber Daya**: Membutuhkan alokasi memori gigabyte untuk proses build.
*   **Tidak Ada Optimasi Kinerja Dinamis**: Karena executable tidak mengandung JVM, optimasi kinerja lebih lanjut tidak mungkin dilakukan setelah kompilasi.
*   **Rentang Garbage Collector yang Terbatas**: GraalVM menawarkan jumlah garbage collector yang terbatas (SerialGC di GraalVM Community Edition dan G1GC di GraalVM Enterprise Edition).
*   **Tidak Kompatibel dengan Fitur Dinamis Java**: Fitur seperti [[Reflection]], [[JNI]], [[Dynamic Proxy]] tidak didukung secara langsung. Ini memerlukan solusi seperti menulis ulang kode atau menyediakan metadata melalui [[Tracing Agent]].
*   **Diagnostik yang Menantang**.

### Mitigasi Kekurangan AOT dengan Liberica Native Image Kit

Untuk meningkatkan kinerja image native, [[Liberica Native Image Kit (NIK)]] dapat digunakan. NIK, yang dikembangkan oleh BellSoft, menambahkan implementasi [[ParallelGC]] yang dapat meningkatkan latensi secara signifikan (10–40% menurut studi mereka). NIK juga direkomendasikan oleh Spring sebagai alat build native, menjanjikan integrasi yang mulus dengan proyek Spring Boot.

## JIT vs AOT: Ringkasan

Baik JIT maupun AOT compiler menawarkan pendekatan berbeda untuk mengoptimalkan kinerja aplikasi Java.

[[JIT Compilation]] memungkinkan kinerja keseluruhan yang lebih tinggi dan optimasi kinerja dinamis. Namun, ia memiliki waktu pemanasan yang panjang dan konsumsi memori yang lebih tinggi. Solusi seperti [[Alpaquita Containers]] dengan [[CRaC API]] dapat mengatasi kekurangan ini.

[[AOT Compilation]] memungkinkan pembuatan image native dengan startup yang hampir instan, konsumsi memori yang lebih rendah, dan keamanan yang lebih baik. Namun, ia tidak menyediakan optimasi kinerja dinamis, memiliki pilihan [[Garbage Collector]] yang terbatas, dan tantangan dalam menangani fitur dinamis Java. [[Liberica Native Image Kit]] dapat membantu mitigasi beberapa kekurangan AOT.

Tidak ada solusi tunggal yang cocok untuk semua. Pilihan antara JIT dan AOT harus didasarkan pada kebutuhan spesifik proyek Anda, dengan mempertimbangkan [[SLO (Service Level Objectives)]] dan mengevaluasi risiko yang terkait dengan kelebihan dan kekurangan masing-masing pendekatan.

---
**Referensi:**
*   Bell-SW. (2024, May 13). *Compilation in Java: JIT vs AOT*. Diperoleh dari [https://bell-sw.com/blog/compilation-in-java-jit-vs-aot/](https://bell-sw.com/blog/compilation-in-java-jit-vs-aot/)
