## 9.1 Tujuan File Ini

File ini mendefinisikan:

- Kontrak komunikasi antara frontend dan backend
    
- Standar desain endpoint
    
- Mekanisme autentikasi & otorisasi
    
- Format response & error
    
- Prinsip konsistensi API
    

Dokumen ini **mengunci ekspektasi perilaku sistem**, sehingga:

- Frontend tidak menebak-nebak response
    
- Backend tidak berubah tanpa kontrol
    
- Refactor tidak merusak integrasi
    

---

## 9.2 API Design Principles

Semua endpoint mengikuti prinsip berikut:

### 1. RESTful & Predictable

- Resource-based URL
    
- HTTP method sesuai semantik
    

|Method|Fungsi|
|---|---|
|GET|Ambil data|
|POST|Buat data|
|PUT|Update penuh|
|PATCH|Update sebagian|
|DELETE|Hapus|

---

### 2. Stateless

- Tidak ada session server
    
- Auth menggunakan token (JWT / wallet signature)
    
- Semua request membawa kredensial sendiri
    

---

### 3. Versioned API

Format:

```
/api/v1/...
```

Tujuan:

- Perubahan breaking tidak merusak client lama
    
- Mudah migrasi versi
    

---

### 4. Consistent Response Format

Semua response harus berbentuk:

```json
{
  "success": true,
  "data": {},
  "error": null,
  "meta": {}
}
```

Jika error:

```json
{
  "success": false,
  "data": null,
  "error": {
    "code": "COURSE_NOT_FOUND",
    "message": "Course does not exist"
  },
  "meta": {}
}
```

---

## 9.3 Authentication & Authorization

Sistem mendukung 2 model auth:

---

### 9.3.1 Wallet-Based Authentication (Primary)

Flow:

1. User connect wallet
    
2. Backend kirim nonce
    
3. User sign nonce
    
4. Backend verifikasi signature
    
5. Backend generate JWT
    

JWT digunakan untuk semua request berikutnya.

Tujuan:

- Hindari simpan private key
    
- Proof-of-ownership wallet
    

---

### 9.3.2 Role-Based Authorization

Role minimal:

- `student`
    
- `instructor`
    
- `admin`
    

Authorization rule example:

|Endpoint|Student|Instructor|Admin|
|---|---|---|---|
|Create course|❌|✅|✅|
|Enroll course|✅|❌|✅|
|Approve funding|❌|❌|✅|

Semua role dicek di middleware.

---

## 9.4 Core API Modules

Struktur modul backend:

- Auth
    
- Users
    
- Courses
    
- Enrollment
    
- Funding
    
- Admin
    
- Webhook / Blockchain Listener
    

---

## 9.5 Endpoint Design — Core Resources

---

## 9.5.1 Auth

### POST `/api/v1/auth/nonce`

Generate nonce untuk wallet.

Response:

```json
{
  "nonce": "random-string"
}
```

---

### POST `/api/v1/auth/verify`

Verifikasi signature dan return JWT.

Body:

```json
{
  "walletAddress": "0x...",
  "signature": "0x..."
}
```

Response:

```json
{
  "token": "jwt-token"
}
```

---

## 9.5.2 Users

### GET `/api/v1/users/me`

Return profile user login.

---

### PATCH `/api/v1/users/me`

Update profile:

- name
    
- bio
    
- avatar
    

---

## 9.5.3 Courses

### GET `/api/v1/courses`

Query params:

- page
    
- limit
    
- search
    
- status
    

---

### GET `/api/v1/courses/:id`

Return detail course + funding info.

---

### POST `/api/v1/courses`

Role: instructor/admin

Body:

- title
    
- description
    
- fundingTarget
    
- duration
    
- metadataIPFSHash
    

---

### PATCH `/api/v1/courses/:id`

Hanya creator atau admin.

---

## 9.5.4 Enrollment

### POST `/api/v1/courses/:id/enroll`

Flow:

1. Backend validasi
    
2. Frontend trigger smart contract
    
3. Backend listen event
    
4. Update status enrollment
    

Enrollment status:

- pending
    
- confirmed
    
- failed
    

---

## 9.5.5 Funding

### POST `/api/v1/courses/:id/fund`

Trigger funding intent (off-chain record).

On-chain execution dilakukan via frontend wallet.

---

### GET `/api/v1/courses/:id/funding`

Return:

- total funded
    
- target
    
- progress %
    
- list contributors (optional)
    

---

## 9.6 Blockchain Event Handling

Backend memiliki event listener:

- Listen smart contract event:
    
    - Funded
        
    - Enrolled
        
    - CourseCompleted
        

Flow:

1. Event terdeteksi
    
2. Validasi data
    
3. Update database
    
4. Idempotent check (anti double-processing)
    

---

## 9.7 Error Handling Strategy

### 1. Standard Error Codes

Contoh:

|Code|Meaning|
|---|---|
|UNAUTHORIZED|Token invalid|
|FORBIDDEN|Role tidak cukup|
|VALIDATION_ERROR|Input salah|
|COURSE_NOT_FOUND|Tidak ada|
|FUNDING_CLOSED|Sudah ditutup|

---

### 2. HTTP Status Mapping

|HTTP|Condition|
|---|---|
|200|OK|
|201|Created|
|400|Validation error|
|401|Unauthorized|
|403|Forbidden|
|404|Not found|
|409|Conflict|
|500|Internal error|

---

## 9.8 Pagination Standard

Query:

```
?page=1&limit=10
```

Response meta:

```json
"meta": {
  "page": 1,
  "limit": 10,
  "total": 125,
  "totalPages": 13
}
```

---

## 9.9 Idempotency & Safety

Untuk endpoint sensitif (funding):

- Gunakan idempotency key header
    
- Cegah double record
    
- Database constraint untuk mencegah duplikasi
    

---

## 9.10 Validation Layer

Semua input divalidasi:

- Type check
    
- Required field
    
- Business rule check
    
- Sanitization
    

Tidak boleh ada data mentah masuk database.

---

## 9.11 Rate Limiting (Minimum)

Untuk mencegah abuse:

- Auth endpoint rate limited
    
- Funding endpoint limited per address
    
- IP throttling basic
    

---

## 9.12 Non-Goals (Agar Tidak Over-Engineering)

- Tidak membuat GraphQL di MVP
    
- Tidak membuat microservices
    
- Tidak membuat event bus kompleks
    

Single modular backend sudah cukup.

---

# Kenapa File Ini Penting?

Tanpa API contract yang tegas:

- Frontend dan backend akan drift
    
- Debugging akan mahal
    
- Refactor berisiko tinggi
    

API adalah **fondasi integrasi**.
