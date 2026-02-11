# 1. Role Users

Terdapat **4 role utama**:

1. **Guest**
    
2. **Student (Pelajar)**
    
3. **Teacher (Pengajar)**
    
4. **Admin**
    

Catatan penting:

- Role bersifat **hierarkis parsial**, bukan linear
    
- Student dan Teacher **extend dari Guest**
    
- Admin **bukan pemilik dana**, hanya pengelola status & moderasi
    

---

# 2. Deskripsi Tiap Role & Kegunaannya

## 2.1 Guest

### Deskripsi

Guest adalah **user publik** (belum login / belum connect wallet) yang berfungsi sebagai **entry point** ke platform.

### Kegunaan

- Memberikan **akses transparansi**
    
- Menurunkan friction onboarding
    
- Meningkatkan trust terhadap course & sistem
    

Guest **tidak berinteraksi dengan blockchain**.

---

## 2.2 Student (Pelajar)

### Deskripsi

Student adalah user yang **belajar course**, berpotensi menjadi **penerima crowdfunding**, dan pihak utama yang menerima manfaat sistem.

Student bisa berada dalam kondisi:

- normal
    
- “tidak mampu” (flag khusus dari Admin)
    

### Kegunaan

- Konsumen course
    
- Beneficiary crowdfunding
    
- Pemilik sertifikat on-chain
    

---

## 2.3 Teacher (Pengajar)

### Deskripsi

Teacher adalah **penyedia course** dan **penerima dana langsung** dari enrollment.

Teacher **tidak mengontrol dana platform**, hanya:

- membuat course
    
- menerima pembayaran sesuai smart contract
    

### Kegunaan

- Menyediakan konten & silabus
    
- Meng-generate value ekonomi platform
    
- Menjadi endpoint pembayaran
    

---

## 2.4 Admin

### Deskripsi

Admin adalah **governance operator**, bukan pemilik sistem secara absolut.

Admin **tidak menyentuh dana**, tidak bisa:

- menarik dana course
    
- menarik dana crowdfund
    
- memodifikasi transaksi blockchain
    

### Kegunaan

- Menjaga integritas sistem
    
- Moderasi user
    
- Validasi kondisi sosial (“tidak mampu”)
    

---

# 3. Kuasa & Ability Tiap Role

## 3.1 Guest

### Ability

- Melihat semua course
    
- Melihat detail course (harga, silabus, status crowdfundable)
    
- Register akun
    
- Login
    
- Connect wallet
    

### Kuasa

- **Read-only**
    
- Tidak punya state on-chain
    
- Tidak memicu smart contract
    

---

## 3.2 Student

### Ability Utama

- Enroll course (direct pay)
    
- Mengikuti progress course
    
- Submit tugas
    
- Menyelesaikan course
    
- Mencetak sertifikat (hash + metadata on-chain)
    

### Ability Crowdfunding

_(hanya jika ditandai “tidak mampu”)_

- Membuat campaign **otomatis** (melekat ke:
    
    - dirinya
        
    - course tertentu)
        
- Menyetujui eksekusi campaign (“fund now”)
    
- Menarik dana jika campaign gagal
    

### Kuasa

- Menginisiasi transaksi pembayaran
    
- Menginisiasi campaign (dengan constraint)
    
- Menjadi signer untuk eksekusi campaign
    

Student **tidak bisa**:

- menentukan target bebas
    
- mengubah logika campaign
    
- memaksa pencairan dana
    

---

## 3.3 Teacher

### Ability

- Membuat course
    
- Mengatur:
    
    - harga course
        
    - silabus
        
    - tugas akhir
        
- Set course:
    
    - crowdfundable / non-crowdfundable
        
    - open / closed
        
- Approve tugas akhir student
    

### Kuasa Finansial

- Menerima dana enrollment **langsung ke wallet**
    
- Menerima dana crowdfund **hanya setelah campaign executed**
    

Teacher **tidak memegang custody** dana sebelum kondisi terpenuhi.

---

## 3.4 Admin

### Ability

- Set student sebagai “tidak mampu”
    
- Ban user
    
- Set user ke inactive
    
- Moderasi data off-chain (profile, metadata)
    

### Kuasa

- Mengubah status user
    
- Menghentikan akses aplikasi
    

Admin **tidak bisa**:

- memodifikasi smart contract state finansial
    
- mengubah hasil transaksi blockchain
    
- mencetak sertifikat
    

---

# 4. Restriction & Allowed Scope (Boundary System)

Bagian ini penting karena **menentukan keamanan & trust model**.

---

## 4.1 Restriction Global

- Semua transaksi keuangan:
    
    - **harus melalui smart contract**
        
    - **non-custodial**
        
- Tidak ada admin override untuk dana
    
- Tidak ada manual settlement
    

---

## 4.2 Restriction per Role

### Guest

❌ Tidak bisa:

- enroll
    
- create campaign
    
- interact on-chain
    

---

### Student

❌ Tidak bisa:

- membuat course
    
- mengubah harga course
    
- membuat campaign bebas
    
- mencetak sertifikat tanpa progress 100%
    

✅ Hanya bisa:

- campaign untuk course tertentu
    
- campaign dengan target = harga course
    

---

### Teacher

❌ Tidak bisa:

- mengedit campaign
    
- menarik dana crowdfund sebelum executed
    
- memaksa student lulus
    

---

### Admin

❌ Tidak bisa:

- menarik dana
    
- memalsukan sertifikat
    
- mengubah progress course
    

Admin adalah **policy enforcer**, bukan **superuser finansial**.

---

## 4.3 Allowed Scope Smart Contract

- Vault crowdfund:
    
    - menyimpan dana aman
        
    - mendukung refund otomatis
        
- Fee:
    
    - 1% course payment → wallet perusahaan
        
- Campaign State Machine:
    
    - `pending`
        
    - `target_reached`
        
    - `executed`
        

Tidak ada state “abu-abu”.