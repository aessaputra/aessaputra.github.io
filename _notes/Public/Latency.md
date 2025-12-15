---
title: Latency - Waktu Perjalanan Digital
categories:
  - "[[Posts]]"
tags:
  - performance
  - networking
  - system-optimization
  - user-experience
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

## Pengantar: Waktu Tempuh dalam Perjalanan Digital

Bayangkan Latency sebagai **waktu tempuh perjalanan** dari rumah ke kantor - semakin lama perjalanan, semakin terlambat Anda sampai dan semakin frustrasi yang dirasakan. Dalam dunia digital, latency adalah delay antara saat request dikirim hingga response diterima, dan seperti kemacetan lalu lintas, latency tinggi dapat membuat user experience menjadi sangat buruk.

Latency adalah measurement waktu yang dibutuhkan untuk data melakukan round-trip dari source ke destination dan kembali lagi. Ini berbeda dengan bandwidth (kapasitas jalan) - Anda bisa memiliki jalan tol 8 jalur (high bandwidth) tapi tetap macet karena jarak yang jauh (high latency).

**Mengapa Latency Critical untuk User Experience?**
- **Perceived Performance**: User merasakan aplikasi sebagai "lambat" meskipun throughput tinggi
- **Interactive Applications**: Real-time apps seperti gaming dan video calls sangat sensitif terhadap latency
- **Compound Effect**: Latency terakumulasi di setiap layer dalam distributed systems
- **Business Impact**: 100ms additional latency dapat mengurangi conversion rate hingga 1%