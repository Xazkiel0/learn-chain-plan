## 8.1 Tujuan File Ini

File ini mendokumentasikan **pilihan teknologi utama**, **alasan rasional di baliknya**, serta **trade-off yang disadari sejak awal**.

Tujuan utamanya:

- Mencegah **gonta-ganti stack tanpa alasan kuat**
    
- Menjadi **referensi tunggal** saat diskusi teknis
    
- Memberi konteks bagi developer baru atau auditor teknis
    
- Memastikan stack **selaras dengan problem domain Web3 + EdTech + Crowdfunding**
    
- Menjawab tantangan **Akses Finansial, Monetisasi Adil, dan Trust** (sesuai Deskripsi Proyek)
    

File ini **bukan** daftar teknologi acak, melainkan hasil kompromi antara:

- Kebutuhan bisnis
    
- Kematangan ekosistem
    
- Risiko teknis
    
- Kecepatan MVP
    

---

## 8.2 Prinsip Pemilihan Teknologi

Semua keputusan stack mengikuti prinsip berikut:

1. **MVP-first**
    
    - Prioritas kecepatan validasi, bukan arsitektur sempurna.
        
2. **Battle-tested**
    
    - Menghindari teknologi terlalu baru untuk core system.
        
3. **Composable**
    
    - Mudah diganti sebagian tanpa rewrite total.
        
4. **Web3-aligned**
    
    - Native support untuk wallet, smart contract, dan event-based system.
        
5. **Cost-aware**
    
    - Gas cost, infra cost, dan operational cost dipertimbangkan.
        
6. **User-Centric Trust (Web2.5)**
    
    - Menggabungkan **UX Web2** (cepat, familiar) dengan **Trust Web3** (transparan, non-custodial).
        

---

## 8.3 High-Level Tech Stack Summary

|Layer|Teknologi Utama|
|---|---|
|Frontend|Next.js + React|
|Styling/UI|Tailwind CSS|
|Wallet & Web3 UI|wagmi + viem|
|Backend API|Node.js (NestJS / Express)|
|Database|PostgreSQL|
|ORM|Prisma|
|Auth (Web2)|JWT + OAuth (optional)|
|Blockchain|EVM-compatible chain|
|Smart Contract|Solidity|
|Storage (File)|IPFS (via pinning service)|
|Infra|Docker + Cloud VM|
|Monitoring|Basic logging + metrics|

---

## 8.4 Frontend Stack

### 8.4.1 Next.js (React)

**Alasan:**

- Industry standard untuk Web3 frontend
    
- SSR/SSG mendukung SEO untuk halaman course
    
- Routing & API integration matang
    
- Komunitas besar dan dokumentasi stabil
    

**Trade-off:**

- Lebih kompleks dibanding SPA murni
    
- Butuh disiplin struktur folder
    

**Kenapa bukan alternatif lain:**

- Vue / Svelte: lebih ringan, tapi ekosistem Web3 lebih kecil
    
- Pure React SPA: SEO dan initial load lebih buruk
    

---

### 8.4.2 Tailwind CSS

**Alasan:**

- Cepat untuk MVP
    
- Konsistensi UI mudah dijaga
    
- Minim CSS debt
    

**Trade-off:**

- HTML jadi lebih verbose
    
- Butuh konvensi internal agar tetap readable
    

---

### 8.4.3 Web3 Frontend Libraries (wagmi + viem)

**Alasan:**

- Standar modern Web3 frontend
    
- Type-safe
    
- Integrasi wallet stabil (MetaMask, WalletConnect)
    

**Trade-off:**

- Learning curve bagi developer non-Web3
    
- Breaking change antar versi harus diawasi
    

---

## 8.5 Backend Stack

### 8.5.1 Node.js Backend (NestJS / Express)

**Alasan:**

- Satu bahasa dengan frontend (JavaScript/TypeScript)
    
- Cocok untuk event-driven & API-heavy system
    
- Mudah integrasi dengan blockchain indexer
    
- Mendukung **Role-Based Access Control (RBAC)** ketat untuk 4 role: Guest, Student, Teacher, Admin.
    

**NestJS (disarankan jika tim >1):**

- Struktur jelas
    
- Dependency Injection
    
- Cocok untuk scaling tim
    

**Express (opsi MVP kecil):**

- Lebih ringan
    
- Setup cepat
    

**Trade-off:**

- Node bukan yang tercepat untuk CPU-heavy task
    
- Perlu manajemen async yang baik
    

---

### 8.5.2 Database: PostgreSQL

**Alasan:**

- Relational data cocok untuk:
    
    - User
        
    - Course
        
    - Enrollment
        
    - Funding record
        
- ACID compliance penting untuk financial logic
    
- Mudah di-query untuk reporting
    
- State Machine Management:
    
    - Campaign (`pending` → `target_reached` → `executed`)
        
    - Course (`draft` → `open` → `closed`)
        

**Trade-off:**

- Schema harus dirancang matang
    
- Kurang fleksibel dibanding NoSQL untuk data tak terstruktur
    

**Kenapa bukan NoSQL:**

- Relasi antar entitas kuat
    
- Query kompleks lebih aman di SQL
    

---

### 8.5.3 ORM: Prisma

**Alasan:**

- Type-safe
    
- Schema sebagai single source of truth
    
- Migration jelas dan terkontrol
    

**Trade-off:**

- Query kompleks kadang perlu raw SQL
    
- Overhead abstraction kecil tapi ada
    

---

### 8.5.4 Authentication Strategy

**Hybrid Auth:**

- **Web2 Auth (JWT):** Untuk session management dan akses data off-chain.
    
- **Wallet Signature (SIWE):** Untuk memverifikasi kepemilikan address saat transaksi sensitif.
    
- **Linkage:** User ID terikat dengan Wallet Address (1-to-1 relationship untuk User, optional untuk Guest).
    

---

## 8.6 Blockchain Stack

### 8.6.1 EVM-Compatible Blockchain

**Karakteristik yang diharapkan:**

- Low gas fee
    
- Finality cepat
    
- Kompatibel dengan tooling Solidity
    

**Contoh (tidak mengikat):**

- Polygon
    
- Arbitrum
    
- Optimism
    
- Testnet EVM untuk MVP
    

**Alasan EVM:**

- Ekosistem paling matang
    
- Developer pool besar
    
- Tooling lengkap (Hardhat, Foundry)
    

**Trade-off:**

- Gas fee tetap ada
    
- UX Web3 lebih kompleks dibanding Web2
    

---

### 8.6.2 Smart Contract: Solidity

**Alasan:**

- Standar industri
    
- Audit tools tersedia
    
- Kompatibel dengan EVM chain
    

**Scope smart contract (dibatasi):**

- Course funding
    
- Enrollment proof
    
- Fund distribution (Splitter: 99% Teacher, 1% Platform)
    
- Event emission
    
- **Vault System**: Escrow aman untuk dana crowdfunding sebelum target tercapai.
    

**Non-goal:**

- Jangan taruh logic kompleks di on-chain
    

---

## 8.7 Storage & Media

### 8.7.1 IPFS (via Pinning Service)

**Use case:**

- Course metadata
    
- Sertifikat
    
- Asset statis non-sensitive
    
- **Immutable Proof**: Metadata sertifikat yang di-hash ke blockchain.
    

**Alasan:**

- Content-addressed
    
- Web3-native
    
- Mengurangi ketergantungan server
    

**Trade-off:**

- Akses lebih lambat
    
- Perlu pinning agar data persisten
    

---

## 8.8 Infrastructure & Deployment

### 8.8.1 Docker

**Alasan:**

- Konsistensi environment
    
- Mudah deploy ke mana saja
    
- Mendukung CI/CD
    

---

### 8.8.2 Cloud VM / Managed Hosting

**Karakteristik:**

- Environment terpisah (dev / prod)
    
- Scalable secara horizontal
    

**Trade-off:**

- Perlu basic DevOps skill
    
- Cost harus dipantau
    

---

## 8.9 Monitoring & Logging

**Scope MVP (minimal):**

- Error logging backend
    
- Basic request metrics
    
- Smart contract event monitoring
    

**Non-goal MVP:**

- Full APM
    
- Advanced observability
    

---

## 8.10 Disadari Sejak Awal (Explicit Trade-offs)

1. **UX Web3 tidak sehalus Web2**  
    → Diterima karena target user Web3-aware.
    
2. **On-chain cost selalu ada**  
    → Mitigasi dengan off-chain logic.
    
3. **Stack ini bukan yang paling murah**  
    → Tapi paling stabil untuk long-term.
    
4. **Tidak semua data di blockchain**  
    → Blockchain hanya untuk trust-critical data.
    

---

## 8.11 Prinsip Anti-Gonta-Ganti Teknologi

Perubahan stack **hanya boleh dilakukan jika**:

1. Ada bottleneck terukur
    
2. Ada risiko keamanan nyata
    
3. Ada kebutuhan bisnis baru
    
4. Ada benefit signifikan yang tidak bisa dicapai dengan stack saat ini
    

Semua perubahan **harus terdokumentasi**.
