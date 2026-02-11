## 3.1 User Segmentation

Sistem ini memiliki **tiga tipe user aktif** dan satu pasif:

1. Guest (pasif)
    
2. Student (aktif – consumer)
    
3. Teacher (aktif – provider)
    
4. Admin (aktif – governance)
    

Setiap user **berinteraksi dengan sistem melalui use case yang berbeda dan tidak overlap**.

---

## 3.2 User Personas

### 3.2.1 Guest Persona

**Karakteristik**

- Belum memiliki akun
    
- Masih mengevaluasi platform
    

**Tujuan**

- Menilai kualitas course
    
- Menilai kredibilitas pengajar
    
- Memahami model pembayaran
    

**Pain Points**

- Kurangnya transparansi di platform edukasi konvensional
    
- Tidak yakin dana benar-benar sampai ke pengajar
    

---

### 3.2.2 Student Persona

**Karakteristik**

- Ingin belajar skill tertentu
    
- Sensitif terhadap biaya
    
- Sebagian memiliki keterbatasan finansial
    

**Tujuan**

- Mengikuti course
    
- Mendapat sertifikat yang sah
    
- Jika tidak mampu, mendapatkan bantuan pembiayaan
    

**Pain Points**

- Course mahal
    
- Sertifikat tidak kredibel
    
- Ketergantungan pada platform kustodian
    

---

### 3.2.3 Teacher Persona

**Karakteristik**

- Pemilik keahlian
    
- Ingin monetisasi tanpa perantara
    

**Tujuan**

- Menjual course
    
- Menerima dana langsung
    
- Mengontrol kualitas akademik
    

**Pain Points**

- Fee platform tinggi
    
- Pembayaran tertunda
    
- Ketergantungan pada admin platform
    

---

### 3.2.4 Admin Persona

**Karakteristik**

- Operator sistem
    
- Tidak terlibat langsung dalam edukasi
    

**Tujuan**

- Menjaga integritas sistem
    
- Mencegah abuse
    

**Pain Points**

- Potensi fraud
    
- Overreach admin (harus dihindari)
    

---

## 3.3 Use Case Principles

Sebelum masuk daftar use case, sistem mengikuti prinsip berikut:

1. Setiap use case harus:
    
    - Memiliki aktor utama
        
    - Memiliki kondisi awal (precondition)
        
    - Memiliki hasil akhir (postcondition)
        
2. Tidak ada use case:
    
    - Tanpa aktor jelas
        
    - Tanpa perubahan state
        

---

## 3.4 Guest Use Cases

### UC-G1 — View Course List

**Aktor**: Guest  
**Tujuan**: Melihat semua course  
**Precondition**: Tidak ada  
**Alur Singkat**:

- Guest membuka halaman course
    
- Sistem menampilkan daftar course open
    

**Postcondition**:

- Tidak ada perubahan state
    

---

### UC-G2 — View Course Detail

**Aktor**: Guest  
**Tujuan**: Melihat detail course  
**Precondition**: Course exists  
**Alur Singkat**:

- Guest membuka halaman detail
    
- Sistem menampilkan syllabus, harga, status crowdfund
    

**Postcondition**:

- Tidak ada perubahan state
    

---

## 3.5 Student Use Cases

### UC-S1 — Register & Connect Wallet

**Aktor**: Student  
**Tujuan**: Membuat akun & menghubungkan wallet  
**Precondition**: Wallet tersedia  
**Postcondition**:

- User profile terbentuk
    
- Wallet address terikat
    

---

### UC-S2 — Enroll Course (Direct Payment)

**Aktor**: Student  
**Tujuan**: Mengikuti course  
**Precondition**:

- Course open
    
- Wallet connected
    

**Alur Normal**:

- Student klik enroll
    
- Smart contract memproses pembayaran
    
- Backend mencatat enrollment
    

**Postcondition**:

- Enrollment aktif
    
- Dana masuk ke teacher
    

---

### UC-S3 — Follow Course Progress

**Aktor**: Student  
**Tujuan**: Menyelesaikan course  
**Precondition**:

- Enrollment aktif
    

**Postcondition**:

- Progress meningkat otomatis
    

---

### UC-S4 — Submit Final Task

**Aktor**: Student  
**Tujuan**: Menyelesaikan course  
**Precondition**:

- Progress 100%
    

**Postcondition**:

- Final task berstatus pending approval
    

---

### UC-S5 — Claim Certificate

**Aktor**: Student  
**Tujuan**: Mendapat sertifikat  
**Precondition**:

- Final task approved
    

**Postcondition**:

- Sertifikat tercatat on-chain
    

---

### UC-S6 — Create Crowdfunding Campaign (Implicit)

**Aktor**: Student  
**Tujuan**: Mendapat pendanaan  
**Precondition**:

- Ditandai “tidak mampu”
    
- Course crowdfundable
    

**Postcondition**:

- Campaign state `pending`
    

---

### UC-S7 — Execute Crowdfunding (Fund Now)

**Aktor**: Student  
**Tujuan**: Menggunakan dana crowdfund  
**Precondition**:

- Campaign state `target_reached`
    

**Postcondition**:

- Dana diproses ke teacher
    
- Enrollment aktif
    

---

### UC-S8 — Withdraw Crowdfunding Funds

**Aktor**: Student / Donor  
**Tujuan**: Menarik dana jika gagal  
**Precondition**:

- Campaign tidak executed
    

**Postcondition**:

- Dana kembali ke donor
    

---

## 3.6 Teacher Use Cases

### UC-T1 — Create Course

**Aktor**: Teacher  
**Tujuan**: Membuat course  
**Postcondition**:

- Course state `draft`
    

---

### UC-T2 — Publish Course

**Aktor**: Teacher  
**Tujuan**: Membuka course  
**Precondition**:

- Course lengkap
    

**Postcondition**:

- Course state `open`
    

---

### UC-T3 — Approve Final Task

**Aktor**: Teacher  
**Tujuan**: Menentukan kelulusan  
**Precondition**:

- Final task submitted
    

**Postcondition**:

- Student eligible for certificate
    

---

### UC-T4 — Close Course

**Aktor**: Teacher  
**Tujuan**: Menghentikan enrollment  
**Postcondition**:

- Course state `closed`
    

---

## 3.7 Admin Use Cases

### UC-A1 — Set Student as “Tidak Mampu”

**Aktor**: Admin  
**Tujuan**: Mengaktifkan crowdfunding  
**Precondition**:

- Student exists
    

**Postcondition**:

- Flag “tidak mampu” aktif
    

---

### UC-A2 — Ban / Deactivate User

**Aktor**: Admin  
**Tujuan**: Moderasi  
**Postcondition**:

- User tidak bisa berinteraksi
    

---

## 3.8 User Journey (Ringkas, End-to-End)

### Student Journey (Happy Path)

1. Register & connect wallet
    
2. Pilih course
    
3. Enroll / crowdfund
    
4. Ikuti course
    
5. Submit final task
    
6. Claim certificate
    

### Teacher Journey

1. Create course
    
2. Publish course
    
3. Monitor enrollment
    
4. Approve final task
    
5. Receive funds
    

---

## 3.9 Explicit Non-Use Cases

- Student menentukan kelulusan sendiri
    
- Admin memicu pembayaran
    
- Teacher menarik dana crowdfund manual
    
- Guest berinteraksi dengan blockchain
    

---

## 3.10 Output File Ini

File ini menjadi dasar langsung untuk:

- Functional requirements (File No.5)
    
- API design
    
- Testing scenario
    
- Smart contract interface