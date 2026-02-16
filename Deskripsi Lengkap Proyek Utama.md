### Web-Based Learning Platform (Web2.5 – Hybrid Web2 + Web3)

Proyek ini adalah **platform pembelajaran digital berbasis web** yang menghubungkan **pengajar (teacher)** dan **pelajar (student)** dalam sebuah ekosistem edukasi yang **transparan, non-kustodial, dan berbasis kepercayaan (trust)**.  
Platform ini menggabungkan pendekatan **Web2 untuk pengalaman pengguna dan manajemen sistem**, serta **Web3 untuk transparansi finansial dan sertifikasi immutable**, tanpa membebani pengguna dengan kompleksitas blockchain.

---

## Masalah yang Diselesaikan

Platform ini dirancang untuk menjawab tiga masalah utama dalam sistem pembelajaran digital saat ini:

1. **Akses pendidikan bagi pelajar yang terkendala finansial**  
    Banyak pelajar memiliki motivasi belajar tetapi tidak memiliki kemampuan finansial untuk membeli course berkualitas. Sistem crowdfunding konvensional sering kali tidak transparan atau tidak terhubung langsung dengan produk edukasi yang diikuti.
    
2. **Monetisasi yang adil dan langsung bagi pengajar**  
    Pada banyak platform, dana pembayaran course mengendap di sistem platform (custodial), menimbulkan risiko kepercayaan, keterlambatan pembayaran, dan ketergantungan pada pihak ketiga.
    
3. **Kurangnya trust terhadap sertifikat digital**  
    Sertifikat course sering kali mudah dipalsukan, tidak dapat diverifikasi secara publik, dan tidak memiliki nilai jangka panjang.
    

---

## Solusi yang Ditawarkan

Platform ini menawarkan **sistem pembelajaran Web2.5** dengan karakteristik utama sebagai berikut:

### 1. Marketplace Course Terdesentralisasi Secara Finansial

- Pengajar dapat membuat dan mempublikasikan course.
    
- Course dapat bersifat:
    
    - **Closed / Paid langsung**, atau
        
    - **Crowdfundable**, khusus untuk pelajar yang dikategorikan “tidak mampu”.
        
- Semua pembayaran course dilakukan melalui **wallet kriptokurensi pengguna**, tanpa dana mengendap di platform.
    

---

### 2. Crowdfunding Edukasi yang Terkontrol

- Crowdfunding **bukan bebas**, melainkan:
    
    - selalu terikat pada **1 course dan 1 pelajar**,
        
    - hanya dapat diakses oleh pelajar dengan status **scholarship / tidak mampu** yang ditetapkan admin.
        
- Dana crowdfunding:
    
    - disimpan di **smart contract vault**,
        
    - transparan dan dapat diaudit,
        
    - dapat ditarik kembali oleh funder jika target tidak tercapai.
        
- Campaign memiliki state yang jelas:
    
    - `pending` → dana terkumpul belum mencapai target,
        
    - `target_reached` → target tercapai, menunggu eksekusi,
        
    - `executed` → dana dialirkan ke pengajar dan course dapat diikuti.
        

---

### 3. Pembayaran Non-Kustodial dan Transparan

- Saat enrollment atau eksekusi crowdfunding:
    
    - **99% dana langsung masuk ke wallet pengajar**,
        
    - **1% fee otomatis masuk ke wallet perusahaan**.
        
- Platform **tidak menyimpan dana user** dalam bentuk apa pun.
    
- Blockchain digunakan sebagai **single source of truth** untuk transaksi finansial.
    

---

### 4. Sistem Pembelajaran dan Progress Terverifikasi

- Pelajar yang sudah enroll mengikuti course melalui sistem Web2:
    
    - progress belajar dihitung oleh sistem (modul, materi, aktivitas),
        
    - tugas akhir memerlukan **approval dari pengajar**.
        
- Course dianggap selesai jika:
    
    - progress mencapai 100%, dan
        
    - tugas akhir disetujui oleh pengajar.
        

---

### 5. Sertifikat Immutable Berbasis Blockchain

- Setelah course selesai, sistem menerbitkan sertifikat digital.
    
- Sertifikat tidak berupa NFT komersial, melainkan:
    
    - **hash + metadata yang dicatat di blockchain**.
        
- Sertifikat:
    
    - tidak dapat diubah,
        
    - dapat diverifikasi publik,
        
    - selalu terikat ke enrollment dan course tertentu,
        
    - tidak bersifat spekulatif atau transferable.
        

---

## Peran Pengguna dalam Sistem

Pada MVP ini, sistem memiliki **4 role utama**:

1. **Guest**
2. **Pelajar (Student)**
3. **Pengajar (Teacher)**
4. **Admin (Platform Operator)**

Catatan penting:

- Semua role (kecuali Guest) adalah **User terdaftar + terhubung wallet**
- Sistem **tidak mengenal role ganda secara bebas**  
  (misalnya Teacher ≠ Student, kecuali secara eksplisit ditentukan di masa depan)

### Guest

- Melihat semua course dan detail course.
    
- Registrasi dan login.
    
- Menghubungkan wallet.

Catatan:

- Guest adalah **pengunjung publik** yang belum memiliki akun atau belum login.
- Guest **tidak berinteraksi dengan blockchain**, tidak menyentuh dana, dan tidak memiliki state.
- Registrasi/login dan menghubungkan wallet adalah langkah untuk menjadi **User terdaftar** (mis. Pelajar/Pengajar/Admin), bukan kemampuan Guest saat masih berada pada status Guest.

Tujuan Role:

- Discovery & transparansi platform
- Memberikan kepercayaan awal (open ecosystem)

Kegunaan:

- Melihat semua course
- Melihat detail course (harga, syllabus, status crowdfund, pengajar)
    

### Pelajar (Student)

- Enroll dan mengikuti course.
    
- Mengajukan crowdfunding untuk course tertentu (jika status scholarship aktif).
    
- Melihat progress pembelajaran.
    

Tambahan:

- Pelajar mengikuti course melalui progres Web2, dan **final task memerlukan approval pengajar**.
- Crowdfunding untuk pelajar bersifat terkontrol: hanya untuk pelajar yang ditetapkan admin sebagai **“tidak mampu”**.
- Mengklaim sertifikat setelah course selesai.

Tujuan Role:

- Konsumsi konten edukasi
- Mendapat sertifikat on-chain
- Menjadi beneficiary crowdfunding (jika eligible)
    

### Pengajar (Teacher)

- Membuat dan mengelola course.
    
- Menentukan apakah course dapat dicrowdfund.
    
- Menutup course dari enrollment baru.

Tambahan:

- Pengajar adalah **penerima dana langsung** dari enrollment/eksekusi crowdfunding (non-kustodial).
- Pengajar dapat menentukan course:
  - Paid / Free
  - Crowdfundable / Non-crowdfundable
- Mengatur syllabus & konten
    
- Menilai dan menyetujui tugas akhir.
    

### Admin

- Menetapkan status pelajar sebagai “tidak mampu”.
    
- Menonaktifkan atau memblokir user.
    
- Menjaga integritas dan keamanan ekosistem.
    

Catatan penting:

- Admin adalah **otoritas platform**, bukan participant akademik dan **tidak ikut transaksi course secara langsung**.
- Admin **tidak boleh menyentuh dana user** dan **tidak boleh mengubah data akademik** (progress, kelulusan).

Tujuan Role:

- Governance
- Trust & compliance
- Moderasi dan kontrol abuse

## Kuasa & Ability Tiap Role

Bagian ini menjadi dasar:

- Authorization
- Smart contract permission
- Backend access control

### Guest

**Abilities**

- Read-only access ke course & detail course

**Tidak Memiliki Kuasa**

- Tidak bisa login
- Tidak bisa enroll
- Tidak bisa connect wallet
- Tidak bisa bertransaksi

### Pelajar (Student)

**Abilities**

- Register & login
- Connect wallet
- Enroll course (jika course open)
- Mengikuti progress course
- Submit tugas
- Submit final task
- Mengklaim sertifikat jika course selesai
- Membuat crowdfunding campaign (hanya jika ditandai “tidak mampu”)
- Menarik dana crowdfunding jika campaign gagal
- Menyetujui eksekusi crowdfunding (fund now)

**Kuasa Finansial**

- Dana milik pelajar hanya:
  - Saat sebelum enroll
  - Saat crowdfunding gagal
- Saat enroll / fund executed → **tidak bisa dibatalkan**

### Pengajar (Teacher)

**Abilities**

- Create & manage course
- Set harga course
- Set course crowdfundable / tidak
- Approve atau reject final task
- Menutup course

**Kuasa Finansial**

- Menerima dana enroll langsung ke wallet
- Tidak bisa:
  - Mengambil dana crowdfund sebelum executed
  - Mengubah harga course yang sedang berjalan

### Admin

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

## Restriction & Allowed Scope

Bagian ini penting untuk mencegah ambiguity dan exploit.

### Restriction Umum

- Semua transaksi **wajib wallet-connected**
- Tidak ada custodial wallet
- Tidak ada admin override terhadap dana
- Tidak ada manual progress override
- Campaign tidak bisa dibuat bebas (menempel ke Course + Student)

### Restriction Pelajar

- Tidak bisa enroll course closed
- Tidak bisa membuat campaign jika:
  - Tidak ditandai “tidak mampu”
  - Course tidak crowdfundable
- Tidak bisa klaim sertifikat tanpa:
  - Progress 100%
  - Final task approved

### Restriction Pengajar

- Tidak bisa mengubah course setelah closed
- Tidak bisa approve final task sebelum progress 100%
- Tidak bisa menarik dana crowdfund secara manual

### Restriction Admin

- Tidak bisa:
  - Memicu eksekusi crowdfund
  - Mengubah state campaign
  - Menyetujui kelulusan pelajar

Admin hanya **governance, bukan operator transaksi**.
Catatan (lanjutan peran Admin): Menonaktifkan atau memblokir user.
    

## Pendekatan Teknologi (Web2.5)

- **Web2** digunakan untuk:
    
    - autentikasi,
        
    - manajemen user dan course,
        
    - progress pembelajaran,
        
    - UI/UX dan pengalaman pengguna.
        
- **Web3** digunakan secara selektif untuk:
    
    - crowdfunding vault (smart contract),
        
    - alur dana non-kustodial,
        
    - pencatatan hash sertifikat.
        

Pendekatan ini menjaga **user experience tetap sederhana**, sambil memberikan **jaminan trust dan transparansi** di aspek kritikal.

---

## Batasan MVP (Disengaja)

Untuk menjaga fokus dan keterjangkauan pengembangan oleh solo full-stack developer, sistem ini **tidak mencakup**:

- DAO dan voting governance,
    
- konversi kripto ke fiat,
    
- KYC atau verifikasi dokumen kompleks,
    
- course korporat atau enterprise,
    
- sistem delegasi pengawas crowdfunding.

- secondary market NFT
- speculative trading
- lending/borrowing
    

Semua fitur tersebut direncanakan sebagai **post-MVP extension**, bukan bagian dari fondasi awal.

---

## Trust & Responsibility Model

Bagian ini menjelaskan:

- Siapa bertanggung jawab atas apa (platform, pengajar, pelajar, funder)
- Apa yang irreversible (on-chain) vs apa yang off-chain dan bisa diperbaiki
- Konsekuensi dari transaksi on-chain yang tidak dapat dibatalkan

---

## State Machine (Conceptual)

Contoh state utama yang perlu konsisten antara backend dan smart contract:

- Course state: `draft → open → closed`
- Campaign state: `pending → target_reached → executed`
- Enrollment state: `enrolled → in_progress → completed`

---

## Explicit Non-Goals (Anti Scope Creep)

Untuk menjaga scope MVP tetap fokus, sistem tidak menargetkan:

- Secondary market untuk sertifikat
- Fitur spekulatif/trading
- Lending/borrowing
- AI Course Assistant
