---
title: Transformer Architecture - Simfoni Ruang Waktu
aliases:
  - Transformer
  - Attention Mechanism
  - Self-Attention
categories:
  - "[[Posts]]"
tags:
  - AI
  - Deep Learning
  - Architecture
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

## Pengantar: Konferensi Meja Bundar Digital
Bayangkan sebuah **Konferensi Meja Bundar Digital** di mana ratusan delegasi (kata-kata) duduk melingkar. Berbeda dengan metode lama ([[RNN]]) yang seperti permainan "pesan berantai" (informasi dibisikkan satu per satu dari telinga ke telinga), di meja bundar ini **semua orang bisa mendengar semua orang secara bersamaan**.

**Transformer Architecture** adalah ruang konferensi ajaib ini. Ia memungkinkan setiap kata dalam kalimat untuk berinteraksi langsung dengan setiap kata lainnya, tanpa harus menunggu giliran. Ini adalah revolusi **pemrosesan paralel** yang memungkinkan kelahiran **[[LLM]]** modern.

## Komponen Utama: Protokol Konferensi

### 1. Positional Encoding (Kartu Nama & Nomor Kursi)
Karena semua orang berbicara sekaligus, kita kehilangan informasi urutan (mana yang bicara duluan?).
*   **Analogi**: Setiap delegasi diberi kartu nama khusus yang berisi koordinat GPS matematika (sinus/cosinus).
*   **Fungsi**: Memberi tahu model bahwa kata "Saya" ada di posisi 1 dan "Makan" ada di posisi 2, meskipun mereka diproses bersamaan. Tanpa ini, "Anjing gigit Orang" dan "Orang gigit Anjing" akan dianggap sama.

### 2. Self-Attention (Mendengar Selektif)
Saat delegasi "Bank" berbicara, dia perlu tahu konteksnya. Apakah dia harus mendengarkan delegasi "Uang" atau delegasi "Sungai"?
*   **Analogi**: Setiap delegasi memancarkan sinyal "Pertanyaan" (Query), memegang "Kunci" (Key), dan membawa "Isi Pesan" (Value).
    *   **Query (Q)**: "Saya mencari konteks finansial."
    *   **Key (K)**: "Saya adalah kata yang berhubungan dengan uang."
    *   **Value (V)**: "Inilah makna saya."
*   Jika Q dan K cocok (resonansi tinggi), maka perhatian (Attention) diberikan penuh.

### 3. Multi-Head Attention (Tim Notulen)
Satu pasang telinga tidak cukup. Kita butuh beberapa tim notulen yang mendengarkan aspek berbeda.
*   **Head 1**: Fokus pada tata bahasa (Subjek-Predikat).
*   **Head 2**: Fokus pada hubungan waktu (Dulu-Sekarang).
*   **Head 3**: Fokus pada emosi/sentimen.
*   Hasil laporan dari semua tim ini digabungkan untuk pemahaman yang utuh.

### 4. Feed-Forward Networks (Otak Delegasi)
Setelah mengumpulkan informasi dari rekan-rekannya (melalui Attention), setiap delegasi merenung sendiri untuk memproses informasi tersebut.
*   Ini adalah lapisan pemrosesan individual yang terjadi secara paralel untuk setiap kata.

## Arsitektur: Encoder vs Decoder

Awalnya, Transformer memiliki dua bagian (seperti di paper "Attention Is All You Need"), namun LLM modern seringkali hanya memakai salah satunya.

### 1. Encoder (Si Pembaca/Penyimak)
*   **Tugas**: Memahami input secara utuh (bi-directional/dua arah). Dia bisa melihat ke kiri dan ke kanan kalimat sekaligus.
*   **Contoh**: [[BERT]] (bagus untuk klasifikasi teks, analisis sentimen).
*   **Analogi**: Kritikus sastra yang membaca seluruh buku sebelum membuat ulasan.

### 2. Decoder (Si Pendongeng/Penenun)
*   **Tugas**: Menghasilkan output satu per satu (uni-directional/satu arah). Dia hanya bisa melihat apa yang sudah ditulis sebelumnya, tidak bisa mengintip masa depan.
*   **Contoh**: [[GPT]] (Generative Pre-trained Transformer).
*   **Analogi**: Penulis novel yang menulis kata demi kata berdasarkan apa yang baru saja dia tulis.

## Visualisasi: Alur Data di Meja Bundar

```mermaid
graph TD
    Input[Input: 'Saya suka AI'] --> PosEnc(Positional Encoding\n+Nomor Urut)
    PosEnc --> MultiHead[Multi-Head Attention\n(Rapat Meja Bundar)]
    MultiHead --> Norm1[Add & Norm\n(Stabilisasi)]
    Norm1 --> FFN[Feed Forward Network\n(Pemrosesan Individu)]
    FFN --> Norm2[Add & Norm]
    Norm2 --> Output[Output Vector]
    
    subgraph "Mekanisme Attention"
    Q[Query: Apa yang saya cari?]
    K[Key: Apa yang saya tawarkan?]
    V[Value: Apa isi pesan saya?]
    Q -- Hitung Kecocokan --> MatMul(Dot Product)
    K --> MatMul
    MatMul -- Bobot Perhatian --> Softmax
    Softmax -- Kalikan --> V
    V --> Context[Context Vector]
    end
```

*Diagram di atas menunjukkan bagaimana satu blok Transformer memproses data, dengan detail mekanisme Q, K, V di dalamnya.*

## Refleksi: Revolusi Paralel
Transformer mengubah dunia AI karena ia menghapus hambatan antrian. Dengan mengizinkan **paralelisasi masif**, kita bisa melatih model dengan data seukuran internet (seperti [[LLM]]) dalam waktu yang masuk akal. Ia mengajarkan kita bahwa kecerdasan bukan hanya tentang seberapa banyak yang kita tahu, tapi seberapa baik kita **memperhatikan** hubungan antar hal-hal yang kita tahu.
