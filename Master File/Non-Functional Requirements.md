## 6.1 Tujuan File Ini

Dokumen ini mendefinisikan **kualitas sistem yang harus dipenuhi**, terlepas dari fitur.

Jika suatu implementasi:

- Memenuhi functional requirements
    
- Tapi melanggar NFR
    

→ dianggap **belum layak rilis**.

---

## 6.2 Performance Requirements

### NFR-PERF-01 — Response Time (Off-chain)

- API backend:
    
    - Target ≤ 500 ms untuk 95% request
        
- Page load (frontend):
    
    - Target ≤ 3 detik pada koneksi normal
        

Catatan:

- Transaksi blockchain **tidak termasuk** SLA ini (bergantung network).
    

---

### NFR-PERF-02 — Concurrency (MVP)

- Sistem harus mendukung:
    
    - ≥ 100 concurrent users
        
- Tanpa:
    
    - Data corruption
        
    - Double enrollment
        

---

## 6.3 Security Requirements

### NFR-SEC-01 — Private Key Handling

- Backend **tidak boleh**:
    
    - Menyimpan private key
        
    - Menandatangani transaksi atas nama user
        

Semua signing dilakukan di client wallet.

---

### NFR-SEC-02 — Smart Contract Authority

- Smart contract adalah:
    
    - Single source of truth untuk dana
        
- Tidak ada:
    
    - Admin key override
        
    - Emergency withdraw di MVP
        

---

### NFR-SEC-03 — Authentication & Authorization

- Setiap endpoint:
    
    - Wajib auth
        
    - Role-based access control (RBAC)
        
- Unauthorized access → 403
    

---

### NFR-SEC-04 — Input Validation

- Semua input:
    
    - Disanitasi
        
    - Diverifikasi tipe & batasannya
        
- On-chain input:
    
    - Validasi ganda (frontend + contract)
        

---

### NFR-SEC-05 — Smart Contract Auditability

- Smart contract harus:
    
    - Verified di block explorer
        
    - Code source terbuka untuk publik
        
- Vault crowdfunding:
    
    - Transparan (siapa funder, berapa terkumpul)
        
    - Tidak ada hidden fee selain 1% platform fee
        

---

### NFR-SEC-06 — Admin Financial Isolation

- Admin platform:
    
    - **Tidak memiliki akses** ke dana user di smart contract
        
    - Tidak bisa memicu eksekusi crowdfunding secara paksa
        
    - Tidak bisa mengubah status kelulusan/akademik secara sepihak
        

---

## 6.4 Reliability & Consistency

### NFR-REL-01 — Transaction Consistency

- Enrollment hanya valid jika:
    
    - On-chain tx sukses
        
- Tidak boleh ada:
    
    - Enrollment tanpa tx
        
    - Tx tanpa enrollment (setelah finality)
        

---

### NFR-REL-02 — Idempotency

- API kritikal (enroll, submit):
    
    - Harus idempotent
        
- Retry request tidak menciptakan state ganda
    

---

### NFR-REL-03 — Fault Tolerance

- Jika:
    
    - RPC gagal
        
    - Network delay
        
- Sistem:
    
    - Tidak corrupt state
        
    - Menampilkan status “pending” secara jelas
        

---

### NFR-REL-04 — Web2-Web3 State Synchronization

- Konsistensi antara database backend (Web2) dan smart contract (Web3):
    
    - Course state (`draft`, `open`, `closed`)
        
    - Campaign state (`pending`, `target_reached`, `executed`)
        
    - Enrollment state (`enrolled`, `completed`)
        
- Mekanisme rekonsiliasi:
    
    - Backend harus mendengarkan event blockchain (listener)
        
    - Mengupdate database lokal secara real-time (atau near real-time)
        

---

## 6.5 Usability Requirements

### NFR-UX-01 — Web3 Transparency

- User harus:
    
    - Melihat status transaksi (pending / success / failed)
        
- Tidak ada:
    
    - Silent failure
        

---

### NFR-UX-02 — Error Feedback

- Error message:
    
    - Jelas
        
    - Tidak teknis berlebihan
        
- Contoh:
    
    - “Transaksi dibatalkan di wallet”
        
    - Bukan stack trace
        

---

### NFR-UX-03 — Minimal Cognitive Load

- Flow utama:
    
    - Enroll
        
    - Fund
        
    - Claim certificate  
        harus ≤ 3 langkah utama
        

---

### NFR-UX-04 — Role Clarity

- Antarmuka harus:
    
    - Membedakan dengan jelas status Guest vs User (wallet connected)
        
    - Memberikan feedback "Connect Wallet" pada fitur yang membutuhkan akses Web3
        
    - Menampilkan role user (Student / Teacher / Admin) secara eksplisit
        

---

## 6.6 Scalability (Conscious Limitation)

### NFR-SCAL-01 — MVP Scalability Target

- Optimasi hanya untuk:
    
    - Skala kecil–menengah
        
- Tidak perlu:
    
    - Sharding
        
    - Microservices
        

Monolith backend diperbolehkan.

---

## 6.7 Maintainability

### NFR-MAIN-01 — Clear Separation of Concerns

- Frontend:
    
    - UI + wallet interaction
        
- Backend:
    
    - Business logic
        
    - State sync
        
- Smart contract:
    
    - Financial logic
        

Tidak boleh overlap.

---

### NFR-MAIN-02 — Configuration Over Hardcode

- Address contract
    
- Fee platform
    
- RPC endpoint  
    → harus via config, bukan hardcoded
    

---

## 6.8 Observability (Minimum)

### NFR-OBS-01 — Logging

- Log event:
    
    - Enrollment
        
    - Crowdfunding execution
        
    - Certificate claim
        
- Tanpa menyimpan data sensitif
    

---

### NFR-OBS-02 — Error Monitoring

- Error backend dicatat
    
- Critical error:
    
    - Bisa ditelusuri via log
        

Tidak wajib alerting canggih di MVP.

---

## 6.9 Compliance & Data Privacy

### NFR-PRIV-01 — Data Minimization

- Hanya simpan:
    
    - Data yang dibutuhkan untuk fungsi sistem
        
- Tidak menyimpan:
    
    - Data finansial sensitif
        

---

### NFR-PRIV-02 — Public vs Private Data

- Public:
    
    - Course info
        
    - Certificate hash
        
- Private:
    
    - User profile
        
    - Submission data
        

---

### NFR-PRIV-03 — On-Chain Privacy

- Data di blockchain:
    
    - Tidak boleh mengandung PII (nama lengkap, email, alamat fisik)
        
    - Hanya menyimpan referensi hash (IPFS CID atau SHA256)
        
    - Transaksi bersifat publik (wallet address visible)
        
- Data crowdfunding:
    
    - Identitas penerima (Student) hanya link ke profil Web2 (optional)
        
    - Alasan finansial sensitif tidak dipublish on-chain
        

---

## 6.10 Non-Goals (Explicit)

- 100% uptime
    
- Zero gas fee
    
- Instant finality
    

Ini di luar kontrol sistem.

---

## 6.11 Quality Bar (Ringkas)

Sistem **tidak boleh dirilis** jika:

- Dana user bisa dimanipulasi off-chain
    
- Enrollment bisa dibuat tanpa tx sah
    
- Sertifikat bisa diklaim tanpa kelulusan
    
- Dana crowdfunding dicairkan tanpa target tercapai
    

---

## 6.12 Output File Ini

File ini menjadi:

- Checklist pre-release
    
- Acuan QA
    
- Guardrail saat refactor