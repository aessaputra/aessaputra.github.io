---
title: Bytecode
categories:
  - "[[Posts]]"
tags:
  - java
  - programming
  - definition
  - computer-science
author:
  - "[[Aes Saputra]]"
url: https://aessaputra.net/notes/bytecode
created: "2025-12-18"
published: "2025-12-18"
date: "2025-12-18"
status: "[[Published]]"
contentType: concept
feed: show
aliases:
  - Bytecode
  - bytecode
  - portable code
  - p-code
---

**Bytecode** (juga dikenal sebagai *portable code* atau *p-code*) adalah bentuk kode instruksi perantara (*intermediate representation*) yang dirancang untuk dieksekusi oleh perangkat lunak interpreter atau [[Virtual Machine]] (VM), bukan secara langsung oleh perangkat keras (CPU).

Berbeda dengan [[Source Code|kode sumber]] yang dapat dibaca manusia atau [[Machine Code|kode mesin]] yang murni biner dan spesifik untuk prosesor tertentu, bytecode berada di tengah-tengah. Ia merupakan hasil kompilasi dari kode sumber yang telah melalui analisis semantik dan sintaksis, namun masih bersifat independen terhadap platform perangkat keras.

## Cara Kerja

Proses eksekusi program berbasis bytecode umumnya melibatkan dua tahapan utama:

1.  **Kompilasi ke Bytecode**: [[Source Code]] (misalnya `.java`) dikompilasi oleh [[Compilation|kompiler]] menjadi file bytecode (misalnya `.class`).
2.  **Eksekusi oleh VM**: Bytecode tersebut kemudian dijalankan oleh [[Virtual Machine]] (seperti [[JVM]] untuk Java atau PVM untuk Python). VM dapat mengeksekusi bytecode dengan dua cara:
    *   **Interpretasi**: Menerjemahkan instruksi satu per satu ke kode mesin saat program berjalan.
    *   **Just-In-Time (JIT) Compilation**: Menerjemahkan blok bytecode menjadi kode mesin asli di memori untuk meningkatkan performa eksekusi.

## Perbandingan Kode

| Fitur | [[Source Code]] | Bytecode | [[Machine Code]] |
| :--- | :--- | :--- | :--- |
| **Keterbacaan** | Tinggi (Manusia) | Rendah (Heksadesimal/Biner) | Tidak Ada (Biner Murni) |
| **Eksekusi** | Tidak bisa langsung | Melalui Virtual Machine | Langsung oleh CPU |
| **Portabilitas** | Perlu dikompilasi ulang | Sangat Tinggi (Portable) | Rendah (Spesifik Hardware) |
| **Abstraksi** | Tingkat Tinggi | Tingkat Menengah | Tingkat Rendah |

## Contoh Implementasi

### 1. [[Java]] (JVM)
Dalam ekosistem Java, bytecode adalah standar distribusi aplikasi.
*   File kode sumber `.java` dikompilasi menjadi `.class`.
*   Instruksi seperti `aload_0` atau `invokevirtual` adalah contoh perintah bytecode Java.
*   Ini memungkinkan prinsip *"Write Once, Run Anywhere"* (WORA).

### 2. Python
Meskipun sering disebut bahasa interpretasi, Python sebenarnya mengompilasi kode sumber menjadi bytecode (`.pyc`) sebelum dijalankan oleh Python Virtual Machine (PVM). Ini membantu mempercepat pemuatan program pada eksekusi berikutnya.

### 3. .NET (CIL)
Bahasa seperti C# dikompilasi menjadi *Common Intermediate Language* (CIL), yang merupakan bentuk bytecode untuk platform .NET. CIL kemudian dieksekusi oleh *Common Language Runtime* (CLR).

### 4. WebAssembly (Wasm)
WebAssembly adalah format instruksi biner (bytecode) modern untuk *stack-based virtual machine*. Wasm dirancang sebagai target portabel untuk kompilasi bahasa tingkat tinggi (C++, Rust) agar dapat berjalan di web browser dengan performa mendekati *native*.

## Keuntungan dan Tantangan

### Keuntungan
*   **Portabilitas**: Kode yang sama dapat berjalan di berbagai arsitektur (Intel, ARM, Apple Silicon) selama ada VM yang sesuai.
*   **Keamanan**: VM dapat memverifikasi bytecode sebelum dieksekusi (misalnya, *bytecode verifier* di JVM) untuk mencegah akses memori ilegal atau operasi berbahaya.
*   **Ukuran**: Umumnya lebih ringkas daripada kode sumber asli, menghemat ruang penyimpanan dan *bandwidth*.

### Tantangan
*   **Overhead Performa**: Eksekusi melalui perantara (VM) umumnya lebih lambat daripada kode mesin asli (native), meskipun teknologi JIT Compiler modern telah meminimalkan celah ini secara signifikan.
*   **Ketergantungan**: Membutuhkan instalasi lingkungan *runtime* (seperti JRE atau Python Runtime) di mesin target.

## Referensi

*   Wikipedia. (n.d.). *Bytecode*. Diambil dari [https://en.wikipedia.org/wiki/Bytecode](https://en.wikipedia.org/wiki/Bytecode)
*   TechTarget. (2022). *What is bytecode?*. Diambil dari [https://www.techtarget.com/whatis/definition/bytecode](https://www.techtarget.com/whatis/definition/bytecode)
*   Pure Storage. (2025). *Bytecode vs. Machine Code*. Diambil dari [https://blog.purestorage.com/purely-technical/bytecode-vs-machine-code/](https://blog.purestorage.com/purely-technical/bytecode-vs-machine-code/)
