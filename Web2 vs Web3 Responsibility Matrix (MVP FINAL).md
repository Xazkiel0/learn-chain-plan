

Tujuan dokumen ini:

- Mengunci **apa yang on-chain, apa yang off-chain**
    
- Menjadi **rule of decision** setiap kali kamu ragu
    
- Mencegah **over-chain**, **gas burn**, dan **logic split**
    

---

## 1. Prinsip Dasar (jangan dilanggar)

Pegang 4 prinsip ini:

1. **Dana = Web3**
    
2. **UX & workflow = Web2**
    
3. **Trust boundary = Web3**
    
4. **State yang sering berubah = Web2**
    

Kalau satu fitur melanggar prinsip ini, **desainnya salah**.

---

## 2. Responsibility Matrix (FINAL untuk MVP)

### A. Identity & Access

|Concern|Web2|Web3|Alasan|
|---|---|---|---|
|Register / Login|✅|❌|UX cepat, murah|
|Role (student/teacher/admin)|✅|❌|Governance off-chain|
|Scholarship flag|✅|❌|Sementara, admin-driven|
|Wallet connect|❌|✅|Ownership user|

➡️ **Wallet ≠ identity**, hanya bukti kepemilikan aset.

---

### B. Course Management

|Concern|Web2|Web3|Alasan|
|---|---|---|---|
|Course CRUD|✅|❌|Sering berubah|
|Price|✅|❌|Referensi UI|
|Syllabus & progress|✅|❌|High frequency|
|Course status|✅|❌|Workflow|

➡️ **Course bukan aset blockchain**, hanya objek bisnis.

---

### C. Enrollment & Learning

|Concern|Web2|Web3|Alasan|
|---|---|---|---|
|Enrollment record|✅|❌|Cepat & mutable|
|Progress tracking|✅|❌|Update intens|
|Task submission|✅|❌|Approval logic|
|Course completion|✅|❌|Precondition cert|

➡️ Jangan pernah simpan progress on-chain.

---

### D. Crowdfunding (INTI TRUST)

|Concern|Web2|Web3|Alasan|
|---|---|---|---|
|Campaign creation|✅|❌|Validasi role & scope|
|Campaign state mirror|✅|❌|UI & analytics|
|Fund transfer|❌|✅|Trustless|
|Vault custody|❌|✅|Non-custodial|
|Refund logic|❌|✅|Anti manipulasi|
|Fee distribution|❌|✅|Transparansi|

➡️ **Crowdfunding = smart contract domain**  
Backend **tidak boleh** memegang saldo.

---

### E. Certificate & Trust Artifact

|Concern|Web2|Web3|Alasan|
|---|---|---|---|
|Completion check|✅|❌|Sistem internal|
|Certificate metadata|✅|❌|Fleksibel|
|Certificate hash|❌|✅|Immutable proof|
|Certificate verification|❌|✅|Public trust|

➡️ Ini **cukup**, NFT transferable **tidak perlu** di MVP.

---

### F. Platform Economics

|Concern|Web2|Web3|Alasan|
|---|---|---|---|
|Fee rule (1%)|❌|✅|Enforced|
|Platform wallet|❌|✅|Transparent|
|Accounting mirror|✅|❌|Reporting|

➡️ Fee **harus** dihitung on-chain, bukan backend.

---

## 3. Boundary Rules (WAJIB kamu ingat saat coding)

### Rule 1 — Backend tidak pernah menyentuh dana

Jika backend:

- menyimpan balance
    
- menghitung saldo
    

→ **desain salah**

---

### Rule 2 — Smart contract tidak peduli UX

Smart contract:

- tidak tahu siapa admin
    
- tidak tahu siapa “tidak mampu”
    
- hanya tahu **address & rules**
    

---

### Rule 3 — Semua state on-chain harus punya mirror off-chain

Tujuan:

- UI cepat
    
- analytics
    
- recovery kalau RPC lambat
    

---

## 4. Dampak langsung ke desain arsitektur kamu

Setelah matrix ini:

- kamu **tahu kontrak apa saja yang perlu**
    
- kamu **tahu API mana yang perlu**
    
- kamu **tahu data apa yang tidak boleh di-chain**
    

Tanpa matrix ini:

- smart contract akan terlalu besar
    
- backend akan terlalu berkuasa
    
- trust narrative runtuh