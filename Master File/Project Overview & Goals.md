# 1. Project Overview & Goals

## 1.1 Project Overview

Proyek ini adalah **platform pembelajaran berbasis Web3** yang memungkinkan pengajar menyediakan course berbayar, pelajar mengikuti course tersebut, serta pembayaran dan sertifikasi dicatat secara **on-chain tanpa kustodi**.

Platform ini mengadopsi pendekatan **Web2.5 (Hybrid Web2 + Web3)**:

- **Web2** digunakan untuk pengalaman pengguna dan manajemen sistem (autentikasi, manajemen user & course, progress pembelajaran, UI/UX).
    
- **Web3** digunakan secara selektif untuk hal kritikal yang membutuhkan trust layer (alur dana non-kustodial, crowdfunding vault via smart contract, dan pencatatan sertifikat immutable).
    
Sistem dirancang untuk:

- Menghilangkan peran pihak ketiga sebagai pemegang dana (non-custodial)
    
- Memberikan transparansi penuh pada alur pembayaran course
    
- Menyediakan mekanisme **crowdfunding terkontrol** bagi pelajar yang dikategorikan “tidak mampu”
    
- Menghasilkan **sertifikat berbasis blockchain** yang merepresentasikan penyelesaian course
    
- Menjaga pengalaman pengguna tetap sederhana tanpa membebani pengguna dengan kompleksitas blockchain
    
- Menetapkan batasan tegas agar admin tidak memiliki kuasa terhadap dana maupun hasil akademik
    
Catatan model course pada MVP:

- Course dapat bersifat **Paid langsung** (enroll berbayar) atau **Crowdfundable** (khusus untuk pelajar yang ditandai “tidak mampu” oleh admin).
    
### Prinsip Pembayaran Non-Kustodial (Detail)

- Semua pembayaran course dilakukan melalui wallet pengguna, tanpa dana mengendap di platform.
    
- Saat enrollment atau eksekusi crowdfunding:
    
    - **99% dana langsung masuk ke wallet pengajar**
        
    - **1% fee otomatis masuk ke wallet perusahaan**
        
### Sertifikat On-Chain (Bukan NFT Spekulatif)

- Sertifikat direpresentasikan sebagai **hash + metadata yang dicatat on-chain**.
    
- Sertifikat bersifat immutable dan dapat diverifikasi publik.
    
- Sertifikat tidak bersifat spekulatif dan tidak transferable.
    

Platform ini **bukan marketplace NFT spekulatif**, melainkan sistem edukasi dengan pencatatan kriptografis sebagai trust layer.

Target utama proyek adalah **aplikasi web end-to-end** yang mengintegrasikan:

- Web frontend
    
- Backend application
    
- Smart contract sebagai trust & payment layer
    

---

## 1.2 Target Users (Untuk Siapa)

Platform ini ditujukan untuk tiga kelompok utama:

1. **Pengajar independen**
    
    - Ingin menjual course tanpa perantara pembayaran
        
    - Ingin dana langsung masuk ke wallet mereka
        
    - Tidak ingin bergantung pada platform kustodian
        
2. **Pelajar**
    
    - Ingin mengikuti course dengan transparansi biaya
        
    - Memiliki opsi bantuan melalui crowdfunding jika tidak mampu
        
    - Menginginkan bukti kelulusan yang tidak bisa dimanipulasi
        
3. **Platform operator (Admin)**
    
    - Menjaga tata kelola sistem
        
    - Mencegah abuse
        
    - Tanpa kuasa terhadap dana dan hasil akademik
        
Selain tiga kelompok utama di atas, ekosistem sistem juga dapat melibatkan **funder** (pemberi dana crowdfunding) sebagai partisipan finansial yang dapat memverifikasi transparansi campaign secara publik dan menarik dana kembali jika target tidak tercapai.

### Peran (Role) pada MVP

Pada MVP, sistem mengenal 4 role utama:

1. **Guest** (pengunjung publik)
2. **Pelajar (Student)**
3. **Pengajar (Teacher)**
4. **Admin (Platform Operator)**

Catatan penting:

- Semua role (kecuali Guest) adalah user terdaftar yang terhubung wallet.
    
- Guest bersifat read-only, tidak menyentuh dana, dan tidak berinteraksi dengan blockchain.
    
- Sistem tidak mengenal role ganda secara bebas pada MVP (misalnya Teacher ≠ Student), kecuali ditentukan eksplisit pada pengembangan lanjutan.
    

---
## 1.3 Problem Statement



Masalah yang ingin diselesaikan oleh sistem ini:

### 1. Ketergantungan pada pihak kustodian

Platform edukasi tradisional:

- Menyimpan dana user
    
- Menunda pembayaran ke pengajar
    
- Rentan dispute dan manipulasi
    

### 2. Tidak adanya transparansi dana

Pelajar dan pengajar:

- Tidak bisa memverifikasi alur pembayaran
    
- Tidak tahu secara pasti fee dan distribusi dana
    

### 3. Akses pendidikan terbatas bagi pelajar tidak mampu

- Tidak ada mekanisme pendanaan terstruktur
    
- Crowdfunding sering tidak terikat langsung ke kebutuhan nyata (course tertentu)
    
  
Dalam sistem ini, crowdfunding dibuat **terkontrol**: campaign selalu terikat pada **1 pelajar + 1 course**, dan hanya dapat dibuat oleh pelajar yang telah ditetapkan admin sebagai “tidak mampu”.

### 4. Sertifikat mudah dipalsukan



- Sertifikat PDF atau database sentral mudah dimanipulasi
    
- Tidak ada bukti kriptografis atas penyelesaian course
    
---

## 1.4 Goals

### Goal Utama (Primary Goals)

1. **Non-custodial payment**
    
    - Dana enrollment langsung masuk ke wallet pengajar
        
    - Platform hanya mengambil fee yang telah didefinisikan (1%)
        
2. **Crowdfunding terkontrol**
    
    - Campaign hanya bisa dibuat oleh pelajar “tidak mampu”
        
    - Campaign terikat ke satu course spesifik
        
    - Dana disimpan di smart contract vault
        
    - Funder dapat menarik dana kembali jika target tidak tercapai
        
    - Campaign memiliki state yang eksplisit: `pending → target_reached → executed`
        
3. **On-chain certification**
    
    - Sertifikat direpresentasikan sebagai hash + metadata on-chain
        
    - Tidak transferable
        
    - Tidak bersifat spekulatif
        
4. **Minim trust ke admin**
    
    - Admin tidak bisa memanipulasi dana
        
    - Admin tidak bisa memanipulasi hasil akademik
        
5. **Explicit state over implicit logic**
    
    - State utama konsisten antara backend dan smart contract (Course/Campaign/Enrollment)
        

---

## 1.5 Success Criteria (Definisi Keberhasilan)

Sistem dianggap **berhasil** jika:



1. Pelajar bisa:
    
    - Enroll course dengan wallet
        
    - Menyelesaikan course
        
    - Mengklaim sertifikat on-chain
        
2. Pengajar:
    
    - Menerima dana langsung ke wallet
        
    - Tanpa intervensi admin
        
    - Tanpa penundaan off-chain
        
3. Crowdfunding:
    
    - Dana aman di vault
        
    - Bisa ditarik kembali jika target tidak tercapai
        
    - Hanya dieksekusi jika memenuhi kondisi sistem
        
4. Tidak ada:
    
    - Dana platform yang menahan uang user
        
    - Sertifikat yang bisa dicetak tanpa kelulusan sah
        
    - Akses admin terhadap private key atau mekanisme pemindahan dana user
        

---

## 1.6 Definition of “Done” (Definisi Sistem Selesai)


Sistem dianggap **selesai (MVP Done)** jika:

### Secara Fungsional


- Course bisa dibuat, dibuka, dan ditutup
    
- Enrollment dan pembayaran berjalan on-chain
    
- Crowdfunding berjalan dengan 3 state:
    
    - `pending`
        
    - `target_reached`
        
    - `executed`
        
- Sertifikat bisa diklaim setelah:
    
    - Progress 100%
        
    - Final task approved
        
  
- State machine utama terdefinisi jelas:
    
    - Course state: `draft → open → closed`
        
    - Campaign state: `pending → target_reached → executed`
        
    - Enrollment state: `enrolled → in_progress → completed`
        
### Secara Teknis



- Tidak ada custodial wallet
    
- Smart contract menjadi satu-satunya pengendali dana crowdfund
    
- Backend tidak menyimpan private key
    
- Platform tidak memiliki custodial wallet dan tidak memiliki kemampuan admin-override untuk transaksi.
    
  
### Secara Produk
- Fitur di luar MVP (secondary market, NFT trading, dll) **tidak ada**
    

- Platform tidak memiliki custodial wallet dan tidak memiliki kemampuan admin-override untuk transaksi.
---

## 1.7 Scope
    
    

### In Scope (MVP)

- User registration & wallet connection
    
- Course management (teacher)
    
- Enrollment & payment on-chain
    
- Crowdfunding berbasis course
    
- Progress tracking otomatis
    
- Final task approval oleh teacher
    
- Sertifikat on-chain (hash + metadata)
    
- Admin governance terbatas
    

---

### Out of Scope (Explicitly Excluded)

- Transferable NFT certificate
    
- Secondary market
    
- Lending / borrowing
    
- Tokenomics kompleks
    
- DAO governance
    
- Mobile app (native)
    
- KYC atau verifikasi dokumen kompleks
    
- Konversi kripto ke fiat
    
- Course korporat / enterprise
    
- Sistem delegasi pengawas crowdfunding
    
- AI Course Assistant
    
Penegasan out-of-scope ini **wajib** agar tidak terjadi scope creep saat development.

---

## 1.8 Guiding Principles

Sebagai penutup file ini, proyek mengikuti prinsip berikut:



1. **Trust minimization**
    
2. **On-chain untuk hal kritikal, off-chain untuk UX**
    
3. **Explicit state over implicit logic**
    
4. **No admin override terhadap dana & akademik**
    
5. **MVP-first, extensible later**
    
---

## 1.9 Restriction & Allowed Scope (Ringkas)

### Restriction Umum

- Semua transaksi wajib wallet-connected.
    
- Tidak ada custodial wallet.
    
- Tidak ada admin override terhadap dana.
    
- Tidak ada manual progress override.
    
- Campaign tidak bisa dibuat bebas (harus menempel ke Course + Student).
    
### Restriction Pelajar

- Tidak bisa enroll course closed.
    
- Tidak bisa membuat campaign jika tidak ditandai “tidak mampu” atau course tidak crowdfundable.
    
- Tidak bisa klaim sertifikat tanpa progress 100% dan final task approved.
    
### Restriction Pengajar

- Tidak bisa mengubah course setelah closed.
    
- Tidak bisa approve final task sebelum progress 100%.
    
- Tidak bisa menarik dana crowdfund secara manual.
    
### Restriction Admin

- Tidak bisa memicu eksekusi crowdfund.
    
- Tidak bisa mengubah state campaign.
    
- Tidak bisa menyetujui kelulusan pelajar atau mengeluarkan sertifikat.
    
