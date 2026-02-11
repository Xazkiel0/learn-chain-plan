## 7.1 Tujuan File Ini

Dokumen ini bertujuan untuk:

- Memberikan **gambaran teknis menyeluruh**
    
- Menentukan **apa berada di mana**
    
- Mencegah:
    
    - Logic salah tempat
        
    - Backend terlalu berkuasa
        
    - Smart contract terlalu gemuk
        

Setelah file ini dikunci, perubahan arsitektur **harus disadari**, bukan insidental.

---

## 7.2 Architecture Style

Sistem menggunakan arsitektur **3-layer hybrid Web2 + Web3**:

1. **Frontend (Client Layer)**
    
2. **Backend (Application Layer)**
    
3. **Blockchain (Trust & Financial Layer)**
    

Prinsip utama:

> _On-chain untuk trust & money, off-chain untuk UX & logic non-kritis._

---

## 7.3 High-Level Architecture Diagram (Textual)

`[ Browser / Web App ]         |         |  (HTTP / Wallet RPC)         v [ Frontend (Next.js / SPA) ]         |         |  (REST / GraphQL)         v [ Backend API ]         |         |  (Read / Verify)         v [ Blockchain (Smart Contracts) ]`

Tidak ada:

- Backend → sign transaction
    
- Backend → move funds
    

---

## 7.4 Component Overview

### 7.4.1 Frontend (Client)

**Tanggung Jawab**

- UI & UX
    
- Wallet connection
    
- Trigger on-chain transaction
    
- Menampilkan status tx & progress
    

**Tidak Bertanggung Jawab**

- Menentukan kelulusan
    
- Menyimpan state keuangan
    

---

### 7.4.2 Backend (Application Server)

**Tanggung Jawab**

- User management
    
- Course & content management
    
- Progress tracking
    
- Sync state on-chain → off-chain
    

**Karakter**

- Stateless (sebisa mungkin)
    
- Tidak dipercaya untuk dana
    

---

### 7.4.3 Smart Contracts (Blockchain Layer)

**Tanggung Jawab**

- Enrollment payment
    
- Platform fee handling
    
- Crowdfunding vault
    
- Certification record
    

**Karakter**

- Deterministik
    
- Immutable (MVP)
    

---

## 7.5 Smart Contract Modules (Conceptual)

### 7.5.1 CoursePayment Contract

- Fungsi:
    
    - enrollCourse()
        
- Logic:
    
    - Validasi harga
        
    - Transfer ke teacher
        
    - Fee ke platform
        

---

### 7.5.2 CrowdfundingVault Contract

- Fungsi:
    
    - fundCampaign()
        
    - executeCampaign()
        
    - withdraw()
        
- Logic:
    
    - State machine campaign
        
    - Vault control
        

---

### 7.5.3 CertificationRegistry Contract

- Fungsi:
    
    - issueCertificate()
        
- Data:
    
    - Certificate hash
        
    - Metadata reference
        

---

## 7.6 Data Flow Overview

### 7.6.1 Enrollment Flow

1. Frontend → wallet sign tx
    
2. Tx → blockchain
    
3. Tx success event emitted
    
4. Backend listens / verifies
    
5. Enrollment created off-chain
    

---

### 7.6.2 Crowdfunding Flow

1. Donor fund via wallet
    
2. Dana masuk vault contract
    
3. Campaign state updated
    
4. Backend sync state
    
5. Student executes when ready
    

---

### 7.6.3 Certification Flow

1. Backend marks eligible
    
2. Frontend trigger claim
    
3. Wallet signs tx
    
4. Hash recorded on-chain
    

---

## 7.7 Integration Points

### 7.7.1 Wallet Provider

- Metamask / WalletConnect
    
- Client-side only
    

---

### 7.7.2 Blockchain Node / RPC

- Read:
    
    - Event
        
    - State
        
- Write:
    
    - Via user wallet
        

Backend **tidak boleh** menjadi tx sender.

---

### 7.7.3 External Services (Optional MVP)

- IPFS / object storage:
    
    - Certificate metadata
        
    - Course assets
        

---

## 7.8 Trust Boundary Definition

|Boundary|Trusted?|
|---|---|
|Frontend|❌|
|Backend|❌|
|Smart Contract|✅|

Backend dianggap **honest-but-curious**, bukan trusted.

---

## 7.9 State Ownership

|State|Owner|
|---|---|
|Course content|Backend|
|Enrollment validity|Blockchain|
|Crowdfunding funds|Blockchain|
|Progress|Backend|
|Certificate validity|Blockchain|

---

## 7.10 Failure Scenarios (High-Level)

### RPC Down

- UI: show pending / retry
    
- Backend: do not mutate state
    

### Tx Failed

- Enrollment not created
    
- No side effects
    

---

## 7.11 Architecture Trade-offs (Disadari)

- Lebih banyak kompleksitas sync
    
- Lebih lambat dari Web2-only
    
- Lebih aman dan transparan
    

Trade-off ini **disengaja**.

---

## 7.12 Output File Ini

File ini menjadi dasar untuk:

- Tech stack choice (File 8)
    
- API & backend design (File 9)
    
- Database design (File 10)
    
- Smart contract TDD