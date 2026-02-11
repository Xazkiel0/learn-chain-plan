## 5.1 Tujuan File Ini

Dokumen ini mendefinisikan:

- **Fungsi yang wajib ada**
    
- **Bagaimana sistem berperilaku**
    
- **Apa yang terjadi saat kondisi normal dan edge case**
    

Jika suatu fitur **tidak tercantum di sini**, maka:

- Tidak termasuk MVP
    
- Tidak boleh diimplementasikan tanpa revisi dokumen
    

---

## 5.2 Feature Grouping

Fitur sistem dikelompokkan menjadi:

1. User & Auth
    
2. Course Management
    
3. Enrollment & Payment
    
4. Crowdfunding
    
5. Progress & Assessment
    
6. Certification
    
7. Admin & Governance
    

---

## 5.3 User & Authentication

### FR-U1 — User Registration

**Deskripsi**  
User dapat membuat akun menggunakan email / auth method yang dipilih platform.

**Perilaku**

- Sistem membuat user profile off-chain
    
- Status user: `active`
    

**Edge Case**

- Email duplikat → gagal
    

**Prioritas**: MVP

---

### FR-U2 — Wallet Connection

**Deskripsi**  
User dapat menghubungkan wallet ke akun.

**Perilaku**

- Wallet address disimpan sebagai financial identifier
    
- Satu wallet ↔ satu user
    

**Edge Case**

- Wallet sudah terhubung ke user lain → gagal
    

**Prioritas**: MVP

---

## 5.4 Course Management (Teacher)

### FR-C1 — Create Course

**Deskripsi**  
Teacher dapat membuat course baru.

**Perilaku**

- Course state awal: `draft`
    
- Course belum bisa di-enroll
    

**Prioritas**: MVP

---

### FR-C2 — Define Course Properties

**Deskripsi**  
Teacher dapat mengatur:

- Harga
    
- Syllabus
    
- Crowdfundable flag
    

**Edge Case**

- Harga = 0 → dianggap free course
    

**Prioritas**: MVP

---

### FR-C3 — Publish Course

**Deskripsi**  
Teacher dapat membuka course.

**Perilaku**

- State berubah ke `open`
    
- Course muncul di listing publik
    

**Edge Case**

- Data belum lengkap → gagal publish
    

**Prioritas**: MVP

---

### FR-C4 — Close Course

**Deskripsi**  
Teacher dapat menutup course.

**Perilaku**

- State berubah ke `closed`
    
- Enrollment baru tidak diperbolehkan
    

**Prioritas**: MVP

---

## 5.5 Enrollment & Payment

### FR-E1 — Enroll Course (Direct Payment)

**Deskripsi**  
Student dapat enroll course berbayar.

**Perilaku**

- Smart contract:
    
    - Transfer dana ke teacher
        
    - Potong fee platform
        
- Backend mencatat enrollment
    

**Edge Case**

- Transaksi gagal → enrollment tidak dibuat
    

**Prioritas**: MVP

---

### FR-E2 — Enroll Free Course

**Deskripsi**  
Student dapat enroll course gratis.

**Perilaku**

- Tidak ada transaksi on-chain
    
- Enrollment langsung aktif
    

**Prioritas**: MVP

---

## 5.6 Crowdfunding

### FR-CF1 — Create Crowdfunding Campaign (Implicit)

**Deskripsi**  
Campaign otomatis dibuat saat student eligible memilih course crowdfundable.

**Precondition**

- Student “tidak mampu”
    
- Course crowdfundable
    

**Perilaku**

- Campaign state: `pending`
    

**Prioritas**: MVP

---

### FR-CF2 — Fund Campaign

**Deskripsi**  
Donor dapat mendanai campaign.

**Perilaku**

- Dana masuk vault smart contract
    
- Total funding diperbarui
    

**Edge Case**

- Campaign executed → funding ditolak
    

**Prioritas**: MVP

---

### FR-CF3 — Target Reached Detection

**Deskripsi**  
Sistem mendeteksi jika target tercapai.

**Perilaku**

- State otomatis berubah ke `target_reached`
    

**Prioritas**: MVP

---

### FR-CF4 — Execute Crowdfunding (Fund Now)

**Deskripsi**  
Student mengeksekusi campaign.

**Perilaku**

- Dana dikirim ke teacher
    
- Enrollment dibuat
    

**Edge Case**

- Student tidak mengeksekusi → dana tetap di vault
    

**Prioritas**: MVP

---

### FR-CF5 — Withdraw Failed Campaign Funds

**Deskripsi**  
Donor dapat menarik dana jika campaign gagal.

**Perilaku**

- Dana dikembalikan penuh
    
- Tanpa fee
    

**Prioritas**: MVP

---

## 5.7 Progress & Assessment

### FR-P1 — Automatic Progress Tracking

**Deskripsi**  
Sistem menghitung progress otomatis.

**Perilaku**

- Progress meningkat berdasarkan modul selesai
    
- Tidak bisa diubah manual
    

**Prioritas**: MVP

---

### FR-P2 — Submit Final Task

**Deskripsi**  
Student dapat submit final task.

**Precondition**

- Progress = 100%
    

**Prioritas**: MVP

---

### FR-P3 — Approve / Reject Final Task

**Deskripsi**  
Teacher dapat menilai final task.

**Perilaku**

- Approved → eligible certificate
    
- Rejected → student revisi
    

**Prioritas**: MVP

---

## 5.8 Certification

### FR-CERT1 — Claim Certificate

**Deskripsi**  
Student dapat mengklaim sertifikat.

**Perilaku**

- Hash + metadata dicatat on-chain
    
- Sertifikat non-transferable
    

**Edge Case**

- Klaim kedua → gagal
    

**Prioritas**: MVP

---

## 5.9 Admin & Governance

### FR-A1 — Set Student as “Tidak Mampu”

**Deskripsi**  
Admin dapat mengubah status student.

**Perilaku**

- Status tersimpan off-chain
    

**Prioritas**: MVP

---

### FR-A2 — Deactivate User

**Deskripsi**  
Admin dapat menonaktifkan user.

**Perilaku**

- User tidak bisa login / transaksi
    

**Edge Case**

- Enrollment aktif tetap berjalan
    

**Prioritas**: MVP

---

## 5.10 Explicitly Deferred (Post-MVP)

- Multi-chain support
    
- Transferable NFT certificate
    
- DAO governance
    
- Rating & review system
    
- Dispute resolution
    

---

## 5.11 Acceptance Criteria (Contoh Kunci)

Contoh untuk **Enroll Course**:

- Given course open
    
- When payment sukses on-chain
    
- Then enrollment aktif
    
- And dana masuk ke teacher
    
- And platform fee tercatat
    

---

## 5.12 Output File Ini

File ini langsung dipakai untuk:

- Backlog engineering
    
- API contract definition
    
- Smart contract interface
    
- Test case derivation