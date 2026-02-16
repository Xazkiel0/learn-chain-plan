## 10.1 Tujuan File Ini

File ini mendefinisikan:

- Struktur tabel utama
    
- Relasi antar entitas
    
- Aturan integritas data
    
- Constraint penting
    
- Prinsip desain skema
    

Database adalah **single source of truth off-chain**.  
Blockchain bukan pengganti database, hanya lapisan trust.

---

## 10.2 Prinsip Desain Data

Semua desain mengikuti prinsip berikut:

### 1. Relational-First

Karena:

- Relasi kuat antar entitas (user, course, enrollment, funding)
    
- Perlu konsistensi transaksi
    
- Reporting membutuhkan query kompleks
    

Menggunakan: **PostgreSQL**

---

### 2. Integrity Over Flexibility

- Foreign key wajib
    
- Constraint eksplisit
    
- ENUM untuk status penting
    
- Unique constraint untuk mencegah duplikasi
    

---

### 3. Blockchain-Aware

Semua entitas yang terkait on-chain harus menyimpan:

- tx_hash
    
- block_number
    
- status sinkronisasi
    

Tujuannya:

- Auditability
    
- Idempotency
    
- Rekonsiliasi bila mismatch
    

---

## 10.3 Entity Relationship Overview (High-Level ERD)

Entitas utama:

- users
    
- courses
    
- enrollments
    
- fundings
    
- funding_transactions
    
- course_progress
    
- admin_logs
    

Relasi utama:

```
User (1) —— (N) Course
User (1) —— (N) Enrollment
Course (1) —— (N) Enrollment
Course (1) —— (N) Funding
Funding (1) —— (N) Funding_Transaction
User (1) —— (N) Funding_Transaction
```

---

## 10.4 Core Tables

---

## 10.4.1 users

Menyimpan semua user (student, instructor, admin).

|Field|Type|Constraint|
|---|---|---|
|id|UUID|PK|
|wallet_address|VARCHAR|UNIQUE, NOT NULL|
|role|ENUM|NOT NULL|
|name|VARCHAR|NULL|
|bio|TEXT|NULL|
|avatar_url|TEXT|NULL|
|created_at|TIMESTAMP|NOT NULL|
|updated_at|TIMESTAMP|NOT NULL|

### Notes:

- wallet_address harus lowercase konsisten
    
- Role enum: `student`, `instructor`, `admin`
    
- Tidak menyimpan private key
    

---

## 10.4.2 courses

|Field|Type|Constraint|
|---|---|---|
|id|UUID|PK|
|creator_id|UUID|FK → users(id)|
|title|VARCHAR|NOT NULL|
|description|TEXT|NOT NULL|
|funding_target|NUMERIC|NOT NULL|
|funding_deadline|TIMESTAMP|NOT NULL|
|metadata_ipfs_hash|VARCHAR|NOT NULL|
|status|ENUM|NOT NULL|
|created_at|TIMESTAMP|NOT NULL|

### Status enum:

- draft
    
- funding_open
    
- funding_closed
    
- active
    
- completed
    
- cancelled
    

### Critical Rules:

- funding_target > 0
    
- funding_deadline > created_at
    
- creator_id harus role instructor/admin
    

---

## 10.4.3 enrollments

|Field|Type|Constraint|
|---|---|---|
|id|UUID|PK|
|user_id|UUID|FK → users|
|course_id|UUID|FK → courses|
|status|ENUM|NOT NULL|
|tx_hash|VARCHAR|NULL|
|enrolled_at|TIMESTAMP|NOT NULL|

### Status enum:

- pending
    
- confirmed
    
- failed
    
- cancelled
    

### Constraint:

UNIQUE(user_id, course_id)

Tujuan:

- User tidak bisa enroll dua kali
    

---

## 10.4.4 fundings

Agregasi funding per course.

|Field|Type|
|---|---|
|id|UUID|
|course_id|UUID (FK)|
|total_amount|NUMERIC|
|status|ENUM|
|updated_at|TIMESTAMP|

Status:

- open
    
- closed
    
- distributed
    

---

## 10.4.5 funding_transactions

Setiap kontribusi individu.

|Field|Type|Constraint|
|---|---|---|
|id|UUID|PK|
|funding_id|UUID|FK|
|user_id|UUID|FK|
|amount|NUMERIC|NOT NULL|
|tx_hash|VARCHAR|UNIQUE|
|block_number|BIGINT|NULL|
|status|ENUM|NOT NULL|
|created_at|TIMESTAMP|NOT NULL|

Status:

- pending
    
- confirmed
    
- failed
    

### Critical:

tx_hash UNIQUE untuk cegah double record.

---

## 10.4.6 course_progress

Tracking progress belajar.

|Field|Type|
|---|---|
|id|UUID|
|enrollment_id|UUID|
|progress_percent|INTEGER|
|last_accessed_at|TIMESTAMP|

Constraint:  
0 ≤ progress_percent ≤ 100

---

## 10.4.7 admin_logs

Audit trail admin.

|Field|Type|
|---|---|
|id|UUID|
|admin_id|UUID|
|action|VARCHAR|
|target_entity|VARCHAR|
|target_id|UUID|
|created_at|TIMESTAMP|

Tujuan:

- Accountability
    
- Trace perubahan kritikal
    

---

## 10.5 Data Integrity Rules (Non-Negotiable)

1. Tidak ada orphan record (FK enforced).
    
2. Tidak ada funding tanpa course valid.
    
3. Enrollment tidak boleh jika course status bukan active.
    
4. Funding tidak boleh jika status bukan open.
    
5. Semua transaksi blockchain harus punya tx_hash unik.
    

---

## 10.6 Indexing Strategy (Minimum)

Index wajib:

- users(wallet_address)
    
- courses(status)
    
- enrollments(user_id)
    
- funding_transactions(tx_hash)
    
- funding_transactions(user_id)
    
- funding_transactions(funding_id)
    

Tujuan:

- Query cepat
    
- Hindari full table scan
    

---

## 10.7 Soft Delete vs Hard Delete

Keputusan:

- User → soft delete (is_deleted flag)
    
- Course → soft delete
    
- Funding transaction → tidak boleh dihapus
    

Karena:

- Data finansial tidak boleh hilang
    
- Auditability penting
    

---

## 10.8 Data Migration Strategy

- Semua perubahan schema via migration tool
    
- Tidak ada manual change di production
    
- Migration harus reversible
    

---

## 10.9 Rekonsiliasi On-Chain vs Database

Potensi mismatch:

- Event gagal diproses
    
- Node downtime
    
- Reorg chain
    

Strategi:

1. Simpan block_number terakhir diproses
    
2. Periodic re-check event
    
3. Flag inconsistency untuk manual review
    

---

## 10.10 Data Growth Consideration

Estimasi pertumbuhan:

- funding_transactions paling cepat tumbuh
    
- enrollment juga besar
    

Solusi jangka panjang:

- Partition table funding_transactions
    
- Archive data lama
    
- Read replica untuk reporting
    

---

# Kenapa File Ini Kritis?

Jika skema salah:

- Logic jadi rumit
    
- Query lambat
    
- Refactor mahal
    
- Bug finansial bisa terjadi
    

Database adalah fondasi integritas, bukan sekadar penyimpanan.
