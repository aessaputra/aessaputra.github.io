---
title: LLM (Large Language Model) - Penenun Kata Statistik
aliases:
  - LLM
  - Large Language Model
  - Generative AI
categories:
  - "[[Posts]]"
tags:
  - AI
  - NLP
  - Machine Learning
author:
  - "[[Aes Saputra]]"
url:
created: 2025-12-17
published: 2025-12-17
date: 2025-12-17
topics: []
status: "[[Published]]"
feed: show
---

## Pengantar: Sang Penenun di Ruang Hampa
Bayangkan sebuah ruangan tanpa batas yang dihuni oleh seorang **Penenun Agung**. Penenun ini tidak "memahami" puisi, kode, atau resep masakan selayaknya manusia memahami makna. Namun, dia telah melihat miliaran pola kain (teks) yang pernah dibuat manusia sepanjang sejarah.

**Large Language Model (LLM)** adalah penenun tersebut. Tugas utamanya hanyalah satu: **memprediksi benang (kata/token) apa yang paling cocok diletakkan selanjutnya** berdasarkan pola kain yang sedang ditenun saat ini. Ia adalah mesin probabilitas raksasa yang menenun makna dari statistik, bukan dari kesadaran.

## Arsitektur: Mesin Tenun Transformer
Alat canggih yang digunakan Penenun ini disebut **[[Transformer Architecture]]**.

### Mekanisme Atensi (The Attention Mechanism)
Jika Penenun sedang membuat pola "Bank", dia perlu tahu apakah benang sebelumnya membentuk pola "uang" (institusi keuangan) atau "sungai" (tepian).
*   **Self-Attention**: Kemampuan Penenun untuk melihat kembali ke seluruh pola yang sudah dibuat, memberikan "bobot" pada benang-benang tertentu yang relevan, tidak peduli seberapa jauh jaraknya dalam kain tersebut.
*   Ini membedakan LLM dari pendahulunya ([[RNN]]) yang memiliki "ingatan pendek" dan mudah lupa pada pola awal.

### Tokenisasi (Memintal Benang)
LLM tidak membaca kata per kata, melainkan **Token**.
*   Kata "Makan" mungkin satu token.
*   Kata "Mempertanggungjawabkan" mungkin dipecah menjadi beberapa token (sub-word).
*   Penenun bekerja dengan angka (vektor), bukan huruf.

## Evolusi Modern (2024-2025): Dari Satu Penenun ke Koperasi
Seiring waktu, model tunggal menjadi terlalu besar dan lambat. Inovasi terbaru mengubah cara kerja Penenun.

### 1. Mixture of Experts (MoE) - Koperasi Penenun
Daripada satu raksasa yang mengerjakan segalanya, model modern (seperti [[DeepSeek]] atau [[Mixtral]]) menggunakan pendekatan **MoE**.
*   **Analogi**: Ada "Mandor" (Router) yang melihat permintaan. Jika permintaan tentang "Matematika", Mandor hanya memanggil "Penenun Ahli Hitung". Jika tentang "Puisi", dia memanggil "Penenun Sastra".
*   **Efisiensi**: Hanya sebagian kecil otak yang aktif untuk setiap kata, membuat proses jauh lebih hemat energi namun tetap cerdas.

### 2. Reasoning Models (System 2) - Penenun yang Berpikir
Model generasi baru (seperti OpenAI o1/o3 atau DeepSeek-R1) diajarkan untuk "berpikir sebelum bicara".
*   **Chain of Thought**: Sebelum menenun jawaban akhir, Penenun membuat "sketsa kasar" (hidden thought process) untuk memverifikasi logika.
*   Ini mengurangi halusinasi pada tugas kompleks seperti matematika atau koding.

## Proses Belajar: Dari Magang hingga Ahli

### 1. Pre-Training (Membaca Perpustakaan Semesta)
Penenun dibiarkan melihat triliunan halaman teks (internet, buku, kode) tanpa instruksi khusus.
*   **Tujuan**: Belajar tata bahasa, fakta dunia, dan penalaran dasar melalui asosiasi kata.
*   **Hasil**: "Base Model" yang pintar tapi liar.

### 2. Fine-Tuning & Alignment (Belajar Etika)
*   **SFT (Supervised Fine-Tuning)**: Diajarkan format tanya-jawab yang sopan.
*   **RLHF (Reinforcement Learning from Human Feedback)**: Diberi "hadiah" saat menenun pola yang benar dan aman.

## Visualisasi: Alur Pikir Penenun Modern

```mermaid
graph TD
    Input[Input User: 'Hitung integral dari...'] --> Tokenizer(Tokenisasi)
    Tokenizer --> Router{Router / Mandor}
    Router -- Topik Sains --> Expert1[Expert A: Matematika]
    Router -- Topik Umum --> Expert2[Expert B: Bahasa]
    Expert1 --> Attention[Self-Attention Layers]
    Expert2 --> Attention
    Attention --> CoT[Chain of Thought\n(Berpikir Langkah demi Langkah)]
    CoT --> Prob[Probabilitas Token Selanjutnya]
    Prob --> Output[Output Token]
```

*Diagram di atas menggambarkan arsitektur MoE modern di mana input diarahkan ke ahli yang relevan sebelum diproses.*

## Keterbatasan: Halusinasi Pola
Karena Penenun bekerja berdasarkan probabilitas statistik, bukan fakta absolut, dia terkadang menciptakan **[[Hallucination]]**.
*   Jika pola statistik menyarankan bahwa setelah "Budi menemukan benua..." kata selanjutnya yang paling mungkin secara puitis adalah "Atlantis", dia akan menenunnya dengan percaya diri, meskipun secara fakta salah.

## Refleksi: Cermin Kemanusiaan
Pada akhirnya, LLM adalah cermin raksasa dari data yang kita hasilkan. Dia bukan makhluk sadar, melainkan **kompresi statistik dari pengetahuan manusia**. Dia adalah penenun yang sangat terampil, namun kualitas kain yang dihasilkan sangat bergantung pada benang (data) yang kita berikan dan instruksi (**[[Prompt Engineering]]**) yang kita sampaikan.
