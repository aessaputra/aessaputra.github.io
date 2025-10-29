---
title: 'Filebase'
feed: 'show'
date: 2025-10-28
categories:
  - '[[Personal Notes]]'
author:
  - '[[Aes Saputra]]'
themes:
  - '[[Decentralization]]'
  - '[[File Hosting]]'
  - '[[IPFS]]'
tags:
  - personal
  - ipfs
  - file-hosting
  - decentralized
  - filebase
rating: 6
---

**Solusi Lengkap Buat:**

- Hosting file di [[Publish/_notes/Public/InterPlanetary File System|IPFS]] dengan performa enterprise
- Bikin dedicated gateway kenceng
- Manage versi konten pakai [[Publish/_notes/Public/InterPlanetary Name System|IPNS]]

---

## 📊 Fitur Inti

### 1. IPFS Pinning

IPFS Pinning adalah layanan yang menjaga file tetap tersedia di jaringan IPFS dengan cara "meng-pin" data ke beberapa node secara permanen. Fitur ini memastikan konten tidak akan hilang meskipun aslinya dihapus dari komputer lokal.

- Data di-pin permanen ke multiple node global
- Auto-backup ke berbagai lokasi untuk keandalan
- Support upload via web interface, CLI, maupun SDK

### 2. Dedicated Gateway

Dedicated Gateway memberikan akses cepat ke konten IPFS tanpa perlu menjalankan node sendiri. Ini seperti memiliki CDN pribadi untuk konten decentralization.

- Respon super cepat (~13-19ms) karena infrastruktur bare-metal
- Custom domain (misal: `cdn.projectkamu.com`) untuk branding
- SSL gratis untuk akses HTTPS yang aman

### 3. Dynamic IPNS

IPNS (InterPlanetary Naming System) memungkinkan pembuatan link yang tetap meskipun konten diupdate. Ini seperti URL permanen untuk konten yang sering berubah.

- Bikin link tetap untuk konten sering update
- Auto-update saat konten baru di-upload
- Cocok untuk website/blog yang dinamis

### 4. CDN Bare-Metal

CDN ini berjalan pada infrastruktur fisik (bare-metal) tanpa bergantung pada penyedia cloud tradisional, memberikan kontrol penuh atas performa dan keamanan.

- Jaringan global tanpa third-party untuk privasi maksimal
- Prioritas kecepatan & keamanan melalui infrastruktur sendiri
- Zero-trust architecture untuk proteksi data

---

## 🛠️ Cara Mulai

1. **Buat akun** (gratis 5GB storage)  
   Kunjungi website Filebase dan daftar dengan email. Gratisan ini cukup untuk memulai proyek kecil.
2. **Upload file** lewat dashboard  
   Drag & drop file ke dashboard atau gunakan tombol upload. File akan otomatis di-pin ke jaringan IPFS.
3. **Akses konten** pakai: `https://ipfs.filebase.io/ipfs/<CID>`  
   Setiap upload menghasilkan Content Identifier (CID) unik yang bisa digunakan untuk mengakses file dari mana saja.

---

## 🚀 Project Ideas

### NFT Metadata Hosting

- Simpan metadata NFT di IPFS melalui Filebase
- Gunakan IPNS untuk update metadata tanpa mengubah token ID
- Pastikan permanensi data untuk jangka panjang

### Decentralized Blog/Website

- Host static website di IPFS dengan custom domain
- Gunakan IPNS untuk update konten tanpa perlu migrasi
- Manfaatkan kecepatan gateway untuk performa optimal

### Backup Database Encrypted

- Upload database terenkripsi ke IPFS untuk backup off-chain
- Gunakan versioning untuk tracking perubahan data
- Implementasi recovery system yang terdistribusi

---

## 📈 Pricing

### Free Tier

- 5GB storage
- Cocok untuk percobaan dan proyek kecil

### Pro Plan

- $20/bulan
- 500GB storage + 500GB bandwidth
- Fitur enterprise untuk produksi

---

## 🔥 Dev Tip

Pake `@filebase/sdk` buat integrasi seamless ke Node.js/Next.js:

```javascript
import { ObjectManager } from '@filebase/sdk';

// Upload file sederhana
await ObjectManager.put('catatan.txt', 'Ini konten private Bos!');

// Upload dengan metadata
await ObjectManager.put(
  'data.json',
  JSON.stringify({
    title: 'Proyek Saya',
    version: '1.0.0',
  })
);

// Download file
const content = await ObjectManager.get('data.json');
console.log(content);
```

---

## 🤔 Refleksi

Filebase menunjukkan bagaimana teknologi decentralization seperti IPFS bisa diakses dengan mudah oleh developer biasa. Kecepatan dan kemudahan penggunaannya menjadi faktor penting untuk adopsi massal teknologi blockchain.

> "Decentralization isn't just about removing central authorities — it's about creating resilient systems that can survive even when parts fail."

---

## 📚 Terkait

- [[IPFS Fundamentals]]
- [[Decentralized web infrastructure]]
- [[Enterprise-grade decentralized solutions]]
