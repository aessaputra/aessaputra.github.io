---
title: Panduan Menggunakan DeepWiki
categories:
  - "[[Posts]]"
tags:
  - posts
  - deepwiki
  - github
  - documentation
  - ai-tools
author:
  - "[[Aes Saputra]]"
created: 2025-12-15
published: true
date: 2025-12-15
topics:
  - development-tools
  - github-exploration
status: published
feed: show
---
DeepWiki adalah tool yang memungkinkan Anda mengeksplorasi dan memahami repository GitHub dengan mudah melalui dokumentasi yang dihasilkan AI.

## Fungsi Utama

### 1. `mcp_deepwiki_read_wiki_structure`

**Tujuan:** Melihat daftar topik dokumentasi yang tersedia

**Syntax:**
```
mcp_deepwiki_read_wiki_structure <owner/repo>
```

**Contoh:**
```
mcp_deepwiki_read_wiki_structure facebook/react
mcp_deepwiki_read_wiki_structure vercel/next.js
mcp_deepwiki_read_wiki_structure microsoft/vscode
```

**Kapan digunakan:**
- Eksplorasi awal repository
- Memahami struktur dan cakupan dokumentasi
- Mencari topik spesifik yang tersedia

### 2. `mcp_deepwiki_read_wiki_contents`

**Tujuan:** Membaca isi dokumentasi lengkap repository

**Syntax:**
```
mcp_deepwiki_read_wiki_contents <owner/repo>
```

**Contoh:**
```
mcp_deepwiki_read_wiki_contents facebook/react
mcp_deepwiki_read_wiki_contents tailwindlabs/tailwindcss
```

**Kapan digunakan:**
- Ingin memahami arsitektur keseluruhan
- Pembelajaran mendalam tentang project
- Referensi komprehensif

**⚠️ Catatan:** Bisa menghasilkan output yang sangat panjang untuk repository besar.

### 3. `mcp_deepwiki_ask_question`

**Tujuan:** Bertanya pertanyaan spesifik tentang repository

**Syntax:**
```
mcp_deepwiki_ask_question <owner/repo> "pertanyaan Anda"
```

**Contoh:**
```
mcp_deepwiki_ask_question facebook/react "How does the reconciliation algorithm work?"
mcp_deepwiki_ask_question vercel/next.js "What are the differences between SSR and SSG?"
mcp_deepwiki_ask_question microsoft/typescript "How to configure strict mode?"
```

**Kapan digunakan:**
- Pertanyaan teknis spesifik
- Troubleshooting
- Best practices
- Implementasi fitur tertentu

## Workflow yang Direkomendasikan

### Untuk Eksplorasi Repository Baru

1. **Mulai dengan struktur:**
   ```
   mcp_deepwiki_read_wiki_structure <owner/repo>
   ```

2. **Identifikasi topik yang menarik**

3. **Tanya pertanyaan spesifik:**
   ```
   mcp_deepwiki_ask_question <owner/repo> "pertanyaan berdasarkan topik"
   ```

### Untuk Pertanyaan Teknis Langsung

Langsung gunakan `ask_question` jika sudah tahu apa yang dicari:
```
mcp_deepwiki_ask_question <owner/repo> "pertanyaan spesifik"
```

### Untuk Pembelajaran Mendalam

1. Baca struktur untuk overview
2. Baca konten lengkap untuk pemahaman komprehensif
3. Tanya pertanyaan follow-up untuk klarifikasi

## Tips Penggunaan

### ✅ Do's

- Gunakan nama repository yang tepat (owner/repo)
- Mulai dengan pertanyaan spesifik untuk efisiensi
- Manfaatkan `ask_question` untuk troubleshooting
- Eksplorasi struktur dulu untuk repository yang belum familiar

### ❌ Don'ts

- Jangan langsung baca konten lengkap untuk repo besar tanpa tujuan jelas
- Jangan gunakan nama repository yang salah
- Jangan ragu bertanya pertanyaan follow-up

## Contoh Kasus Penggunaan

### Mempelajari Framework Baru

```bash
# 1. Lihat struktur
mcp_deepwiki_read_wiki_structure sveltejs/svelte

# 2. Tanya konsep dasar
mcp_deepwiki_ask_question sveltejs/svelte "What are the core concepts of Svelte?"

# 3. Tanya implementasi
mcp_deepwiki_ask_question sveltejs/svelte "How to handle state management in Svelte?"
```

### Debugging Issue

```bash
# Langsung tanya masalah spesifik
mcp_deepwiki_ask_question facebook/react "Why am I getting 'Cannot read property of undefined' in useEffect?"
```

### Memahami Arsitektur

```bash
# 1. Struktur untuk overview
mcp_deepwiki_read_wiki_structure kubernetes/kubernetes

# 2. Pertanyaan arsitektur
mcp_deepwiki_ask_question kubernetes/kubernetes "How does the controller pattern work in Kubernetes?"
```

## Repository Populer untuk Dicoba

- `facebook/react` - React library
- `vercel/next.js` - Next.js framework
- `microsoft/vscode` - VS Code editor
- `microsoft/typescript` - TypeScript language
- `tailwindlabs/tailwindcss` - Tailwind CSS
- `sveltejs/svelte` - Svelte framework
- `vuejs/vue` - Vue.js framework
- `angular/angular` - Angular framework
- `kubernetes/kubernetes` - Kubernetes orchestration
- `docker/docker` - Docker containerization

---

**Pro Tip:** DeepWiki paling efektif ketika Anda mengajukan pertanyaan spesifik. Jangan ragu untuk bertanya apa saja tentang repository yang Anda eksplorasi!