---
title: Fine Tuning - Pendidikan Spesialis
aliases:
  - Fine-Tuning
  - Transfer Learning
  - RLHF
  - Instruction Tuning
  - Fine Tuning
categories:
  - "[[Posts]]"
tags:
  - AI
  - Machine Learning
  - LLM
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

## Pengantar: Dokter Umum vs. Dokter Spesialis

Bayangkan sebuah **Model Pre-trained** (seperti GPT-5 atau Llama 3) sebagai seorang lulusan fakultas kedokteran yang jenius. Ia telah membaca semua buku teks medis di dunia, menghafal anatomi, dan mengerti dasar-dasar penyakit. Ia adalah **Dokter Umum** yang sangat cerdas. Namun, jika Anda memintanya melakukan bedah saraf mikro yang rumit besok pagi, ia mungkin akan gemetar. Ia punya dasarnya, tapi belum punya "jam terbang" spesifik.

**Fine Tuning** adalah proses **Pendidikan Spesialis (Residensi)**. Ini adalah fase di mana kita mengambil dokter umum yang jenius tersebut, dan memasukkannya ke dalam program pelatihan intensif khusus untuk bedah saraf. Kita tidak mengajarinya cara membaca atau cara menggunakan stetoskop lagi (karena ia sudah tahu). Kita hanya fokus melatihnya pada nuansa, teknik, dan kasus-kasus spesifik bedah saraf.

Dalam dunia [[Machine Learning]], Fine Tuning menyesuaikan bobot model yang sudah "berpendidikan umum" agar menjadi ahli dalam tugas tertentu, seperti analisis sentimen hukum, koding Python, atau menulis puisi Jawa.

## Kurikulum Pelatihan: Metode Fine Tuning

Tidak semua sekolah spesialis sama. Ada yang menuntut perombakan total, ada yang hanya memberikan modul tambahan, dan ada yang fokus pada etika.

### 1. Full Fine-Tuning (Sekolah Ulang)
Ini adalah metode "brute force". Kita memperbarui *semua* parameter di otak si dokter.
*   **Analogi**: Dokter tersebut disuruh belajar ulang dari semester 1, tapi kali ini semua materi dikaitkan dengan bedah saraf.
*   **Resiko**: **Catastrophic Forgetting**. Saking fokusnya belajar bedah saraf, ia mungkin lupa cara mengobati flu ringan atau lupa etika dasar kedokteran [[Overfitting]].
*   **Biaya**: Sangat mahal. Butuh "uang kuliah" (komputasi/GPU) yang sangat besar.

### 2. PEFT (Parameter-Efficient Fine-Tuning) - Modul Tambahan
Alih-alih mengubah seluruh otak dokter, kita membekukan pengetahuan lamanya (agar tidak hilang) dan hanya melatih bagian kecil baru.

#### LoRA (Low-Rank Adaptation)
Ini adalah teknik paling populer saat ini.
*   **Analogi**: Alih-alih mengoperasi otak dokter, kita memberinya sebuah **Buku Saku Spesialis** yang sangat tipis namun padat. Dokter tetap menggunakan otak lamanya untuk pengetahuan umum, tapi setiap kali menghadapi kasus spesifik, ia merujuk pada buku saku ini.
*   **Mekanisme**: Kita menyisipkan matriks kecil (low-rank matrices) ke dalam lapisan [[Transformer Architecture|Transformer]] yang sudah ada. Hanya matriks kecil ini yang dilatih.
*   **Keuntungan**: "Buku saku" ini sangat kecil (hanya beberapa MB), bisa ditukar-tukar. Hari ini bawa buku saku "Hukum", besok bawa buku saku "Koding".

#### QLoRA (Quantized LoRA)
*   **Analogi**: Buku saku yang ditulis dengan singkatan super padat (misalnya menggunakan kode stenografi) sehingga ukurannya jauh lebih kecil lagi, memungkinkan dokter belajar di ruangan yang sempit (GPU dengan VRAM kecil).

## Tahapan Lanjut: Etika dan Instruksi

Selain spesialisasi teknis, dokter juga perlu dilatih cara berinteraksi.

### Instruction Tuning (Pelatihan Bedside Manner)
Pre-trained model seringkali hanya bisa "melanjutkan kalimat". Instruction Tuning mengajarkan model untuk **mengikuti perintah**.
*   **Analogi**: Melatih dokter untuk menjawab dengan format yang benar. Jika pasien bertanya "Apa obat sakit kepala?", dokter tidak boleh meracau sejarah aspirin, tapi harus menjawab lugas: "Parasetamol atau Ibuprofen".
*   **Tujuan**: Mengubah model dari "Penyelesai Teks" menjadi "Asisten yang Patuh".

### RLHF (Reinforcement Learning from Human Feedback) - Dewan Etik
Ini adalah tahap akhir yang krusial untuk keamanan dan kenyamanan.
*   **Analogi**: Dokter diawasi oleh **Dewan Etik Senior**. Setiap kali dokter memberikan resep yang berbahaya (misal: racun) atau bersikap kasar, Dewan Etik memberikan nilai buruk (hukuman). Jika dokter bersikap sopan dan aman, ia diberi pujian (reward). Lama kelamaan, dokter belajar untuk tidak hanya pintar, tapi juga **bijak dan aman**.
*   **Peran**: Menyelaraskan (*align*) jawaban model dengan nilai-nilai manusia (tidak rasis, tidak bias, tidak berbahaya).

## Fine Tuning vs. RAG: Hafalan vs. Mencontek

Seringkali orang bingung membedakan Fine Tuning dengan [[RAG]] (Retrieval-Augmented Generation).

| Konsep | Fine Tuning (Spesialis) | RAG (Perpustakaan) |
| :--- | :--- | :--- |
| **Analogi** | Dokter menghafal materi spesialis di kepalanya. | Dokter membawa buku referensi saat memeriksa pasien. |
| **Kekuatan** | Mengubah *perilaku* dan gaya bicara. | Menambah *pengetahuan* faktual terbaru. |
| **Update Data** | Sulit (harus training ulang). | Mudah (ganti isi buku perpustakaan). |
| **Halusinasi** | Masih mungkin terjadi (salah ingat). | Lebih rendah (ada sumber rujukan). |
| **Kapan Dipakai?** | Saat ingin model bicara gaya "Shakespeare" atau koding gaya "Google". | Saat butuh data real-time (harga saham, berita hari ini). |

## Peta Proses Pembelajaran

Berikut adalah alur transformasi lengkap dari Dokter Umum menjadi Dokter Spesialis yang Etis.

```mermaid
graph LR
    A[Pre-trained Model<br/>(Dokter Umum)] --> B{Instruction Tuning<br/>(Bedside Manner)}
    B --> C[SFT Model<br/>(Asisten Patuh)]
    C --> D{RLHF / DPO<br/>(Sidang Etik)}
    D --> E[Chat Model Final<br/>(Dokter Spesialis Bijak)]
    
    style A fill:#f9f,stroke:#333
    style E fill:#9f9,stroke:#333
```

**Penjelasan Diagram:**
Proses dimulai dari Model Mentah (A) yang hanya bisa memprediksi kata. Melalui Instruction Tuning (B), ia belajar format tanya-jawab. Terakhir, melalui RLHF (D), ia diselaraskan agar aman dan sesuai preferensi manusia, menghasilkan model final (E) yang kita gunakan sehari-hari seperti ChatGPT.

## Refleksi: Menjaga Keseimbangan

Dalam perjalanan menjadi spesialis, tantangan terbesarnya bukan pada mempelajari hal baru, tetapi pada **mempertahankan kebijaksanaan lama**. Sebuah model yang di-finetune terlalu agresif mungkin menjadi sangat hebat dalam menjawab pertanyaan medis, tetapi kehilangan kemampuan berbahasa yang luwes atau menjadi kasar (kehilangan *alignment*).

Sama seperti dokter spesialis bedah jantung yang hebat, ia tetap harus ingat bahwa pasiennya adalah manusia utuh, bukan sekadar kumpulan katup dan arteri. Fine tuning yang berhasil adalah yang menambahkan keahlian tanpa menghapus jati diri.
