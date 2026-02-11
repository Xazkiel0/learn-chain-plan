
# 1. Role Users dalam Sistem

Pada MVP ini, sistem memiliki **4 role utama**:

1. **Guest**
    
2. **Pelajar (Student)**
    
3. **Pengajar (Teacher)**
    
4. **Admin (Platform Operator)**
    

Catatan penting:

- Semua role (kecuali Guest) adalah **User terdaftar + terhubung wallet**
    
- Sistem **tidak mengenal role ganda secara bebas**  
    (misalnya Teacher ≠ Student, kecuali secara eksplisit ditentukan di masa depan)
    

---

# 2. Deskripsi Tiap Role & Kegunaannya

## 2.1 Guest

### Deskripsi

Guest adalah **pengunjung publik** yang belum memiliki akun atau belum login.

### Tujuan Role

- Discovery & transparansi platform
    
- Memberikan kepercayaan awal (open ecosystem)
    

### Kegunaan

- Melihat semua course
    
- Melihat detail course (harga, syllabus, status crowdfund, pengajar)
    

Guest **tidak berinteraksi dengan blockchain**, tidak menyentuh dana, dan tidak memiliki state.

---

## 2.2 Pelajar (Student)

### Deskripsi

Pelajar adalah user yang mendaftar untuk **mengikuti course**, baik dengan:

- Pembayaran langsung, atau
    
- Melalui mekanisme **crowdfunding** (khusus pelajar yang ditandai “tidak mampu”)
    

### Tujuan Role

- Konsumsi konten edukasi
    
- Mendapat sertifikat on-chain
    
- Menjadi beneficiary crowdfunding (jika eligible)
    

### Kegunaan Utama

- Enroll course
    
- Mengikuti progres course
    
- Mengerjakan tugas & final task
    
- Mengajukan crowdfunding campaign (jika memenuhi syarat)
    
- Mencetak sertifikat berbasis blockchain
    

---

## 2.3 Pengajar (Teacher)

### Deskripsi

Pengajar adalah **penyedia course**, pemilik materi, dan penerima dana secara langsung dari enrollment.

### Tujuan Role

- Monetisasi keahlian
    
- Menyediakan course terstruktur
    
- Melakukan evaluasi akademik (khusus final task)
    

### Kegunaan Utama

- Membuat course
    
- Mengatur syllabus & konten
    
- Menentukan course:
    
    - Paid / Free
        
    - Crowdfundable / Non-crowdfundable
        
- Approve atau reject final task
    
- Menutup course (closed)
    

---

## 2.4 Admin (Platform)

### Deskripsi

Admin adalah **otoritas platform**, bukan participant akademik dan **tidak ikut transaksi course secara langsung**.

### Tujuan Role

- Governance
    
- Trust & compliance
    
- Moderasi dan kontrol abuse
    

### Kegunaan Utama

- Menentukan status “tidak mampu” pada pelajar
    
- Menonaktifkan user
    
- Moderasi platform (ban, suspend)
    

Catatan penting:  
Admin **tidak boleh menyentuh dana user** dan **tidak boleh mengubah data akademik (progress, kelulusan)**.

---

# 3. Kuasa & Ability Tiap Role

Bagian ini penting karena menjadi dasar:

- Authorization
    
- Smart contract permission
    
- Backend access control
    

---

## 3.1 Guest

**Abilities**

- Read-only access ke course & detail course
    

**Tidak Memiliki Kuasa**

- Tidak bisa login
    
- Tidak bisa connect wallet
    
- Tidak bisa enroll
    
- Tidak bisa bertransaksi
    

---

## 3.2 Pelajar (Student)

**Abilities**

- Register & login
    
- Connect wallet
    
- Enroll course (jika course open)
    
- Mengikuti progress course
    
- Submit tugas
    
- Submit final task
    
- Mengklaim sertifikat jika course selesai
    
- Membuat crowdfunding campaign **(hanya jika ditandai “tidak mampu”)**
    
- Menarik dana crowdfunding jika campaign gagal
    
- Menyetujui eksekusi crowdfunding (fund now)
    

**Kuasa Finansial**

- Dana milik pelajar hanya:
    
    - Saat sebelum enroll
        
    - Saat crowdfunding gagal
        
- Saat enroll / fund executed → **tidak bisa dibatalkan**
    

---

## 3.3 Pengajar (Teacher)

**Abilities**

- Create & manage course
    
- Set harga course
    
- Set course crowdfundable / tidak
    
- Approve final task
    
- Menutup course
    

**Kuasa Finansial**

- Menerima dana enroll langsung ke wallet
    
- Tidak bisa:
    
    - Mengambil dana crowdfund sebelum executed
        
    - Mengubah harga course yang sedang berjalan
        

---

## 3.4 Admin

**Abilities**

- Set status user (active / inactive)
    
- Set pelajar sebagai “tidak mampu”
    
- Ban user
    

**Batasan Kuasa (Sangat Penting)**

- Tidak bisa:
    
    - Mengambil dana
        
    - Mengubah progress course
        
    - Mengeluarkan sertifikat
        
    - Mengubah hasil akademik
        

Ini krusial untuk **trust model Web3**.

---

# 4. Restriction & Allowed Scope

Bagian ini sering dilupakan, tapi **penting untuk mencegah ambiguity dan exploit**.

---

## 4.1 Restriction Umum

- Semua transaksi **wajib wallet-connected**
    
- Tidak ada custodial wallet
    
- Tidak ada admin override terhadap dana
    
- Tidak ada manual progress override
    
- Campaign tidak bisa dibuat bebas (menempel ke Course + Student)
    

---

## 4.2 Restriction Pelajar

- Tidak bisa enroll course closed
    
- Tidak bisa membuat campaign jika:
    
    - Tidak ditandai “tidak mampu”
        
    - Course tidak crowdfundable
        
- Tidak bisa klaim sertifikat tanpa:
    
    - Progress 100%
        
    - Final task approved
        

---

## 4.3 Restriction Pengajar

- Tidak bisa mengubah course setelah closed
    
- Tidak bisa approve final task sebelum progress 100%
    
- Tidak bisa menarik dana crowdfund secara manual
    

---

## 4.4 Restriction Admin

- Tidak bisa:
    
    - Memicu eksekusi crowdfund
        
    - Mengubah state campaign
        
    - Menyetujui kelulusan pelajar
        

Admin hanya **governance, bukan operator transaksi**.

---

# 5. Tambahan Penting (Wajib Ada di Dokumentasi)

Saya sarankan kamu **menambahkan 3 bagian ini** ke dokumentasi:

---

## 5.1 Trust & Responsibility Model

Menjelaskan:

- Siapa bertanggung jawab atas apa
    
- Apa yang irreversible (on-chain)
    
- Apa yang off-chain dan bisa diperbaiki
    

---

## 5.2 State Machine (Conceptual)

Contoh:

- Course state: `draft → open → closed`
    
- Campaign state: `pending → target_reached → executed`
    
- Enrollment state: `enrolled → in_progress → completed`
    

Ini **penting untuk backend + smart contract sync**.

---

## 5.3 Explicit Non-Goals (Anti Scope Creep)

Misalnya:

- Tidak ada secondary market NFT
    
- Tidak ada speculative trading
    
- Tidak ada lending/borrowing