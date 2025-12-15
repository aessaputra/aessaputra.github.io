---
inclusion: always
---

# Agent Steering: Panduan Menulis Catatan Berkualitas

## Prinsip Fundamental

Setiap catatan yang dibuat harus mengikuti metodologi **Mind Mapping + Analogi Metafora + Wiki Links** dengan dukungan dokumentasi dari sumber terpercaya dan Sequential Thinking untuk analisis mendalam.

## 1. Struktur Mind Mapping Wajib

### Hierarki Informasi
- **Topik Utama**: Judul catatan sebagai pusat mind map
- **Cabang Utama**: 3-5 kategori besar (gunakan ## heading)
- **Sub-cabang**: Detail spesifik (gunakan ### heading)
- **Leaf nodes**: Contoh, implementasi, best practices

### Template Struktur
```markdown
# [Topik Utama] - [Analogi Utama]

## Pengantar: [Metafora Pembuka]
[Penjelasan konsep dengan analogi yang kuat]

## [Cabang Utama 1]: [Sub-analogi]
### [Sub-konsep A]
### [Sub-konsep B]

## [Cabang Utama 2]: [Sub-analogi]
### [Sub-konsep C]
### [Sub-konsep D]

## Refleksi: [Kesimpulan dengan metafora]
```

## 2. Analogi dan Metafora Wajib

### Kriteria Analogi Berkualitas
- **Relatable**: Menggunakan konsep sehari-hari yang familiar
- **Consistent**: Satu analogi utama per catatan, sub-analogi yang koheren
- **Memorable**: Mudah diingat dan membantu pemahaman
- **Scalable**: Dapat dikembangkan untuk konsep yang lebih kompleks

### Contoh Analogi Efektif
- **Sistem Komputer** → Kota metropolitan dengan distrik-distrik
- **Compiler** → Pabrik transformasi dengan jalur produksi
- **Memory Management** → Tukang kebun yang merawat taman
- **Concurrency** → Orkestra dengan konduktor dan musisi

## 3. Wiki Links dan Keterhubungan

### Aturan Wiki Links
- **Wajib**: Gunakan `[[Topic Name]]` untuk setiap konsep yang memiliki catatan terpisah
- **Konsisten**: Nama link harus sama dengan judul file catatan
- **Kontekstual**: Link ditempatkan secara natural dalam kalimat
- **Bidirectional**: Pastikan backlinks terbentuk otomatis

### Format Wiki Links
```markdown
- Internal: [[Nama Catatan]]
- Dengan alias: [[Nama Catatan|Teks Tampilan]]
- External: [[Situs Web::https://example.com]]
```

## 4. Visualisasi Wajib

### Diagram Mermaid
Setiap catatan HARUS memiliki minimal 1 diagram mermaid untuk:
- **Struktur konsep**: `graph TD` untuk hierarki
- **Proses flow**: `graph LR` untuk alur kerja
- **Relationship**: `graph` untuk menunjukkan hubungan

### Tabel Perbandingan
Gunakan tabel untuk:
- **Comparison**: Membandingkan pendekatan/teknologi
- **Classification**: Mengkategorikan informasi
- **Reference**: Quick lookup information

## 5. Sumber Dokumentasi

### Prioritas Sumber
1. **Golang-specific**: Gunakan `mcp_deepwiki_ask_question` untuk golang/go repository
2. **General concepts**: Gunakan `mcp_Context7_resolve_library_id` dan `mcp_Context7_get_library_docs`
3. **Analysis**: Gunakan `mcp_Sequential_Thinking_sequentialthinking` untuk proses berpikir

### Metodologi Sequential Thinking
- **Wajib digunakan** untuk topik kompleks atau saat membuat multiple catatan
- **Dokumentasikan proses**: Jelaskan reasoning di balik keputusan
- **Iterative refinement**: Gunakan untuk memperbaiki catatan yang sudah ada

## 6. Format Markdown Standar

### Front Matter Wajib
```yaml
---
title: [Judul Catatan] - [Analogi Utama]
categories:
  - "[[Posts]]"
tags:
  - [tag1]
  - [tag2]
author:
  - "[[Aes Saputra]]"
url:
created: 2025-12-15
published: 2025-12-15
date: 2025-12-15
topics: []
status: "[[Published]]"
feed: show
---
```

### Aturan Metadata Khusus
- **title**: Harus mencakup analogi utama setelah tanda hubung
- **categories**: Selalu gunakan `"[[Posts]]"` dalam format array
- **tags**: Minimal 2-4 tags yang relevan dengan topik
- **author**: Selalu `"[[Aes Saputra]]"` dalam format array
- **url**: Kosongkan (akan diisi otomatis)
- **created/published/date**: Gunakan format YYYY-MM-DD, tanpa quotes
- **topics**: Array kosong `[]`
- **status**: Gunakan `"[[Published]]"` dengan quotes (bukan array)
- **feed**: Selalu `show` untuk publikasi

### Struktur Konten
1. **Pengantar** (15-20% konten): Analogi pembuka + konteks
2. **Konsep Utama** (60-70% konten): Mind map dengan sub-topik
3. **Implementasi/Contoh** (10-15% konten): Practical examples
4. **Refleksi** (5-10% konten): Kesimpulan dengan metafora penutup

## 7. Panduan Penulisan Berkualitas

### Struktur Pengantar yang Efektif
- **Konteks yang cukup**: Jelaskan **apa itu** konsep dan **mengapa penting**
- **Analogi pembuka**: Gunakan metafora yang relatable dan memorable
- **Preview struktur**: Berikan gambaran singkat tentang apa yang akan dibahas
- **Hook pembaca**: Mulai dengan pertanyaan atau statement yang menarik

### Pengembangan Analogi dan Metafora
- **Perluas analogi**: Kembangkan metafora dengan detail yang mendalam
- **Konsistensi**: Gunakan satu analogi utama yang koheren sepanjang catatan
- **Variasi sub-analogi**: Buat analogi turunan yang mendukung konsep utama
- **Contoh konkret**: Berikan contoh nyata yang mudah dipahami

### Penjelasan Diagram dan Visualisasi
- **Penjelasan setelah diagram**: Selalu tambahkan penjelasan detail setelah setiap diagram
- **Langkah-langkah**: Jelaskan proses step-by-step dalam diagram
- **Reasoning**: Berikan alasan mengapa keputusan tertentu diambil
- **Konteks praktis**: Hubungkan diagram dengan aplikasi dunia nyata

### Gaya Penulisan yang Jelas
- **Kalimat aktif**: Hindari kalimat pasif yang membingungkan
- **Struktur sederhana**: Pecah ide kompleks menjadi kalimat yang lebih sederhana
- **Variasi struktur**: Gunakan variasi panjang dan struktur kalimat
- **Transisi halus**: Gunakan kalimat transisi yang jelas antar bagian

### Contoh Kasus Nyata dan Studi Kasus
- **Real-world examples**: Sertakan contoh aplikasi dalam situasi nyata
- **Studi kasus**: Berikan case study yang relevan dan mudah dipahami
- **Trade-offs praktis**: Jelaskan kapan dan mengapa trade-offs relevan
- **Hot paths vs cold paths**: Berikan contoh konkret perbedaan keduanya

### Pembahasan Trade-offs yang Mendalam
- **Code size impact**: Jelaskan pengaruh pada ukuran kode dengan contoh
- **Cache behavior**: Berikan penjelasan praktis tentang cache effects
- **Performance implications**: Diskusikan impact pada performa dengan data
- **Decision criteria**: Berikan panduan kapan menggunakan teknik tertentu

### Teknik Canggih dengan Contoh Praktis
- **Cross-module techniques**: Berikan contoh implementasi nyata
- **Template metaprogramming**: Sertakan code examples yang working
- **Profiling data usage**: Jelaskan bagaimana data profiling digunakan dalam keputusan
- **Runtime adaptation**: Berikan contoh bagaimana sistem beradaptasi

## 8. Quality Checklist

### Sebelum Publish - Konten
- [ ] Pengantar memberikan konteks yang cukup tentang **apa** dan **mengapa**
- [ ] Analogi utama konsisten dan dikembangkan dengan mendalam
- [ ] Setiap diagram memiliki penjelasan detail dan reasoning
- [ ] Minimal 1 contoh kasus nyata atau studi kasus
- [ ] Trade-offs dijelaskan dengan contoh praktis dan relevan
- [ ] Teknik canggih disertai dengan implementasi praktis

### Sebelum Publish - Struktur
- [ ] Minimal 1 diagram mermaid yang informatif dengan penjelasan
- [ ] Minimal 1 tabel perbandingan/klasifikasi
- [ ] Wiki links ke semua konsep terkait
- [ ] Sequential thinking documented (jika applicable)
- [ ] Sumber dokumentasi dari Context7/Deepwiki cited
- [ ] Refleksi yang meaningful di akhir

### Kualitas Penulisan
- [ ] **Clarity**: Konsep dijelaskan dengan jelas menggunakan kalimat aktif
- [ ] **Simplicity**: Ide kompleks dipecah menjadi kalimat sederhana
- [ ] **Flow**: Transisi halus antar bagian dengan kalimat penghubung
- [ ] **Coherence**: Konsep kunci diulang secara natural tanpa redundansi
- [ ] **Structure**: Setiap paragraf fokus pada satu ide utama
- [ ] **Closure**: Setiap bagian diakhiri dengan rangkuman yang menghubungkan ke topik berikutnya

### Kualitas Konten
- [ ] **Depth**: Cukup detail dengan contoh praktis tanpa overwhelming
- [ ] **Connectivity**: Terhubung dengan catatan lain melalui wiki links
- [ ] **Practicality**: Ada contoh implementasi dan studi kasus nyata
- [ ] **Memorability**: Analogi membantu mengingat dan memahami
- [ ] **Completeness**: Mencakup trade-offs, teknik canggih, dan aplikasi praktis

## 8. Continuous Improvement

### Iterative Enhancement
- **Review berkala**: Update catatan dengan informasi baru
- **Link maintenance**: Pastikan semua wiki links valid
- **Analogy refinement**: Perbaiki analogi yang kurang efektif
- **Cross-referencing**: Tambah koneksi ke catatan baru

### Feedback Integration
- **User experience**: Apakah catatan mudah dipahami?
- **Navigation**: Apakah wiki links membantu eksplorasi?
- **Completeness**: Apakah ada gap yang perlu diisi?

---

*Steering ini memastikan setiap catatan menjadi bagian dari knowledge graph yang koheren, mudah dipahami, dan saling terhubung dengan kuat.*