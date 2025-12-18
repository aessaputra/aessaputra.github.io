---
title: Compilation
categories:
  - "[[Posts]]"
tags:
  - programming
  - compiler
  - computer-science
author:
  - "[[Aes Saputra]]"
url: https://aessaputra.net/notes/compilation
created: "2025-12-18"
published: "2025-12-18"
date: "2025-12-18"
status: "[[Published]]"
contentType: concept
feed: show
aliases:
  - Kompilasi
  - kompilasi
  - compilation
  - compiler
  - kompiler
---

**Compilation** (kompilasi) adalah proses transformasi [[Source Code|kode sumber]] yang ditulis dalam bahasa pemrograman tingkat tinggi (seperti C++, Java, atau Rust) menjadi bahasa tingkat rendah (seperti [[Machine Code|kode mesin]] atau [[Bytecode|bytecode]]) agar dapat dieksekusi oleh komputer. Program yang melakukan tugas ini disebut **kompiler** (*compiler*).

Tujuan utama kompilasi adalah menghasilkan program eksekusi yang efisien sambil mendeteksi kesalahan sintaksis dan semantik dalam kode sumber sebelum program dijalankan.

## Tahapan Kompilasi

Proses kompilasi modern umumnya melibatkan serangkaian tahapan yang kompleks, yang sering dikelompokkan menjadi dua bagian besar: **Front-end** (Analisis) dan **Back-end** (Sintesis).

### 1. Lexical Analysis (Scanning)
Tahap pertama di mana kompiler membaca aliran karakter dari kode sumber dan mengelompokkannya menjadi unit-unit bermakna yang disebut **token**.
*   **Input**: `int x = 10;`
*   **Output**: Token `KEYWORD(int)`, `ID(x)`, `OP(=)`, `LITERAL(10)`, `PUNCT(;)`.

### 2. Syntax Analysis (Parsing)
Kompiler menyusun token-token tersebut menjadi struktur pohon hirarkis yang disebut **Syntax Tree** atau **Parse Tree** berdasarkan tata bahasa (*grammar*) bahasa pemrograman tersebut.
*   Memastikan struktur kode valid (misalnya, memastikan kurung tutup seimbang).

### 3. Semantic Analysis
Memeriksa makna dari struktur sintaksis untuk memastikan konsistensi logika.
*   **Type Checking**: Memastikan operasi dilakukan pada tipe data yang kompatibel (misalnya, tidak menjumlahkan *string* dengan *integer* secara langsung).
*   **Scope Resolution**: Memastikan variabel telah dideklarasikan sebelum digunakan.

### 4. Intermediate Code Generation
Menghasilkan representasi kode perantara (*Intermediate Representation* atau IR) yang independen terhadap mesin.
*   Contoh: *Three-Address Code*.
*   IR memungkinkan kompiler untuk mendukung berbagai arsitektur mesin tanpa harus menulis ulang bagian *front-end*.

### 5. Code Optimization
Tahap krusial untuk meningkatkan efisiensi program tanpa mengubah fungsinya.
*   **Dead Code Elimination**: Menghapus kode yang tidak pernah dieksekusi.
*   **Loop Optimization**: Mengurangi overhead dalam perulangan.
*   **Constant Folding**: Menghitung ekspresi konstan pada saat kompilasi (misalnya, mengubah `3 + 4` menjadi `7`).

### 6. Code Generation
Menerjemahkan IR yang telah dioptimalkan menjadi kode target spesifik (biasanya [[Machine Code|bahasa mesin]] atau [[Assembly]]).
*   Mengalokasikan register memori dan instruksi prosesor yang sesuai.

## Jenis-Jenis Kompilator

*   **Ahead-of-Time (AOT) Compiler**: Mengompilasi seluruh kode menjadi kode mesin *sebelum* program dijalankan. Contoh: GCC (C/C++), Rustc.
*   **Just-In-Time (JIT) Compiler**: Mengompilasi kode (biasanya [[Bytecode]]) menjadi kode mesin *saat* program sedang berjalan (runtime). Contoh: [[JVM]] (Java), V8 (JavaScript).
*   **Cross-Compiler**: Berjalan di satu arsitektur (misal: Windows x86) tetapi menghasilkan kode untuk arsitektur lain (misal: Android ARM).
*   **Transpiler (Source-to-Source)**: Menerjemahkan satu bahasa tingkat tinggi ke bahasa tingkat tinggi lainnya (misal: TypeScript ke JavaScript).

## Kompilator vs Interpreter

| Fitur | Kompilator | Interpreter |
| :--- | :--- | :--- |
| **Cara Kerja** | Menerjemahkan seluruh kode sekaligus sebelum eksekusi. | Menerjemahkan dan mengeksekusi kode baris demi baris. |
| **Kecepatan Eksekusi** | Lebih cepat (karena sudah berupa kode mesin). | Lebih lambat (ada overhead terjemahan saat runtime). |
| **Deteksi Error** | Melaporkan semua error setelah pemindaian selesai. | Melaporkan error segera saat baris bermasalah dieksekusi. |
| **Output** | Menghasilkan file eksekusi (misal `.exe`). | Tidak menghasilkan file eksekusi mandiri. |
| **Contoh** | C, C++, Rust, Go. | Python, Ruby, PHP, JavaScript (awal). |

## Contoh Implementasi

### 1. [[Java]] (`javac`)
Java menggunakan pendekatan hibrida.
1.  `javac` mengompilasi kode sumber (`.java`) menjadi [[Bytecode]] (`.class`).
2.  Saat dijalankan, [[JVM]] menggunakan JIT Compiler untuk menerjemahkan bytecode ke kode mesin asli sesuai perangkat keras pengguna.

### 2. C++ (`gcc` / `clang`)
Menggunakan kompilasi murni AOT. Kode sumber dikompilasi langsung menjadi kode mesin biner yang spesifik untuk sistem operasi dan arsitektur CPU target.

## Referensi

*   GeeksforGeeks. (2025). *Phases of a Compiler*. Diambil dari [https://www.geeksforgeeks.org/compiler-design/phases-of-a-compiler/](https://www.geeksforgeeks.org/compiler-design/phases-of-a-compiler/)
*   GeeksforGeeks. (2025). *Language Processors: Assembler, Compiler and Interpreter*. Diambil dari [https://www.geeksforgeeks.org/computer-science-fundamentals/language-processors-assembler-compiler-and-interpreter/](https://www.geeksforgeeks.org/computer-science-fundamentals/language-processors-assembler-compiler-and-interpreter/)
*   Group-21. (2023). *Types of Compilers*. Medium. Diambil dari [https://medium.com/@grp-21/types-of-compilers-ac2e9f5ab4cd](https://medium.com/@grp-21/types-of-compilers-ac2e9f5ab4cd)
