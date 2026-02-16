## 12.1 Tujuan File Ini

File ini mendefinisikan:

- Security minimum yang wajib ada
    
- Proteksi data & wallet
    
- Strategi pencegahan abuse
    
- Logging & audit trail
    
- Error handling strategy sistemik
    
- Incident response dasar
    

Dokumen ini bukan tambahan.  
Ini adalah lapisan proteksi inti.

---

## 12.2 Security Philosophy

Prinsip dasar:

1. **Assume breach**  
    Sistem harus siap jika sesuatu gagal.
    
2. **Minimize trust surface**  
    Blockchain untuk trust-critical logic.
    
3. **Least privilege**  
    Setiap role hanya punya akses minimum.
    
4. **Fail safely**  
    Jika ragu, tolak request.
    

---

## 12.3 Authentication Security

### 12.3.1 Wallet Signature Flow

Keamanan minimum:

- Nonce harus:
    
    - Unique
        
    - Expire (misal 5 menit)
        
    - One-time use
        
- Verifikasi signature server-side
    
- Jangan pernah menyimpan private key
    

Jika nonce tidak expire → replay attack bisa terjadi.

---

### 12.3.2 JWT Security

- Short expiry (misal 1–2 jam)
    
- Refresh token opsional (MVP bisa tanpa refresh)
    
- Disimpan di HTTP-only cookie (lebih aman dari localStorage)
    
- Token harus diverifikasi di setiap request
    

---

## 12.4 Authorization & Access Control

Semua endpoint protected via:

- Auth middleware
    
- Role guard
    

Critical checks:

- Instructor hanya bisa edit course miliknya
    
- Student tidak bisa mengakses admin endpoint
    
- Funding tidak bisa dilakukan jika status closed
    

Tidak boleh hanya bergantung pada frontend check.

---

## 12.5 Input Validation & Injection Prevention

Semua input harus:

- Type validated
    
- Sanitized
    
- Length limited
    
- Pattern checked
    

Proteksi terhadap:

- SQL Injection (ORM + parameterized query)
    
- XSS (escape output)
    
- CSRF (gunakan same-site cookie atau CSRF token)
    

---

## 12.6 Rate Limiting & Abuse Prevention

Minimal:

- Auth endpoint: rate limit per IP
    
- Funding attempt: limit per wallet
    
- Course creation: limit per account
    

Tujuan:

- Hindari brute force
    
- Hindari spam
    
- Hindari bot abuse
    

---

## 12.7 Blockchain-Specific Security

### 12.7.1 Smart Contract Security

Minimal:

- Gunakan library standar (misalnya OpenZeppelin)
    
- Hindari reentrancy
    
- Validasi semua input
    
- Gunakan modifier untuk role check
    
- Audit internal sebelum deploy mainnet
    

Risiko umum:

- Reentrancy
    
- Integer overflow
    
- Incorrect access control
    
- Logic bug distribusi dana
    

---

### 12.7.2 Event Handling Security

Backend listener harus:

- Idempotent
    
- Verifikasi tx_hash valid
    
- Pastikan event dari contract address resmi
    
- Simpan block number
    

Jika tidak → fake event bisa diproses.

---

## 12.8 Data Privacy

Data yang dianggap sensitif:

- Wallet address (masih pseudo-anonymous)
    
- Profile data
    
- Funding history
    

Kebijakan minimum:

- Jangan expose email jika ada
    
- Jangan expose internal ID
    
- Jangan expose admin metadata
    

Semua response harus whitelist field, bukan blacklist.

---

## 12.9 Error Handling Strategy (System-Level)

### 12.9.1 Principle

Error harus:

- Terstruktur
    
- Tidak bocorkan internal detail
    
- Bisa dilacak
    
- Bisa di-reproduce
    

---

### 12.9.2 Error Categories

1. User error (4xx)
    
2. System error (5xx)
    
3. Blockchain error
    
4. Validation error
    
5. Authorization error
    

---

### 12.9.3 Centralized Error Handler

Backend harus memiliki:

- Global exception handler
    
- Mapping error internal → error code publik
    
- Logging otomatis untuk 5xx
    

---

## 12.10 Logging Strategy

Log minimal:

- Auth attempts
    
- Funding transaction
    
- Enrollment confirmation
    
- Admin action
    
- Failed blockchain sync
    
- 5xx error
    

Log harus menyimpan:

- user_id (jika ada)
    
- endpoint
    
- timestamp
    
- tx_hash (jika relevan)
    

Log tidak boleh menyimpan:

- Signature
    
- Private key
    
- Token mentah
    

---

## 12.11 Monitoring & Alerting (Minimum)

Alert jika:

- 5xx spike
    
- Blockchain listener berhenti
    
- Funding mismatch
    
- Database connection error
    

MVP cukup:

- Basic log monitoring
    
- Email/Slack alert sederhana
    

---

## 12.12 Incident Handling (Basic Procedure)

Jika terjadi insiden:

1. Freeze action (misal disable funding endpoint)
    
2. Identifikasi scope
    
3. Audit log
    
4. Patch
    
5. Dokumentasi insiden
    

Semua insiden harus dicatat.

---

## 12.13 Backup Strategy

- Database backup harian
    
- Retention minimal 7–14 hari
    
- Test restore secara periodik
    

Tanpa test restore → backup tidak berguna.

---

## 12.14 Secure Deployment Practices

- ENV variable untuk secret
    
- Tidak commit private key
    
- HTTPS wajib
    
- Disable debug mode di production
    
- Production DB tidak boleh diakses publik
    

---

## 12.15 Security Non-Negotiables

1. Tidak deploy contract tanpa review.
    
2. Tidak expose admin endpoint tanpa guard.
    
3. Tidak log sensitive raw token.
    
4. Tidak bypass validation untuk “cepat”.
    

---

## 12.16 Known Risk Areas

- Smart contract bug
    
- Wallet UX confusion
    
- Event desync
    
- Race condition funding
    

Mitigasi sudah didefinisikan di file sebelumnya.

---

# Kenapa File Ini Vital?

Karena:

- Sistem menyentuh dana.
    
- Web3 irreversibel.
    
- Reputasi sangat rapuh.
    

Satu insiden → trust hilang.