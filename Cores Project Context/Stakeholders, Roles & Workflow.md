## 2.1 Stakeholders Overview

Stakeholder dalam proyek ini dibagi menjadi **dua kategori besar**:

1. **External Stakeholders (Pengguna Sistem)**
    
2. **Internal Stakeholders (Pengelola & Pengembang Sistem)**
    

Pemisahan ini penting karena:

- External stakeholder berinteraksi dengan produk
    
- Internal stakeholder bertanggung jawab atas keberlangsungan sistem
    

---

## 2.2 External Stakeholders

### 2.2.1 Pelajar (Student)

**Peran dalam Sistem**

- Konsumen utama course
    
- Beneficiary crowdfunding
    
- Pemilik hasil akademik (sertifikat)
    

**Kepentingan Utama**

- Akses course yang jelas dan transparan
    
- Keamanan dana
    
- Bukti kelulusan yang sah dan tidak bisa dimanipulasi
    

**Interaksi Utama**

- Frontend (UI)
    
- Smart contract (payment & certification)
    
- Backend (progress tracking, submission)
    

---

### 2.2.2 Pengajar (Teacher)

**Peran dalam Sistem**

- Penyedia konten edukasi
    
- Penerima dana course
    
- Evaluator akademik (final task)
    

**Kepentingan Utama**

- Dana masuk langsung ke wallet
    
- Kontrol penuh atas course yang dibuat
    
- Tidak bergantung pada admin untuk pembayaran
    

**Interaksi Utama**

- Frontend (course management)
    
- Backend (content & task review)
    
- Smart contract (penerimaan dana)
    

---

## 2.3 Internal Stakeholders

### 2.3.1 Admin (Platform Operator)

**Peran dalam Sistem**

- Governance & moderation
    
- Trust enabler, bukan trust holder
    

**Kepentingan Utama**

- Sistem stabil
    
- Tidak ada abuse
    
- Kepatuhan terhadap aturan internal platform
    

**Catatan Penting**  
Admin **bukan pemilik sistem keuangan**, dan **bukan pengambil keputusan akademik**.

---

### 2.3.2 Developer (Solo Fullstack Dev)

**Peran**

- System designer
    
- Implementor backend, frontend, dan smart contract
    
- Maintainer sistem
    

**Kepentingan**

- Arsitektur yang tidak ambigu
    
- Workflow yang bisa dikerjakan end-to-end tanpa koordinasi tim besar
    
- Dokumentasi yang mengurangi keputusan ad-hoc saat coding
    

Dokumen ini secara eksplisit dibuat untuk **melindungi developer dari scope creep dan desain inkonsisten**.

---

## 2.4 Roles Mapping & Responsibility Matrix (Ringkas)

|Area|Student|Teacher|Admin|System|
|---|---|---|---|---|
|Course Creation|❌|✅|❌|❌|
|Course Enrollment|✅|❌|❌|✅|
|Payment Handling|❌|❌|❌|✅ (SC)|
|Crowdfunding Control|Partial|❌|❌|✅ (SC)|
|Final Task Approval|❌|✅|❌|❌|
|Certification Issuance|Trigger|❌|❌|✅|
|User Status Control|❌|❌|✅|❌|

(SC = Smart Contract)

---

## 2.5 High-Level Workflow Overview

Secara garis besar, workflow sistem terbagi menjadi **5 alur utama**:

1. User onboarding
    
2. Course lifecycle
    
3. Enrollment & payment
    
4. Crowdfunding
    
5. Course completion & certification
    

Masing-masing alur **berdiri sendiri tapi saling terhubung**.

---

## 2.6 Workflow 1 — User Onboarding

### Alur

1. Guest mengakses platform
    
2. User register & login
    
3. User connect wallet
    
4. System:
    
    - Membuat user profile off-chain
        
    - Mengaitkan wallet address
        

### Catatan Desain

- Wallet address adalah **identifier finansial**, bukan primary key user
    
- Backend **tidak menyimpan private key**
    

---

## 2.7 Workflow 2 — Course Lifecycle (Teacher-Centric)

### Alur

1. Teacher membuat course (draft)
    
2. Teacher:
    
    - Menentukan harga
        
    - Menentukan crowdfundable / tidak
        
3. Teacher membuka course (open)
    
4. Course tersedia untuk enrollment
    
5. Teacher menutup course (closed)
    

### Restriksi

- Course closed tidak bisa diubah
    
- Course open tidak bisa dihapus
    

---

## 2.8 Workflow 3 — Enrollment & Payment

### Alur Normal

1. Student memilih course
    
2. Student klik enroll
    
3. Smart contract:
    
    - Menerima pembayaran
        
    - Mengirim dana ke wallet teacher
        
    - Mengirim fee ke wallet platform
        
4. Backend mencatat enrollment
    

### Catatan Penting

- Backend **tidak pernah menyentuh dana**
    
- Enrollment bersifat **irreversible**
    

---

## 2.9 Workflow 4 — Crowdfunding

### Kondisi Awal

- Student ditandai “tidak mampu” oleh admin
    
- Course bersifat crowdfundable
    

### Alur

1. Student membuat campaign (implicit)
    
2. Campaign state awal: `pending`
    
3. Donor mendanai campaign
    
4. Jika total >= harga course → `target_reached`
    
5. Student memilih:
    
    - `fund now` → state `executed`
        
    - atau tidak mengeksekusi
        
6. Jika gagal:
    
    - Donor bisa withdraw dana
        

### Prinsip Utama

- Tidak ada manual override
    
- Smart contract adalah satu-satunya vault
    

---

## 2.10 Workflow 5 — Course Completion & Certification

### Alur

1. Student menyelesaikan semua modul
    
2. Progress otomatis mencapai 100%
    
3. Student submit final task
    
4. Teacher approve final task
    
5. System:
    
    - Menandai course completed
        
    - Mengaktifkan klaim sertifikat
        
6. Student klaim sertifikat on-chain
    

### Catatan

- Sertifikat tidak transferable
    
- Sertifikat hanya bisa diklaim sekali
    

---

## 2.11 Development Workflow (Ringkas, Solo Dev Friendly)

Urutan kerja yang direkomendasikan:

1. Lock dokumentasi (file 1–4)
    
2. Final ERD & state machine
    
3. Smart contract first (payment + crowdfund)
    
4. Backend API
    
5. Frontend
    
6. Integrasi end-to-end
    
7. Testing & deploy
    

Tujuannya: **menghindari rewrite besar di akhir**.

---

## 2.12 Coordination & Decision Authority

|Keputusan|Otoritas|
|---|---|
|Harga course|Teacher|
|Kelulusan|Teacher|
|Status tidak mampu|Admin|
|Eksekusi crowdfund|Student|
|Distribusi dana|Smart contract|
|Sertifikat valid|System (on-chain)|

Tidak ada keputusan yang **ambigu atau overlap**.

---

## 2.13 Explicit Non-Responsibilities

- Admin **bukan** financial operator
    
- Teacher **bukan** controller crowdfunding
    
- Student **bukan** validator akademik
    
- Backend **bukan** trusted party
    

Ini sengaja ditulis eksplisit untuk mencegah pelanggaran desain saat coding.