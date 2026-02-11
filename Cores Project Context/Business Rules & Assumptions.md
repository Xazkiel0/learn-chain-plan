## 4.1 Tujuan File Ini

Dokumen ini mendefinisikan:

- **Aturan bisnis yang tidak boleh dilanggar**
    
- **Batasan sistem yang disengaja**
    
- **Asumsi eksplisit** yang menjadi dasar desain
    

Jika terjadi konflik antara:

- implementasi kode
    
- intuisi developer
    
- permintaan fitur tambahan
    

→ **dokumen ini yang menang**, kecuali direvisi secara sadar.

---

## 4.2 Core Business Rules (Aturan Utama)

### BR-01 — Non-Custodial Funds

- Platform **tidak boleh menyimpan dana user**
    
- Semua dana:
    
    - Enrollment
        
    - Crowdfunding  
        harus dikontrol oleh **smart contract**
        

Backend dan admin **tidak memiliki akses** ke private key atau vault.

---

### BR-02 — Direct Payment to Teacher

- Pembayaran course:
    
    - Langsung ke wallet teacher
        
    - Fee platform (1%) dipotong otomatis
        
- Tidak ada:
    
    - Penahanan dana
        
    - Escrow off-chain
        

Transaksi **irreversible** setelah sukses on-chain.

---

### BR-03 — Crowdfunding Terikat (Restricted Campaign)

- Campaign:
    
    - Menempel pada **1 Student + 1 Course**
        
    - Tidak bisa dibuat dengan parameter bebas
        
- Tidak ada:
    
    - Campaign global
        
    - Campaign dengan target arbitrary
        

Tujuannya: mencegah misuse crowdfunding.

---

### BR-04 — Crowdfunding Vault Authority

- Dana crowdfunding:
    
    - Disimpan di vault smart contract
        
- Hanya smart contract yang boleh:
    
    - Menyimpan
        
    - Mendistribusikan
        
    - Mengembalikan dana
        

Tidak ada:

- Admin override
    
- Teacher override
    
- Backend override
    

---

### BR-05 — Crowdfunding State Machine (Wajib)

Campaign hanya memiliki **3 state sah**:

1. `pending`
    
2. `target_reached`
    
3. `executed`
    

Aturan transisi:

- `pending → target_reached`  
    Jika total dana ≥ harga course
    
- `target_reached → executed`  
    Hanya jika student memilih **fund now**
    

Tidak ada transisi lain yang valid.

---

### BR-06 — Withdraw Policy (Failed Campaign)

- Jika campaign:
    
    - Tidak pernah dieksekusi
        
- Maka:
    
    - Donor **berhak withdraw penuh**
        
    - Tidak dikenakan fee
        

Ini berlaku tanpa batas waktu (selama campaign belum executed).

---

### BR-07 — Enrollment Validity

- Enrollment sah hanya jika:
    
    - Payment sukses on-chain, atau
        
    - Crowdfunding berhasil dieksekusi
        
- Backend **tidak boleh** menciptakan enrollment manual
    

---

### BR-08 — Course Completion Definition

Course dianggap **selesai** jika dan hanya jika:

1. Progress otomatis mencapai 100%
    
2. Final task telah **approved oleh teacher**
    

Kedua syarat **wajib terpenuhi**.

---

### BR-09 — Certification Rules

- Sertifikat:
    
    - Dicatat on-chain (hash + metadata)
        
    - Tidak transferable
        
    - Tidak bisa dicabut
        
- Sertifikat hanya bisa:
    
    - Diklaim sekali
        
    - Setelah course completed sah
        

---

### BR-10 — Admin Power Limitation

Admin **tidak boleh**:

- Mengubah progress
    
- Menyetujui kelulusan
    
- Mengubah state campaign
    
- Mengambil atau mendistribusikan dana
    

Admin hanya boleh:

- Mengubah status user
    
- Menandai “tidak mampu”
    

---

## 4.3 System Constraints (Batasan Sistem)

### C-01 — Wallet as Financial Identity

- Wallet address adalah satu-satunya identitas finansial
    
- User bisa:
    
    - Ganti profile
        
    - Tapi tidak bisa memindahkan histori dana
        

---

### C-02 — On-chain vs Off-chain Boundary

- On-chain:
    
    - Payment
        
    - Crowdfunding
        
    - Certification record
        
- Off-chain:
    
    - User profile
        
    - Course content
        
    - Progress tracking
        

Tidak boleh tertukar.

---

### C-03 — No Manual Override

- Tidak ada:
    
    - Manual update progress
        
    - Manual enrollment
        
    - Manual certificate issuance
        

Jika sistem tidak mendukung, maka **fitur tidak ada**.

---

### C-04 — MVP Scope Constraint

- Hanya satu chain
    
- Satu currency (native atau ERC20, dipilih di TDD)
    
- Tidak ada cross-chain
    
- Tidak ada upgrade contract tanpa migrasi eksplisit
    

---

## 4.4 Assumptions (Asumsi yang Digunakan)

### A-01 — User Mengerti Risiko Web3

Diasumsikan:

- User memahami:
    
    - Transaction fee
        
    - Irreversible transaction
        
- Sistem hanya memberi notifikasi, bukan proteksi penuh
    

---

### A-02 — Kategori “Tidak Mampu” Ditentukan Off-chain

- Admin menentukan status “tidak mampu”
    
- Sistem tidak:
    
    - Mengkalkulasi ekonomi user
        
    - Mengverifikasi dokumen finansial
        

Ini keputusan governance, bukan teknis.

---

### A-03 — Teacher Bertindak Jujur Secara Akademik

Diasumsikan:

- Teacher:
    
    - Menilai final task secara objektif
        
- Sistem tidak:
    
    - Meng-audit kualitas penilaian
        

---

### A-04 — Platform Fee Stabil

- Fee platform ditetapkan:
    
    - 1%
        
- Tidak berubah dalam MVP
    
- Tidak dinamis
    

---

### A-05 — No Legal Enforcement Layer

- Sistem:
    
    - Tidak menangani sengketa hukum
        
    - Tidak menyediakan arbitration
        

Dispute di luar sistem.

---

## 4.5 Dependencies (Ketergantungan Eksternal)

- Blockchain network stabil
    
- Wallet provider tersedia
    
- RPC provider reliabel
    

Jika dependency gagal:

- Sistem tetap aman
    
- Tapi fungsi terkait tertunda
    

---

## 4.6 Explicit Non-Rules (Hal yang Sengaja Tidak Diatur)

- Harga course tidak diatur platform
    
- Jadwal course tidak dipaksakan sistem
    
- Donor tidak dijanjikan imbalan apa pun
    
- Tidak ada SLA akademik
    

---

## 4.7 Conflict Resolution Guideline

Jika terjadi konflik antara:

- UX vs security
    
- Simplicity vs flexibility
    

**Keputusan default**:

1. Security
    
2. Business rule
    
3. Simplicity
    
4. UX
    

---

## 4.8 Output File Ini

File ini menjadi:

- Guardrail utama saat implementasi
    
- Rujukan saat muncul edge case
    
- Dasar validasi fitur di File No.5