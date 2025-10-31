---
categories:
  - "[[Posts]]"
tags:
  - posts
author:
  - "[[Aes Saputra]]"
url: https://writing.aes.my.id/notes/ipfs-fundamentals
created: 2025-10-30
published: 2025-10-30
topics:
  - "[[Decentralization]]"
status:
  - "[[Published]]"
feed: show
title: IPFS Fundamentals
date: 2025-10-30
---
> "The InterPlanetary File System - IPFS - is a peer-to-peer distributed system for storing and accessing files, websites, applications, and data. IPFS is designed to power the Distributed Web - DWeb."

## Web Terpusat vs Web Terdistribusi

Web saat ini sangat terpusat. "Kekuatan" berada di tangan beberapa perusahaan besar. Ini berarti sebagian besar aktivitas kita di web, seperti membuat postingan atau berbagi sesuatu, dimiliki oleh orang lain - perusahaan yang berkuasa.

Web terpusat didorong oleh ekonomi data - pemanfaatan konten yang dibuat pengguna dan digunakan kembali terhadap pengguna itu sendiri.

Web terpusat mengakibatkan kontrol mutlak atas informasi, bagaimana kita melihat informasi, dan eksploitasi melalui pemanfaatan persepsi kita saat ini.

## Cara IPFS Bekerja

Secara tingkat tinggi, IPFS bekerja dengan menemukan informasi yang Anda cari berdasarkan kontennya. Ini dikenal sebagai **content addressing** dan dicapai melalui Content Identifier - CID.

### Tiga Prinsip Fundamental IPFS

1. **Identifikasi unik melalui content addressing**
   
   Perbedaan kunci antara web terpusat dan web terdistribusi adalah identifikasi dan pengambilan data/informasi di masing-masing sistem. Di web terpusat, location addressing melalui URL digunakan untuk mengidentifikasi dan "lokasi" data.
   
   Di sisi lain, web terdistribusi menggunakan content addressing melalui content identifier unik - CID - untuk mengambil data dari berbagai sumber (peer dan/atau node).
   
   Content identifier - CID adalah bentuk khusus content addressing yang dikembangkan untuk IPFS. Ini adalah satu pengidentifikasi yang berisi hash kriptografi dan codec, yang menyimpan informasi tentang cara menafsirkan data.
   
   Content identifier tidak menunjukkan di mana data disimpan. Namun, ini membentuk semacam alamat berdasarkan konten mendasar data.

2. **Penghubung konten melalui Directed Acyclic Graphs (DAGs)**
   
   Data diakses dari peer di web terdistribusi, bukan dari otoritas pusat. Secara tingkat tinggi, grafik adalah abstraksi matematika yang digunakan untuk mewakili hubungan antara kumpulan objek.
   
   - **Directed Graphs**: Grafik dikatakan terarah jika setiap sisi memiliki beberapa arah. Koneksi antar node hanya benar-benar berhubungan dalam satu arah, dan panah kepala tunggal menunjukkan arah ini.
   - **Acyclic Graphs**: Grafik acyclic tidak memiliki loop dalam grafik. Ini berarti tidak ada cara untuk menavigasi dari node kembali ke dirinya sendiri sepanjang sisi grafik.
   - **Directed Acyclic Graphs - DAGs**: Grafik yang terarah dan acyclic disebut, seperti yang Anda tebak? Grafik terarah acyclic - DAG.

3. **Penemuan konten melalui distributed hash tables (DHTs)**
   
   Distributed hash table - DHT adalah sistem terdistribusi untuk memetakan kunci ke nilai. Di IPFS, DHT digunakan sebagai komponen fundamental sistem routing konten dan bertindak seperti silang antara katalog dan sistem navigasi.
   
   DHT memetakan apa yang pengguna cari - CID - ke peer yang benar-benar menyimpan konten yang cocok.
   
   Ada tiga jenis pasangan kunci-nilai yang dipetakan menggunakan DHT:
   
   - Provide records - memetakan pengidentifikasi data ke peer yang telah mengiklankan mereka memiliki konten tersebut dan bersedia menyediakannya untuk Anda.
   - IPNS records - Memetakan kunci IPNS - hash dari kunci publik - ke catatan IPNS.
   - Peer records - memetakan peerID ke setiap alamat multi di mana peer dapat dijangkau.

## Keunggulan IPFS

Dengan menggunakan IPFS untuk mengunduh file dari sistem lain, komputer Anda juga menjadi distributor. Di sinilah salah satu kekuatan menggunakan IPFS sebagai protokol - sistem Anda menjadi bagian dari jaringan terdistribusi, membantu menyebarkan dan mendistribusikan informasi.

## Sumber Belajar Lebih Lanjut

- [ProtoSchool](https://proto.school/)
- [IPFS YouTube Channel](https://www.youtube.com/c/IPFSbot)
- [IPFS docs](https://docs.ipfs.tech/)

---

## Catatan Reflektif

IPFS mewakili pergeseran fundamental dalam cara kita memikirkan penyimpanan dan distribusi data. Dengan memindahkan fokus dari lokasi ke konten, IPFS menciptakan sistem yang lebih tahan terhadap sensor dan kegagalan pusat.

Prinsip content addressing melalui CID menarik karena mengubah cara kita berpikir tentang identitas data - bukan di mana data berada, tetapi apa yang ada di dalamnya yang penting.

DAGs menawarkan cara yang elegan untuk mewakili hubungan kompleks tanpa risiko loop tak terbatas, sementara DHTs memberikan mekanisme praktis untuk menemukan konten di jaringan yang tersebar luas.

---

## Hubungan dengan Konsep Lain

- [[Decentralization]]
- [[Peer-to-peer networks]]
- [[Content addressing]]
- [[Distributed systems]]
- [[Web3 fundamentals]]
