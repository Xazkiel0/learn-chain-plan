
## 1. Project Overview

Proyek ini adalah **platform pembelajaran berbasis Web3** yang memungkinkan pengajar menyediakan course berbayar, pelajar mengikuti course tersebut, serta pembayaran dan sertifikasi dicatat secara **on-chain tanpa kustodi**.

Sistem dirancang untuk:

- Menghilangkan peran pihak ketiga sebagai pemegang dana (non-custodial)
    
- Memberikan transparansi penuh pada alur pembayaran course
    
- Menyediakan mekanisme **crowdfunding terkontrol** bagi pelajar yang dikategorikan “tidak mampu”
    
- Menghasilkan **sertifikat berbasis blockchain** yang merepresentasikan penyelesaian course
    

Platform ini **bukan marketplace NFT spekulatif**, melainkan sistem edukasi dengan pencatatan kriptografis sebagai trust layer.

Target utama proyek adalah **aplikasi web end-to-end** yang mengintegrasikan:

- Web frontend
    
- Backend application
    
- Smart contract sebagai trust & payment layer
    

---

## 2. Target Users (Untuk Siapa)

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
        

---

## 3. Problem Statement

Masalah yang ingin diselesaikan oleh sistem ini:

### 3.1. Ketergantungan pada pihak kustodian

Platform edukasi tradisional:

- Menyimpan dana user
    
- Menunda pembayaran ke pengajar
    
- Rentan dispute dan manipulasi
    

### 3.2. Tidak adanya transparansi dana

Pelajar dan pengajar:

- Tidak bisa memverifikasi alur pembayaran
    
- Tidak tahu secara pasti fee dan distribusi dana
    

### 3.3. Akses pendidikan terbatas bagi pelajar tidak mampu

- Tidak ada mekanisme pendanaan terstruktur
    
- Crowdfunding sering tidak terikat langsung ke kebutuhan nyata (course tertentu)
    

### 3.4. Sertifikat mudah dipalsukan

- Sertifikat PDF atau database sentral mudah dimanipulasi
    
- Tidak ada bukti kriptografis atas penyelesaian course
    

---

## 4. Goals

### Goal Utama (Primary Goals)

1. **Non-custodial payment**
    
    - Dana enrollment langsung masuk ke wallet pengajar
        
    - Platform hanya mengambil fee yang telah didefinisikan (1%)
        
2. **Crowdfunding terkontrol**
    
    - Campaign hanya bisa dibuat oleh pelajar “tidak mampu”
        
    - Campaign terikat ke satu course spesifik
        
    - Dana disimpan di smart contract vault
        
3. **On-chain certification**
    
    - Sertifikat direpresentasikan sebagai hash + metadata on-chain
        
    - Tidak transferable
        
    - Tidak bersifat spekulatif
        
4. **Minim trust ke admin**
    
    - Admin tidak bisa memanipulasi dana
        
    - Admin tidak bisa memanipulasi hasil akademik
        

---

## 5. Success Criteria (Definisi Keberhasilan)

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
        

---

## 6. Definition of “Done” (Definisi Sistem Selesai)

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
        

### Secara Teknis

- Tidak ada custodial wallet
    
- Smart contract menjadi satu-satunya pengendali dana crowdfund
    
- Backend tidak menyimpan private key
    

### Secara Produk

- Fitur di luar MVP (secondary market, NFT trading, dll) **tidak ada**
    

---

## 7. Scope

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
    

Penegasan out-of-scope ini **wajib** agar tidak terjadi scope creep saat development.

---

## 8. Guiding Principles

Sebagai penutup file ini, proyek mengikuti prinsip berikut:

1. **Trust minimization**
    
2. **On-chain untuk hal kritikal, off-chain untuk UX**
    
3. **Explicit state over implicit logic**
    
4. **No admin override terhadap dana & akademik**
    
5. **MVP-first, extensible later**