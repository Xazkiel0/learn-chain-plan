## 11.1 Tujuan File Ini

File ini mengunci:

- Prinsip desain UI/UX
    
- Struktur halaman utama
    
- Aturan komponen
    
- Pola interaksi Web3
    
- Validasi & feedback error
    

Frontend bukan hanya “tampilan”, tetapi lapisan:

- Validasi awal
    
- Orkestrasi wallet
    
- Pengendalian state transaksi
    
- Pengurangan friction user
    

---

## 11.2 Prinsip UI/UX Utama

### 1. Clarity Over Decoration

- Fokus pada informasi penting
    
- Hindari visual noise
    
- Prioritaskan status (funding, enrollment, transaction)
    

---

### 2. Explicit State Communication

Karena ini Web3, state harus selalu jelas:

- Loading
    
- Waiting wallet signature
    
- Transaction pending
    
- Transaction confirmed
    
- Failed
    

User tidak boleh menebak apa yang sedang terjadi.

---

### 3. Prevent Irreversible Mistake

Untuk aksi kritikal:

- Funding
    
- Withdraw
    
- Cancel course
    

Harus ada:

- Confirmation modal
    
- Ringkasan detail sebelum confirm
    
- Warning eksplisit
    

---

### 4. Deterministic Interaction

User harus tahu:

- Klik ini → hasil apa
    
- Gagal → kenapa
    
- Berapa lama menunggu
    

Tidak boleh ada “silent failure”.

---

## 11.3 Struktur Halaman Utama

### 1. Public Pages

- Landing Page
    
- Browse Courses
    
- Course Detail
    
- Instructor Profile
    

---

### 2. Authenticated Pages

- Dashboard (Student)
    
- Dashboard (Instructor)
    
- My Courses
    
- My Funding
    
- Admin Panel
    

---

### 3. Transaction-Oriented Screens

- Funding Modal
    
- Enrollment Confirmation
    
- Transaction Status Screen
    

---

## 11.4 Layout Structure

Struktur dasar:

```
<AppLayout>
 ├── Navbar
 ├── Main Content
 └── Footer
```

Untuk dashboard:

```
<DashboardLayout>
 ├── Sidebar
 ├── Header
 └── Content Area
```

Guideline:

- Max width container konsisten
    
- Spacing system konsisten
    
- Typography hierarchy jelas
    

---

## 11.5 Component Design Rules

### 11.5.1 Button Rules

Primary:

- Aksi utama halaman
    

Secondary:

- Aksi alternatif
    

Danger:

- Aksi irreversible
    

Loading state wajib:

- Disable button
    
- Spinner
    
- Prevent double click
    

---

### 11.5.2 Form Rules

Setiap form harus memiliki:

- Label jelas
    
- Required indicator
    
- Inline validation
    
- Error message spesifik
    
- Disabled state saat submit
    

Tidak boleh hanya:

> “Something went wrong”

---

### 11.5.3 Modal Rules

Modal digunakan untuk:

- Konfirmasi transaksi
    
- Wallet interaction
    
- Detail penting
    

Modal tidak boleh:

- Digunakan untuk konten panjang
    
- Menggantikan halaman penuh
    

---

## 11.6 Web3 Interaction UX Pattern

Web3 UX adalah titik paling riskan.

### Standard Flow:

1. User klik “Fund”
    
2. Modal tampil:
    
    - Amount
        
    - Estimated gas
        
    - Final amount
        
3. User confirm
    
4. Wallet popup
    
5. UI masuk state:
    
    - “Waiting for confirmation…”
        
6. Setelah broadcast:
    
    - “Transaction submitted”
        
7. Setelah event confirmed:
    
    - “Funding successful”
        

Semua state harus visible.

---

## 11.7 Error Handling di UI

### 1. Validation Error

Ditampilkan inline.

Contoh:

- “Amount must be greater than 0”
    
- “Funding target exceeded”
    

---

### 2. Blockchain Error

Mapping error:

|Blockchain Issue|UI Message|
|---|---|
|User reject|“Transaction cancelled”|
|Insufficient gas|“Insufficient balance for gas”|
|Revert|“Transaction failed”|

---

### 3. Backend Error

Response error code harus dipetakan ke pesan user-friendly.

Tidak boleh menampilkan raw internal error.

---

## 11.8 State Management Strategy

State dibagi menjadi:

### 1. Server State

- Course list
    
- Funding status
    
- Enrollment status
    

Menggunakan:

- React Query / SWR
    

---

### 2. Client State

- Modal open/close
    
- Form value
    
- Wallet connection state
    

Gunakan:

- Local state / Zustand (jika kompleks)
    

---

## 11.9 Loading & Skeleton Rules

Untuk halaman data:

- Gunakan skeleton loader
    
- Jangan gunakan spinner kosong untuk seluruh halaman
    

Tujuan:

- Perceived performance lebih baik
    

---

## 11.10 Accessibility Minimum

- Button bisa diakses keyboard
    
- Label terkait input
    
- Kontras warna cukup
    
- Error message terbaca screen reader
    

MVP tidak perlu perfect WCAG compliance, tapi tidak boleh mengabaikan aksesibilitas dasar.

---

## 11.11 Responsiveness

Breakpoints minimal:

- Mobile
    
- Tablet
    
- Desktop
    

Prinsip:

- Mobile-first
    
- Dashboard tetap usable di tablet
    
- Funding flow tetap jelas di layar kecil
    

---

## 11.12 Design Consistency Rules

- Warna status konsisten:
    
    - Green → success
        
    - Yellow → pending
        
    - Red → failed
        
- Icon tidak campur library berbeda
    
- Spacing mengikuti sistem 4px/8px grid
    

---

## 11.13 Non-Goals (MVP)

- Animasi kompleks
    
- Theme customization
    
- Multi-language
    
- Dark mode (opsional nanti)
    

---

## 11.14 Anti-Pattern yang Harus Dihindari

- Disable button tanpa penjelasan
    
- Double submit transaction
    
- Auto refresh yang mengganggu
    
- Hard reload setelah transaksi
    

---

# Kenapa File Ini Penting?

Karena:

- Web3 sudah punya friction alami.
    
- Jika UI buruk, user akan menganggap sistem scam.
    
- Error UX lebih merusak reputasi daripada bug minor.
    

Frontend bukan kosmetik.  
Frontend adalah lapisan kepercayaan.
