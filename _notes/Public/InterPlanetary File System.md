---
title: InterPlanetary File System
aliases:
  - IPFS
  - InterPlanetary File System
  - Distributed File System
  - P2P File System
  - Decentralized Storage
feed: show
date: 2025-10-28
author:
  - "[[Aes Saputra]]"
themes:
  - "[[Decentralization]]"
  - "[[Peer to Peer]]"
  - "[[Distributed System]]"
tags:
  - ipfs
  - file-sharing
  - web3
  - blockchain
rating: 6
categories:
  - "[[Posts]]"
---
IPFS adalah protokol, hipermedia, dan jaringan peer-to-peer untuk berbagi data menggunakan tabel hash terdistribusi untuk menyimpan informasi penyedia. Melalui penomoran konten, IPFS mengidentifikasi setiap file dalam namespace global yang menghubungkan host IPFS, menciptakan sistem terdistribusi untuk penyimpanan dan berbagi file.

## Prinsip Dasar

IPFS memungkinkan pengguna untuk meng-host dan menerima konten dengan cara mirip BitTorrent. Berbeda dengan server terpusat, IPFS dibangun di sekitar sistem terdistribusi dari operator pengguna yang menyimpan sebagian data keseluruhan. Setiap pengguna dalam jaringan dapat melayani file berdasarkan alamat kontennya, dan peer lain dapat menemukan dan meminta konten tersebut dari node mana pun yang memilikinya menggunakan tabel hash terdistribusi (DHT).

### Perbedaan dengan Protokol Tradisional

Berbeda dengan protokol berbasis lokasi seperti HTTP dan HTTPS, IPFS menggunakan penomoran berbasis konten untuk menyediakan alternatif terdesentralisasi dalam mendistribusikan World Wide Web.

## Fitur Utama

- **Penyimpanan file berbasis konten**: Setiap file diidentifikasi secara unik berdasarkan hash kontennya, memastikan integritas data dan memfasilitasi pengambilan yang efisien.
- **Arsitektur peer-to-peer**: Jaringan node terdistribusi memfasilitasi berbagi file langsung tanpa memerlukan server terpusat.
- **Sistem file berbasis versi**: Mendukung pengelolaan versi file dan memungkinkan pengguna untuk melacak perubahan seiring waktu.
- **Interoperabilitas dengan aplikasi terdistribusi**: IPFS terintegrasi dengan aplikasi terdistribusi (dApps), menawarkan lapisan penyimpanan yang kuat untuk ekosistem blockchain dan Web3.

## Sejarah

IPFS dibuat oleh Juan Benet, yang kemudian mendirikan Protocol Labs pada Mei 2014. Versi alpha diluncurkan pada Februari 2015, dan pada Oktober tahun yang sama dijelaskan oleh TechCrunch sebagai "cepat menyebar dari mulut ke mulut". Penyedia layanan jaringan Cloudflare mulai menggunakan IPFS pada 2018 dan meluncurkan gatewaynya sendiri pada sistem pada 2022.

## Aplikasi

- **Filecoin**: Penyimpanan cloud berbasis IPFS, juga dikembangkan oleh Protocol Labs.
- **Perpustakaan bayangan**: Anna's Archive dan Library Genesis meng-host buku melalui IPFS.
- **Browser Brave**: Menambahkan dukungan pada 2021, meskipun dukungan untuk node lokal dan skema ipfs:// dihapus pada 2024 karena penggunaan rendah dan kurangnya dukungan.

## Penggunaan Anti-Sensor

IPFS telah digunakan untuk menciptakan cermin konten yang dapat diakses meskipun diblokir:

- **Referendum kemerdekaan Katala**: Situs web terkait dicerminkan di IPFS untuk menghindari pemblokiran.
- **Pemblokiran Wikipedia di Turki**: IPFS digunakan untuk membuat cermin Wikipedia, memungkinkan akses ke konten Wikipedia statis yang diarsipkan meskipun dilarang.

## Keamanan

- **Phishing**: Serangan phishing telah didistribusikan melalui gateway IPFS Cloudflare se Juli 2018.
- **Botnet IPStorm**: Botnet yang terdeteksi pertama kali pada Juni 2019 menggunakan IPFS untuk menyembunyikan command-and-controlnya di antara aliran data yang sah di jaringan IPFS.

## Hubungan dengan Konsep Lain

- [File over app](app://obsidian.md/File%20over%20app): IPFS mewakili filosofi "file over app" dengan menyediakan sistem terdistribusi yang tidak bergantung pada server terpusat.
- [Decentralization](app://obsidian.md/Decentralization): IPFS adalah contoh konkret dari desentralisasi dalam teknologi informasi.
- [Web3](app://obsidian.md/Web3): IPFS sering digunakan sebagai lapisan penyimpanan untuk aplikasi Web3 dan blockchain.

> "IPFS bukan hanya teknologi —  
> tapi cara baru berpikir tentang bagaimana data harus hidup dan berbagi."
