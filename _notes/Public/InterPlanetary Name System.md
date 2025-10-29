---
title: 'InterPlanetary Name System'
feed: 'show'
date: 2025-10-28
author:
  - '[[Aes Saputra]]'
themes:
  - '[[Decentralization]]'
  - '[[Distributed System]]'
  - '[[IPFS]]'
tags:
  - ipfs
  - ipns
  - decentralized
  - distributed-system
  - cryptography
rating: 6
categories:
  - '[[Personal Notes]]'
---

IPNS adalah sistem di dalam ekosistem [[InterPlanetary File System|IPFS]] yang memungkinkan pembuatan alamat mutable (nama tetap) yang dapat menunjuk ke konten IPFS (CID) yang dapat sering diperbarui. Ideal untuk use-case seperti situs web dinamis, blog, aplikasi yang terus diperbarui.

## Konsep Utama

- IPFS menggunakan [[CID]] (immutable).
- IPNS memungkinkan "pointer => content" yang bisa diperbarui tanpa mengganti alamat pointer.
- Nama IPNS dibentuk dari hash [[public key]] ([[key pair]]).
- Record IPNS memuat [[path target]], [[sequence number]], [[validitas/lifetime]], [[signature]].
- Nama bersifat [[self-certifying]] (verifikasi harusnya bisa dilakukan secara terdesentralisasi).

## Mekanisme

### Publikasi & Resolusi

- **Publikasi (update)**: buat record baru → sign → publish.
- **Resolusi**: nama → jaringan ([[DHT]] atau [[PubSub]]) → record → path → konten.

### Transport Mechanism

- [[DHT]]: konsistensi lebih tinggi, latency bisa lebih besar, perlu republish berkala.
- [[PubSub]]: kecepatan lebih tinggi, ketersediaan lebih baik, tapi overhead koneksi/subscription.

### Trade-off: Konsistensi vs Ketersediaan

- Pengaturan yang relevan: [[validity]] (lifetime), [[TTL caching]], [[transport mechanism]].
- Praktis: bisa diakses lewat gateway IPFS (`/ipns/…` atau subdomain `*.ipns.dweb.link`).
- Alternatif: [[DNSLink]], solusi berbasis [[blockchain]].

## Catatan Konfigurasi / Tips

- Jika Anda memperbarui nama sering → gunakan [[lifetime]] pendek + [[TTL]] rendah agar perubahan cepat tersedia.
- Jika alamat jarang berubah → [[lifetime]] panjang lebih efisien (kurang beban republish).
- Perhatikan cache di gateway/relay → kadang bisa menyebabkan konten lama muncul walau record sudah terupdate.
- Jika menggunakan [[PubSub]]: pantau jumlah subscriptions agar tidak melewati limit dan membebani peer.
- Untuk produksi: pertimbangkan penggunaan nama yang mudah (via [[DNSLink]]) yang menunjuk ke IPNS di belakangnya agar UX lebih baik.
- Jika menyediakan layanan via gateway publik → pahami bahwa pengguna mempercayai gateway (trusted). Untuk verifikasi penuh → resolver harus melakukan verifikasi record signature sendiri.

## Kaitannya dengan Workflows/Metrik

- Nama IPNS bisa diintegrasikan ke alur [[CI/CD]]: setiap deploy situs IPFS → update CID → publish IPNS.
- Dalam [[PKM]] atau sistem file terdistribusi: bisa gunakan IPNS untuk "pointer" ke versi terbaru vault/backup Anda.
- Jika Anda punya banyak versi atau branches dari konten → bisa gen key IPNS tersendiri tiap branch (via `ipfs key gen`) agar fleksibel.

## Terminologi Penting

- [[CID]]: immutable content identifier.
- [[IPNS name]]: nama mutabel berbasis key-pair.
- [[Sequence number]]: versi record, semakin besar = lebih baru.
- [[Validity/lifetime]]: jangka waktu record dianggap valid.
- [[TTL]]: waktu caching record di resolver/gateway.
- [[DHT]]: Distributed Hash Table, transport dasar.
- [[PubSub]]: publish/subscribe overlay untuk update lebih cepat.
- [[DNSLink]]: alternatif untuk nama manusiawi yang menunjuk ke IPFS/IPNS.

## Hubungan dengan Konsep Lain

- [[InterPlanetary File System|IPFS]]: Fondasi teknis dari IPNS.
- [[Decentralized web]]: Konteks penggunaan IPNS dalam web terdesentralisasi.
- [[Cryptography in distributed systems]]: Dasar dari mekanisme keamanan IPNS.
- [[Content addressing vs name addressing]]: Perbedaan fundamental antara CID dan IPNS.

## Refleksi

IPNS menunjukkan bagaimana sistem terdesentralisasi bisa mengatasi tantangan mutability dalam jaringan yang didesain untuk immutability. Konsep "pointer yang bisa berubah" ini mengingatkan pada prinsip [[file over app]] — di mana kita butuh cara untuk merujuk ke konten tanpa kehilangan kemampuan untuk memperbarui.

Dalam konteks [[knowledge-synthesis]], IPNS bisa menjadi metafora untuk bagaimana kita menghubungkan ide-ide yang terus berkembang dalam vault kita, sambil mempertahankan integritas dan kemudahan akses.
