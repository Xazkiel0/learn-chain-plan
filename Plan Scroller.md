Saya akan menjawab **sebagai full-stack + project manager** dengan pendekatan **objektif, sistemik, dan bisa langsung dipakai di dunia nyata**.  
Fokusnya: **menghilangkan ambiguity, overlap scope, dan wasted effort**.

---


---

# A. MANAJEMEN TIM DAN DIVISI

## A.1. Prinsip Dasar (ini fondasi, jangan dilewati)
Sebelum bicara urutan kerja, ada **3 prinsip manajerial** yang wajib dipenuhi:

1. **Single Source of Truth (SSOT)**  
    Semua divisi mengacu ke artefak yang sama (dokumen, diagram, data model).
    
2. **Downstream–Upstream Discipline**  
    Divisi downstream _tidak_ menebak-nebak kerja upstream.  
    Kalau upstream belum selesai → downstream **blocked secara resmi**, bukan improvisasi.
    
3. **Scope is Owned, Not Shared**  
    Setiap output **punya satu owner**. Kolaborasi boleh, kepemilikan tidak.
    

Kalau tiga ini gagal, pembagian seindah apa pun tetap chaos.

---

## A.2. Reframing: Nama Divisi Profesional (Real World)
Saya rapikan dan **rename** supaya sesuai praktik industri.

|Kode|Nama Divisi|
|---|---|
|A|**Business & System Analysis (BSA)**|
|B|**Data Architecture & Governance (DAG)**|
|C|**System Design & Process Engineering (SDPE)**|
|D|**Project Management Office (PMO)**|
|E|**Knowledge & Resource Management (KRM)**|
|F|**Product Planning & Delivery (PPD)**|
|G|**Backend Engineering (BE)**|
|H|**UI/UX & Product Design (UX)**|
|I|**Frontend Engineering (FE)**|
|J|**Quality Control & Assurance (QA/QC)**|
|K|**DevOps & Platform Engineering (DPE)**|

> Catatan kritis:  
> **PMO bukan sekadar admin timeline**, tapi pengendali scope & dependency.

---

## A.3. Urutan Kerja yang Benar (End-to-End Flow)
### A.3.a. FASE 1 — DEFINISI & KEJELASAN (NO CODE)
#### A.3.a.i. Business & System Analysis (BSA)
**Output wajib (tidak boleh lompat):**

- Business objectives
    
- Stakeholder map
    
- Business process high-level
    
- Data requirement per divisi
    
- Non-functional requirements (security, scalability, compliance)
    

📦 Artefak:

- Business Requirement Document (BRD)
    
- System Requirement Specification (SRS)
    

➡️ **Tanpa ini, semua divisi lain tidak boleh jalan.**

---

#### A.3.a.ii. Data Architecture & Governance (DAG)
**Tugas utama:**

- Normalisasi data
    
- Penentuan _data ownership_
    
- Data classification (public / internal / restricted)
    
- Master data vs transactional data
    

📦 Artefak:

- ERD
    
- Data Dictionary
    
- Data Access Matrix (divisi vs data)
    

➡️ Ini **mengunci kebingungan data antar divisi**.

---

#### A.3.a.iii. System Design & Process Engineering (SDPE)
**Mengikat logika sistem**

- Flow bisnis
    
- Flow data
    
- Sequence diagram
    
- API contract draft
    
- Permission flow
    

📦 Artefak:

- System Architecture Diagram
    
- BPMN
    
- API Blueprint
    

➡️ Backend & Frontend **wajib patuh ke ini**.

---

### A.3.b. FASE 2 — PEMBAGIAN SCOPE & WAKTU
#### A.3.b.i. Project Management Office (PMO)
**Ini inti dari pertanyaanmu.**

PMO membuat:

##### Scope Partializator
- Feature Breakdown Structure (FBS)
    
- Task decomposition per divisi
    
- Dependency map
    
- Conflict prevention (siapa _tidak boleh_ mengerjakan apa)
    

##### Bobot & Effort
Gunakan **weighted scoring**:

- Complexity
    
- Risk
    
- Dependency
    
- Impact
    

📦 Artefak:

- RACI Matrix
    
- Work Breakdown Structure (WBS)
    
- Dependency Graph
    

➡️ **Tidak ada task tanpa owner dan bobot.**

---

#### A.3.b.ii. Knowledge & Resource Management (KRM)
**Menghemat 30–40% waktu tim**

Isi:

- Tech stack decision
    
- Coding guideline
    
- API reference
    
- Design system
    
- FAQ lintas divisi
    

📦 Artefak:

- Internal Wiki / Notion / Confluence
    

➡️ Kalau masih sering “nanya-nanya”, berarti KRM gagal.

---

### A.3.c. FASE 3 — DELIVERY
#### A.3.c.i. Product Planning & Delivery (PPD)
Menyusun:

- Sprint plan
    
- Feature priority
    
- Release milestone
    

📦 Artefak:

- Product roadmap
    
- Sprint backlog

---

#### A.3.c.ii. UI/UX & Product Design (UX)
**Jalan paralel dengan backend awal**

- Wireframe
    
- Design system
    
- User flow
    
- Prototype
    

📦 Artefak:

- Figma + Design Spec
    

➡️ UX **tidak boleh** mendesain fitur yang belum disetujui BSA + SDPE.

---

#### A.3.c.iii. Backend Engineering (BE)
- API implementation
    
- Auth & authorization
    
- Business logic
    
- Data validation
    

📦 Artefak:

- API Docs (OpenAPI)
    
- Unit test

---

#### A.3.c.iv. Frontend Engineering (FE)
- Component slicing
    
- State management
    
- Integration API
    
- Modularization
    

📦 Artefak:

- Component library
    
- Feature modules

---

### A.3.d. FASE 4 — VALIDASI & RELEASE
#### A.3.d.i. 🔟 Quality Control & Assurance (QA/QC)
- Test case
    
- Regression test
    
- Security testing
    
- UAT support
    

📦 Artefak:

- Test report
    
- Bug list dengan severity

---

#### A.3.d.ii. 1️⃣ DevOps & Platform Engineering (DPE)
- CI/CD
    
- Environment
    
- Third-party service
    
- Monitoring
    
- Rollback strategy
    

📦 Artefak:

- Deployment pipeline
    
- Infrastructure diagram

---

## A.4. Ringkasan Alur Sederhana (Mental Model)
```
IDEA
 ↓
BSA → DAG → SDPE
 ↓
PMO + KRM
 ↓
UX ↔ BE → FE
 ↓
QA
 ↓
DEVOPS
 ↓
RELEASE
```

---

## A.5. Kesalahan Fatal yang Harus Dihindari
- Backend jalan sebelum data governance
    
- Frontend slicing sebelum API contract
    
- UX desain tanpa business constraint
    
- QA baru masuk di akhir
    
- PMO hanya jadi tukang timeline

---


---

# B. KRITIK TERHADAP PENDEKATAN BELAJAR TRADISIONAL

## B.1. Kritik cara lama kamu (ERD → UI/UX → Coding)
Pendekatan ini **umum, tapi rawan jebakan**:

1. **ERD dulu tanpa konteks bisnis**  
    → sering berakhir refactor karena rule bisnis baru muncul belakangan.
    
2. **UI/UX tanpa kontrak fitur**  
    → klien bilang “kok ini belum ada?” padahal tidak pernah disepakati.
    
3. **Coding sebagai black hole**  
    → scope creep karena tidak ada batas eksplisit.
    

Masalah utamanya:  
❌ **tidak ada kontrak pemahaman sebelum kerja teknis**

---

## B.2. Prinsip Baru untuk Solo Dev (ini kunci)
Sebagai solo dev, **kamu tidak butuh semua dokumen korporat**, tapi kamu butuh:

> **Dokumen tipis tapi mengikat**

Target:

- Klien **tidak bisa seenaknya nambah scope**
    
- Kamu **tidak tersesat secara teknis**
    
- Semua keputusan bisa ditelusuri

---

## B.3. Apa yang HARUS kamu gali dari client (wajib, non-negotiable)
### B.3.a. Informasi Inti (harus kamu gali, walau klien gaptek)
Ini **tidak selalu ada di dokumen**, tapi harus kamu ekstrak.

1. **Masalah utama apa yang mau diselesaikan?**
    
    - Bukan fitur
        
    - Bukan “bikin web”
        
    - Tapi pain nyata
        
2. **Siapa user utamanya?**
    
    - 1–2 role saja (jangan terima 5 role di awal)
        
3. **Apa indikator sukses?**
    
    - Lebih cepat?
        
    - Lebih murah?
        
    - Lebih rapi?
        
4. **Apa yang TIDAK perlu dibuat?**
    
    - Ini penting untuk mengunci scope
        

👉 Ini bisa **spoken**, tapi **harus kamu tulis ulang**.

---

### B.3.b. File Pendukung yang WAJIB kamu minta (kalau ada)
|File|Untuk Apa|Jika Tidak Ada|
|---|---|---|
|SOP / Flow kerja|pahami proses nyata|kamu buat versi kasar|
|Excel / Google Sheet|lihat data real|minta contoh dummy|
|Contoh sistem lama|referensi behaviour|kamu asumsi & tulis|
|Brand guideline|UI konsisten|kamu buat default|
|Legal / regulasi|hindari blunder|flag risiko|

> Kalau klien bilang “nggak ada” → **kamu buatkan versi minimalnya** dan minta approval.

---

## B.4. Dokumen Minimum yang HARUS kamu buat (solo version)
Ini versi **ringkas, bukan korporat**.

### B.4.a. Project Brief (1–2 halaman)
Isi:

- Tujuan proyek
    
- User & role
    
- Fitur utama (bullet, bukan detail)
    
- Non-goal
    
- Timeline kasar
    

➡️ Ini **kontrak pemahaman**, bukan teknis.

---

### B.4.b. Feature List + Boundary
Format simpel:

|Feature|Included|Notes|
|---|---|---|
|Login|✅|Email + password|
|Export PDF|❌|Phase berikut|
|Role admin|✅|CRUD user|

➡️ Ini **tameng scope creep**.

---

### B.4.c. User Flow Sederhana
- Pakai diagram kasar atau bullet:
    
    - User login → dashboard → input data → submit
        

➡️ Jangan Figma dulu.

---

## B.5. Setelah info terkumpul, langkah teknis yang BENAR
### B.5.a. Kunci Fitur DULU (bukan ERD)
Tanya diri kamu:

- Fitur apa yang **pasti ada**
    
- Fitur apa yang **boleh menyusul**
    

Output:

- Feature map

---

### B.5.b. Buat Data Map (bukan ERD detail)
Cukup jawab:

- Data apa masuk?
    
- Disimpan di mana?
    
- Dipakai di fitur apa?
    

Baru setelah itu:  
➡️ **ERD sederhana**

---

### B.5.c. API & Logic Skeleton
Sebelum coding:

- Endpoint list
    
- Payload contoh
    
- Response shape
    

➡️ Ini bikin FE & BE selaras walau kamu solo.

---

### B.5.d. UI/UX LOW fidelity
- Wireframe kasar
    
- Fokus flow, bukan estetika
    

➡️ Jangan pixel-perfect dulu.

---

### B.5.e. Breakdown To-Do Teknis (ini penting)
Contoh breakdown solo dev:

1. Setup repo & environment
    
2. Auth basic
    
3. Core entity CRUD
    
4. Business logic
    
5. UI utama
    
6. Edge case
    
7. Testing manual
    
8. Deployment
    

Setiap item:

- estimasi waktu
    
- dependency

---

## B.6. Workflow Praktis Solo Dev (yang realistis)
```
Client Brief
 ↓
Project Brief (ditulis kamu)
 ↓
Feature Lock
 ↓
Data Map → ERD
 ↓
API Skeleton
 ↓
Wireframe
 ↓
Coding Iteratif
 ↓
Review Berkala
 ↓
Release
```

---

## B.7. Rule Emas agar tidak overthinking
- **Jika belum mempengaruhi fitur → jangan dianalisis**
    
- **Jika belum dipakai user → tunda**
    
- **Jika bisa ditulis 1 paragraf → cukup**

---


---

# C. KESALAHAN UMUM DALAM PROYEK MANDIRI

## C.1. Kesalahan umum saat membangun proyek dari ide sendiri

Kebanyakan solo dev jatuh ke salah satu ekstrem:

1. **Langsung ngoding karena “ini ide saya sendiri”**  
    → cepat jalan, tapi cepat pula refactor total.
    
2. **Terlalu lama mikir arsitektur masa depan**  
    → proyek tidak pernah selesai, tidak pernah dipakai.
    

Masalah intinya:

> **tidak ada fase “menulis ide menjadi sistem”**

---

## C.2. Prinsip kerja baru untuk proyek ide sendiri

Pegang 4 prinsip ini:

1. **Tulis dulu sebelum bangun**
    
2. **Bangun untuk dipakai, bukan dipamerkan**
    
3. **Setiap keputusan harus punya alasan bisnis / usage**
    
4. **Semua yang belum dipakai user = spekulasi**
    

Kalau ini dipegang, kamu aman dari overthinking.

---

## C.3. Persiapan WAJIB sebelum teknis (tanpa klien)

Anggap kamu adalah **client paling kejam untuk diri sendiri**.

### C.3.a. Klarifikasi ide (sangat singkat, tapi tajam)

Jawab **tertulis**, maksimal 1 halaman:

1. **Masalah apa yang ingin diselesaikan?**  
    (bukan fitur)
    
2. **Siapa user utama? (1 role saja dulu)**  
    contoh: admin UMKM, guru, owner bisnis kecil
    
3. **Aktivitas utama user apa?**  
    → login, input data, lihat laporan, dsb.
    
4. **Apa versi paling kecil yang masih berguna?**  
    → ini MVP sejati
    

Jika kamu tidak bisa jawab ini dengan jelas, **jangan buka editor kode**.

---

### C.3.b. Tentukan batas sejak awal (ini sering diabaikan)

Tuliskan secara eksplisit:

- Fitur yang **tidak akan dibuat sekarang**
    
- Asumsi yang kamu pakai
    
- Hal yang kamu sengaja sederhanakan
    

Ini menggantikan “client approval”.

---

## C.4. Dokumen MINIMAL untuk proyek ide sendiri

Bukan PRD panjang. Cukup **3 artefak inti**.

---

### C.4.a. Project Intent Document (PID)

Ini pengganti dokumen klien.

Isi:

- Tujuan proyek
    
- Target user
    
- Masalah yang diselesaikan
    
- MVP definition
    
- Non-goal
    

📌 Panjang ideal: 1 halaman.

---

### C.4.b. Feature Boundary List

Buat tabel sederhana:

|Feature|Status|Alasan|
|---|---|---|
|Auth|include|wajib|
|Role multi-level|exclude|belum perlu|
|Export PDF|later|nice to have|

Ini **mengunci scope internal kamu sendiri**.

---

### C.4.c. User Flow Tekstual / Diagram Kasar

Contoh:

```
User login
→ dashboard
→ buat data X
→ simpan
→ lihat hasil
```

Tidak perlu Figma dulu.

---

## C.5. Urutan teknis yang BENAR (solo dev version)

Sekarang kita masuk teknis, **tanpa cara tradisional yang mentah**.

---

### C.5.a. Feature-first, bukan ERD-first

❌ Jangan mulai dari ERD  
✅ Mulai dari **fitur dan aksi user**

Tanya:

- User klik apa?
    
- Sistem respon apa?
    
- Data apa yang dibutuhkan?

---

### C.5.b. Data Mapping (sebelum ERD)

Buat list seperti ini:

|Data|Digunakan di fitur|Catatan|
|---|---|---|
|User|login, profile|wajib|
|Order|dashboard|inti|
|Payment|laporan|nanti|

Baru setelah itu:  
➡️ **ERD sederhana dan fleksibel**

---

### C.5.c. API & Logic Skeleton (walau monolith)

Tulis dulu:

- Endpoint
    
- Input
    
- Output
    
- Rule bisnis
    

Tanpa implementasi.

Kenapa?

> karena ini mengurangi refactor besar di FE dan BE.

---

### C.5.d. UI/UX low fidelity

- Wireframe kasar
    
- Fokus: **alur kerja**
    
- Abaikan warna, font, animasi

---

### C.5.e. Breakdown to-do teknis (solo WBS)

Contoh realistis:

1. Setup project & auth
    
2. Core entity CRUD
    
3. Business logic utama
    
4. UI utama
    
5. Edge case minimal
    
6. Manual testing
    
7. Deploy
    

Setiap item:

- estimasi jam
    
- dependency

---

## C.6. Workflow ringkas tapi aman

```
Ide
↓
Project Intent
↓
Feature Boundary
↓
User Flow
↓
Data Mapping → ERD
↓
API Skeleton
↓
Wireframe
↓
Coding Iteratif
↓
Release
```

Ini **versi dewasa** dari ERD → UI → code.

---

## C.7. Kapan kamu BOLEH skip analisis?

Boleh skip jika:

- tidak mengubah alur user
    
- tidak mempengaruhi data inti
    
- tidak berdampak ke keamanan
    

Tidak boleh skip jika:

- auth
    
- permission
    
- data ownership
    
- money / payment

---


---

# D. KONSEP VERTICAL SLICE ARCHITECTURE

lakukan 4 hal secara berurutan dan **tegas**:

1. **Memvalidasi dan merapikan definisi masalah & asumsi** (tanpa mengiyakan mentah).
    
2. **Mengunci scope MVP yang benar-benar buildable oleh solo dev**.
    
3. **Menyusun urutan pengerjaan end-to-end yang efisien** (mengganti pola ERD → UI → code).
    
4. **Memberi breakdown teknis konkret** yang bisa langsung kamu jadikan todo list.
    

Kalau di satu titik ada asumsi yang lemah, saya akan bilang.

---


---

# E. MANAJEMEN PROYEK UNTUK SOLO DEVELOPER

## E.1. Evaluasi masalah & tujuan (objektif, kritis)
### E.1.a. Masalah yang ingin kamu selesaikan — VALID, tapi bercabang
Kamu sebenarnya ingin menyelesaikan **3 masalah berbeda**:

1. **Akses edukasi** untuk pelajar tidak mampu
    
2. **Monetisasi adil** untuk guru tanpa dana mengendap
    
3. **Trust & credential** (sertifikat immutable)
    

➡️ Ini **valid**, tapi untuk solo dev **tidak bisa diperlakukan setara di MVP**.

**Kesimpulan kritis:**

> Untuk MVP, **satu masalah harus jadi poros utama**, dua lainnya pendukung.

👉 Dari deskripsi kamu, poros paling kuat adalah:  
**crowdfunded course + transparansi finansial**

Sertifikat immutable = _value add_, bukan core di fase awal.

---

### E.1.b. User utama — sudah benar, tapi perlu hirarki
Untuk MVP:

1. **Teacher** = supply
    
2. **Student (regular + scholarship)** = demand
    
3. **Admin** = kontrol trust & risk (WAJIB, jangan di-skip)
    

Perusahaan memang benar ditunda.

---

### E.1.c. Aktivitas user — perlu dikoreksi satu titik penting
> “jika pelajar memilih fund this course, maka pelajar membuat campaign crowdfund”

⚠️ Ini **rawan desain**.

Secara sistem:

- Course dibuat oleh **teacher**
    
- Campaign crowdfund **harus terkait ke course**
    
- Student **menginisiasi**, tapi **tidak memiliki penuh**
    

👉 Ownership campaign **harus dipegang sistem / course**, bukan student individual.  
Kalau tidak:

- potensi manipulasi
    
- konflik dana
    
- kompleks di smart contract
    

Ini nanti kita sederhanakan di MVP.

---

## E.2. Reframing: versi MVP yang masuk akal untuk SOLO DEV
Saya akan sederhanakan tanpa menghilangkan visi.

### E.2.a. Fokus MVP (dikunci)
> **Platform course di mana teacher bisa membuka course untuk crowdfunding terbatas, dan student terverifikasi bisa mengakses course tersebut, dengan alur dana transparan ke wallet teacher.**

Yang **belum kita kejar**:

- DAO
    
- verifikasi dokumen kompleks
    
- fiat
    
- governance lanjutan

---

## E.3. Scope MVP yang DIKUNCI (ini penting)
### E.3.a. Role & Capability Matrix (versi MVP)
|Role|Capability|
|---|---|
|Guest|lihat course|
|Student|enroll, fund, belajar|
|Teacher|buat course, set crowdfund|
|Admin|approve scholarship, moderate|

---

### E.3.b. Feature MVP — Final Lock
#### E.3.b.i. Core (WAJIB ADA)
- Auth (email + wallet optional)
    
- Teacher create course
    
- Course: paid / crowdfunded
    
- Scholarship flag (boolean via admin)
    
- Crowdfund progress tracking
    
- Enroll course
    
- Course completion status
    
- Certificate hash (on-chain / pseudo)
    

#### E.3.b.ii. Explicitly Excluded
- DAO
    
- voting
    
- fiat
    
- KYC real
    
- multi-chain
    

➡️ Ini **aman untuk 1 orang**.

---

## E.4. Cara pengerjaan yang BENAR (bukan ERD → UI → code)
Sekarang kita masuk **metode kerja baru**.

---

## E.5. Tuliskan _System Intent_ (1 halaman, final)
Ini bukan PRD panjang. Ini pengunci logika.

Isi (sudah bisa kamu tulis sekarang):

- tujuan sistem
    
- role & hak
    
- alur dana
    
- apa yang dianggap “course selesai”
    
- apa yang dianggap “campaign sukses”
    

➡️ Tanpa ini, smart contract dan backend akan tarik-menarik.

---

## E.6. Feature → Data Mapping (sebelum ERD)
Contoh awal:

|Feature|Data yang dibutuhkan|
|---|---|
|Login|user, role, wallet|
|Course|course, teacher|
|Crowdfund|campaign, target, current|
|Funding|transaction|
|Enrollment|enrollment|
|Certificate|completion, hash|

➡️ Baru setelah ini kamu **boleh bikin ERD**.

---

## E.7. ERD MVP (jangan sempurna)
Entity minimal yang **cukup**:

- User
    
- Course
    
- Enrollment
    
- CrowdfundingCampaign
    
- FundingTransaction
    
- Certificate
    

Relasi sederhana, no polymorphism dulu.

---

## E.8. Tentukan batas Web2 vs Web3 (KRUSIAL)
Untuk MVP solo dev, **aturan emas**:

|Bagian|Tempat|
|---|---|
|Auth|Web2|
|Course & enroll|Web2|
|Crowdfund fund|Web3|
|Certificate hash|Web3|
|Progress, UI|Web2|

👉 Jangan kebalik.  
👉 Jangan semua di-chain.

---

## E.9. API Skeleton (bahkan sebelum UI)
Contoh:

- POST /course
    
- POST /course/:id/crowdfund
    
- POST /fund
    
- POST /enroll
    
- POST /complete
    
- GET /certificate
    

➡️ Ini akan menyelamatkan kamu dari refactor besar.

---

## E.10. UI/UX LOW FIDELITY
Hanya:

- halaman list course
    
- detail course
    
- dashboard teacher
    
- dashboard student
    

Tidak perlu animasi, tidak perlu design system dulu.

---

## E.11. Coding ITERATIF (urutan aman)
1. Auth + role
    
2. Course CRUD
    
3. Enrollment
    
4. Crowdfunding logic (off-chain dulu)
    
5. Smart contract funding
    
6. Certificate hash
    
7. UI polishing
    
8. Deploy

---

## E.12. Kejujuran profesional
Proyek ini:

- **bukan kecil**
    
- **bisa selesai oleh solo dev**
    
- **asal kamu disiplin scope**
    

Jika kamu langsung:

- mikir DAO
    
- mikir governance
    
- mikir enterprise
    

→ proyek akan mati di bulan ke-2.

---

## E.13. System Intent — LearnChain (MVP)

### E.13.a. Tujuan Sistem

- Membuka akses bagi pengajar sebagai penyedia course.
    
- Menyediakan pembayaran course berbasis kriptokurensi tanpa kustodi (non-custodial).
    
- Memberikan sertifikat penyelesaian course yang immutable (NFT atau hash on-chain).
    
- Menyediakan mekanisme crowdfunding terkontrol bagi user dengan status "tidak mampu" yang menempel pada entitas user.
    

### E.13.b. Role & Hak Akses

#### E.13.b.i. Guest (dan semua role sebelum login)

- Melihat daftar course dan detail course.
    
- Registrasi dan login.
    
- Connect wallet.
    

#### E.13.b.ii. Pelajar (extend Guest)

- Enroll dan mengikuti course.
    
- Menginisiasi campaign crowdfunding (hanya jika status "tidak mampu").
    
- Mencetak / mengklaim sertifikat setelah course selesai.
    

#### E.13.b.iii. Pengajar

- Membuat dan mengelola course.
    
- Menandai course sebagai crowdfundable.
    
- Menetapkan course sebagai closed (tidak menerima enrollment baru).
    

#### E.13.b.iv. Admin

- Menetapkan status pelajar sebagai "tidak mampu".
    
- Menonaktifkan (ban) user.
    

### E.13.c. Alur Dana

- Semua user harus connect wallet untuk melakukan enrollment.
    
- Pembayaran enrollment course langsung masuk ke wallet pengajar melalui transaksi blockchain (tanpa kustodi).
    
- Platform mengambil fee 1% dari pembayaran course ke wallet perusahaan.
    
- Dana crowdfunding disimpan di vault crowdfunding.
    
- Jika target crowdfunding tidak tercapai, user dapat menarik dana tanpa dikenakan fee.
    

### E.13.d. Definisi Course Selesai

- Course dianggap selesai jika pelajar mencapai progress 100%.
    
- Pelajar telah menyelesaikan sylabus terakhir dan tugas akhir.
    

### E.13.e. Definisi Campaign Sukses

- Campaign dianggap sukses ketika total funding mencapai harga course.
    
- Pelajar secara eksplisit menyetujui dan mengeksekusi aksi "fund now".

---

Bagus. Ini **sudah level “bisa dibangun”**, bukan lagi ide mentah.  
Sekarang saya akan **bersikap kritis dan objektif**, bukan memuji, dengan tujuan:  
👉 **mengunci risiko sebelum kamu masuk teknis**.

Saya akan lakukan 3 hal:

1. **Audit System Intent kamu** (apa yang sudah kuat, apa yang berbahaya).
    
2. **Perbaikan logika role, alur dana, dan crowdfunding** supaya aman untuk MVP solo dev.
    
3. **Langkah NEXT yang konkret**: apa yang harus kamu kerjakan setelah dokumen ini.

---

### E.13.f. Audit cepat System Intent (jujur & tegas)

#### E.13.f.i. Tujuan sistem — VALID dan konsisten

Semua tujuan:

- non-custodial payment
    
- trust via blockchain
    
- crowdfund terkontrol
    

👉 **konsisten satu sama lain**, ini poin kuat.

Catatan kritis:

- “sertifikat berbasis NFT atau tercatat di blockchain”  
    → untuk MVP **harus dipilih salah satu**, jangan “atau”.
    

Rekomendasi MVP:

> **hash + metadata on-chain, bukan full NFT transferable**  
> Lebih murah, lebih cepat, lebih aman dari spekulasi.

---

#### E.13.f.ii. Role & hak — 1 masalah desain penting

##### Masalah:

> Pelajar bisa “up crowdfund campaign”

Ini **secara logika bisnis boleh**,  
tapi **secara sistem dan keamanan berbahaya** kalau tidak dibatasi.

Risikonya:

- campaign liar
    
- duplikasi campaign
    
- manipulasi target
    

##### Koreksi yang saya rekomendasikan (penting):

- **Campaign menempel ke Course + Student**
    
- **Tidak bisa membuat campaign manual dengan parameter bebas**
    

Artinya:

> Pelajar hanya bisa klik  
> **“Request crowdfunding for this course”**  
> bukan membuat campaign bebas.

Ini **mengurangi kompleksitas smart contract & backend drastis**.

---

#### E.13.f.iii. Alur dana — 80% sudah benar, 20% rawan

Yang sudah benar:

- non-custodial ✔
    
- fee transparan ✔
    
- refund crowdfund jika gagal ✔
    

⚠️ Titik rawan:

> “dana crowdfund disimpan di vault crowdfund”

Pertanyaan kritis:

- vault ini **siapa yang kontrol?**
    
- smart contract atau backend?
    

Untuk MVP solo dev:

- vault **HARUS smart contract**
    
- backend **tidak boleh pegang dana**
    

Kalau tidak:  
→ seluruh trust narasi runtuh.

---

#### E.13.f.iv. Definisi “course selesai” — cukup, tapi perlu satu penegasan

Sekarang:

- progress 100%
    
- tugas akhir selesai
    

Tambahkan satu rule eksplisit:

> progress dihitung **berdasarkan sistem**, bukan manual teacher

Kalau tidak:

- sertifikat bisa diperdebatkan
    
- trust hilang

---

#### E.13.f.v. Definisi “campaign sukses” — perlu klarifikasi kecil

Sekarang:

> total funding mencapai harga course + pelajar set “fund now”

Secara logika oke, tapi **kurang satu state**.

Saya sarankan 3 state:

1. `pending`
    
2. `target_reached`
    
3. `executed`
    

Kenapa?

- supaya dana tidak auto-mengalir tanpa konfirmasi final
    
- mencegah edge case user berubah pikiran

---

### E.13.g. Versi FINAL yang lebih aman (tanpa nambah scope)

Saya rangkum koreksi **tanpa mengubah visi** kamu.

#### E.13.g.i. Crowdfunding (MVP-safe version)

- Campaign **selalu terkait ke 1 course + 1 student**
    
- Parameter campaign:
    
    - target = harga course
        
    - deadline (opsional, default)
        
- Dana:
    
    - masuk ke smart contract vault
        
    - refundable jika gagal
        
- Jika target tercapai:
    
    - student mengeksekusi `fundNow()`
        
    - dana dialirkan:
        
        - 99% → teacher wallet
            
        - 1% → platform wallet
            

Ini **cukup kuat secara trust**, dan **masih doable solo**.

---

### E.13.h. Sekarang: apa LANGKAH BERIKUTNYA (jangan lompat)

Kamu sudah menyelesaikan **System Intent**.  
Langkah berikutnya **bukan UI dan bukan coding**.

#### E.13.h.i. NEXT STEP YANG BENAR (pilih satu, urut)

#### E.13.h.ii. 🔥 STEP A — Entity & Data Boundary Lock (wajib)

Tujuan:

- mencegah refactor database & contract
    

Isi:

- daftar entity final (MVP)
    
- relasi utama
    
- mana on-chain vs off-chain
    

Kalau ini belum dikunci → **jangan sentuh code**.

---

#### E.13.h.iii. STEP B — Web2 vs Web3 Responsibility Matrix

Tujuan:

- mencegah over-chain
    
- mencegah gas burn
    

Contoh:

- enrollment → Web2
    
- funding → Web3
    
- progress → Web2
    
- certificate hash → Web3

---

#### E.13.h.iv. STEP C — Smart Contract Scope Lock

Tujuan:

- kontrak kecil, aman, bisa di-audit
    

MVP contract biasanya cukup:

- FundingVault
    
- CertificateRegistry

---

### E.13.i. Rekomendasi tegas sebagai konsultan

Kalau kamu bertanya:

> “apakah ini terlalu besar untuk solo dev?”

Jawaban jujur:

- **visi besar**
    
- **MVP-nya masih realistis**
    
- **asal kamu disiplin pada scope ini**
    

Kalau kamu mulai:

- nambah DAO
    
- nambah governance
    
- nambah multi-chain  
    sebelum MVP live → proyek akan berhenti.

---


---

# F. PERANCANGAN DATA DAN SKEMA DATABASE (ERD)

Dokumen ini mengunci **entity dan relasi final untuk MVP**, dengan asumsi:

- Solo full‑stack developer
    
- Non‑custodial payment
    
- Crowdfunding terkontrol
    
- Sertifikat berbasis hash + metadata on‑chain

---

### F.0.a. Entity List (FINAL untuk MVP)

#### F.0.a.i. User

Representasi semua aktor sistem.

**Field inti:**

- id (PK)
    
- email
    
- password_hash
    
- role (student | teacher | admin)
    
- wallet_address (nullable)
    
- is_active (boolean)
    
- is_scholarship (boolean)
    
- created_at

---

#### F.0.a.ii. Course

Unit utama produk edukasi.

**Field inti:**

- id (PK)
    
- teacher_id (FK → User)
    
- title
    
- description
    
- price
    
- is_crowdfundable (boolean)
    
- status (draft | published | closed)
    
- syllabus_version
    
- created_at

---

#### F.0.a.iii. Enrollment

Relasi pelajar ↔ course.

**Field inti:**

- id (PK)
    
- user_id (FK → User)
    
- course_id (FK → Course)
    
- status (enrolled | completed)
    
- progress (0–100)
    
- enrolled_at
    
- completed_at (nullable)

---

#### F.0.a.iv. CrowdfundingCampaign

Campaign crowdfunding yang **selalu menempel ke 1 course + 1 student**.

**Field inti:**

- id (PK)
    
- course_id (FK → Course)
    
- student_id (FK → User)
    
- target_amount
    
- total_funded
    
- state (pending | target_reached | executed)
    
- vault_contract_address
    
- created_at

---

#### F.0.a.v. FundingTransaction

Pencatatan kontribusi crowdfund (off‑chain mirror).

**Field inti:**

- id (PK)
    
- campaign_id (FK → CrowdfundingCampaign)
    
- funder_id (FK → User)
    
- amount
    
- tx_hash (on‑chain reference)
    
- created_at

---

#### F.0.a.vi. Certificate

Representasi sertifikat penyelesaian course.

**Field inti:**

- id (PK)
    
- enrollment_id (FK → Enrollment)
    
- certificate_hash (on‑chain)
    
- metadata_uri
    
- issued_at

---

### F.0.b. Relasi Antar Entity

- User (teacher) 1 ── * Course
    
- User (student) 1 ── * Enrollment
    
- Course 1 ── * Enrollment
    
- Course 1 ── * CrowdfundingCampaign
    
- User (student) 1 ── * CrowdfundingCampaign
    
- CrowdfundingCampaign 1 ── * FundingTransaction
    
- Enrollment 1 ── 1 Certificate

---

### F.0.c. Boundary Web2 vs Web3

#### F.0.c.i. Web2 (Database & Backend)

- User
    
- Course
    
- Enrollment
    
- CrowdfundingCampaign (state & mirror)
    
- FundingTransaction (mirror)
    

#### F.0.c.ii. Web3 (Smart Contract)

- Crowdfunding vault (fund, refund, execute)
    
- Certificate hash registry

---

### F.0.d. Explicit MVP Constraints

- Tidak ada polymorphic role
    
- Tidak ada multi‑campaign per course per student
    
- Tidak ada editable certificate
    
- Tidak ada fiat conversion
    
- Tidak ada DAO / governance
    

Dokumen ini menjadi **baseline teknis**. Jika entity baru muncul → itu **post‑MVP**.

Baik. **Entity + ERD MVP sudah terkunci.**  
Yang barusan kita lakukan itu **keputusan arsitektural**, bukan sekadar desain data.

Sekarang saya akan jelaskan **apa arti ERD ini secara praktis**, lalu **apa yang BOLEH dan TIDAK BOLEH kamu lakukan setelah titik ini**.

---

### F.0.e. Validasi cepat: apakah ERD ini sudah “aman”?

Jawaban profesional: **ya, untuk MVP solo dev ini sudah aman dan realistis**.

Kenapa?

- Semua **aktor inti** terwakili → user, teacher, student, admin
    
- Crowdfunding **tidak liar** → selalu terikat `course + student`
    
- Dana **tidak pernah menyentuh backend**
    
- Sertifikat **immutable tapi murah**
    
- Tidak ada entity “abu-abu” yang bikin refactor besar
    

Artinya:

> kalau kamu build sesuai ERD ini, **kamu tidak akan kejebak redesign struktural** di tengah jalan.

---

### F.0.f. Hal penting yang perlu kamu pahami (ini sering disalahartikan)

#### F.0.f.i. CrowdfundingCampaign adalah entity “semi-on-chain”

- Di **Web2**: state, relasi, progress UI
    
- Di **Web3**: dana, refund, execute
    

👉 Jangan coba “menyatukan logika” ini.  
Backend **hanya mirror dan guardrail**, bukan sumber kebenaran dana.

---

#### F.0.f.ii. Enrollment adalah pusat trust sertifikat

Perhatikan:

- Certificate **tidak berdiri sendiri**
    
- Certificate selalu **turunan dari Enrollment**
    

Ini keputusan yang **sangat tepat**, karena:

- mencegah sertifikat palsu
    
- mencegah mint manual
    
- memudahkan audit

---

#### F.0.f.iii. Scholarship = flag, bukan sistem

Keputusan kamu:

> `is_scholarship: boolean`

Ini **benar untuk MVP**.

Jangan:

- nambah tabel verifikasi
    
- nambah workflow approval kompleks
    

Kalau nanti perlu:  
→ **extend**, bukan ganti.

---

### F.0.g. Apa yang TIDAK BOLEH kamu ubah setelah ini

Mulai titik ini, anggap ini **frozen**:

- Role model (student / teacher / admin)
    
- Campaign → selalu 1 student + 1 course
    
- Certificate → hanya bisa lahir dari enrollment completed
    
- Fee → fixed 1%
    

Kalau kamu ubah ini di tengah jalan:

> backend, smart contract, dan UI akan saling merusak.

---

### F.0.h. Sekarang: apa LANGKAH TEKNIS SELANJUTNYA (jangan lompat)

Setelah ERD dikunci, **urutan yang benar** adalah:

#### F.0.h.i. NEXT STEP (harus berurutan)

#### F.0.h.ii. 🔥 Step B — Web2 vs Web3 Responsibility Matrix

Tujuan:

- mengunci apa yang **boleh dan tidak boleh masuk blockchain**
    
- mencegah over-engineering & gas burn
    

Output:

- tabel tanggung jawab
    
- dasar desain smart contract
    

Tanpa ini:

- kamu akan ragu setiap kali menulis fitur
    
- atau malah over-chain

---

#### F.0.h.iii. Setelah itu (baru boleh):

- Step C — Smart Contract Textual Design
    
- Step D — API Skeleton
    
- Step E — Roadmap 8–12 minggu

---

### F.0.i. Kejujuran terakhir (penting)

Dengan ERD ini:

- kamu **sudah berpikir seperti system designer**
    
- bukan lagi “coder bikin web”
    

Tapi bahaya terbesarnya sekarang adalah:

> merasa “fondasinya sudah beres” lalu lompat ke coding.

Kalau itu terjadi:

- boundary Web2/Web3 akan bocor
    
- trust narrative akan runtuh

---


---

# G. ARSITEKTUR SMART CONTRACT DAN WEB3

Baik. Kita lanjut **B — Web2 vs Web3 Responsibility Matrix**.  
Ini **titik paling krusial** di proyek Web2.5. Banyak proyek gagal bukan karena coding jelek, tapi karena **boundary bocor**.

Saya akan susun ini dengan **logika sistem + alasan teknis**, bukan opini.

---

## G.1. Web2 vs Web3 Responsibility Matrix (MVP FINAL)

Tujuan dokumen ini:

- Mengunci **apa yang on-chain, apa yang off-chain**
    
- Menjadi **rule of decision** setiap kali kamu ragu
    
- Mencegah **over-chain**, **gas burn**, dan **logic split**

---

### G.1.a. Prinsip Dasar (jangan dilanggar)

Pegang 4 prinsip ini:

1. **Dana = Web3**
    
2. **UX & workflow = Web2**
    
3. **Trust boundary = Web3**
    
4. **State yang sering berubah = Web2**
    

Kalau satu fitur melanggar prinsip ini, **desainnya salah**.

---

### G.1.b. Responsibility Matrix (FINAL untuk MVP)

#### G.1.b.i. Identity & Access

|Concern|Web2|Web3|Alasan|
|---|---|---|---|
|Register / Login|✅|❌|UX cepat, murah|
|Role (student/teacher/admin)|✅|❌|Governance off-chain|
|Scholarship flag|✅|❌|Sementara, admin-driven|
|Wallet connect|❌|✅|Ownership user|

➡️ **Wallet ≠ identity**, hanya bukti kepemilikan aset.

---

#### G.1.b.ii. Course Management

|Concern|Web2|Web3|Alasan|
|---|---|---|---|
|Course CRUD|✅|❌|Sering berubah|
|Price|✅|❌|Referensi UI|
|Syllabus & progress|✅|❌|High frequency|
|Course status|✅|❌|Workflow|

➡️ **Course bukan aset blockchain**, hanya objek bisnis.

---

#### G.1.b.iii. Enrollment & Learning

|Concern|Web2|Web3|Alasan|
|---|---|---|---|
|Enrollment record|✅|❌|Cepat & mutable|
|Progress tracking|✅|❌|Update intens|
|Task submission|✅|❌|Approval logic|
|Course completion|✅|❌|Precondition cert|

➡️ Jangan pernah simpan progress on-chain.

---

#### G.1.b.iv. Crowdfunding (INTI TRUST)

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

#### G.1.b.v. Certificate & Trust Artifact

|Concern|Web2|Web3|Alasan|
|---|---|---|---|
|Completion check|✅|❌|Sistem internal|
|Certificate metadata|✅|❌|Fleksibel|
|Certificate hash|❌|✅|Immutable proof|
|Certificate verification|❌|✅|Public trust|

➡️ Ini **cukup**, NFT transferable **tidak perlu** di MVP.

---

#### G.1.b.vi. Platform Economics

|Concern|Web2|Web3|Alasan|
|---|---|---|---|
|Fee rule (1%)|❌|✅|Enforced|
|Platform wallet|❌|✅|Transparent|
|Accounting mirror|✅|❌|Reporting|

➡️ Fee **harus** dihitung on-chain, bukan backend.

---

### G.1.c. Boundary Rules (WAJIB kamu ingat saat coding)

#### G.1.c.i. Rule 1 — Backend tidak pernah menyentuh dana

Jika backend:

- menyimpan balance
    
- menghitung saldo
    

→ **desain salah**

---

#### G.1.c.ii. Rule 2 — Smart contract tidak peduli UX

Smart contract:

- tidak tahu siapa admin
    
- tidak tahu siapa “tidak mampu”
    
- hanya tahu **address & rules**

---

#### G.1.c.iii. Rule 3 — Semua state on-chain harus punya mirror off-chain

Tujuan:

- UI cepat
    
- analytics
    
- recovery kalau RPC lambat

---

### G.1.d. Dampak langsung ke desain arsitektur kamu

Setelah matrix ini:

- kamu **tahu kontrak apa saja yang perlu**
    
- kamu **tahu API mana yang perlu**
    
- kamu **tahu data apa yang tidak boleh di-chain**
    

Tanpa matrix ini:

- smart contract akan terlalu besar
    
- backend akan terlalu berkuasa
    
- trust narrative runtuh

---

### G.1.e. Apa yang SEKARANG BOLEH kamu kerjakan

Setelah dokumen ini dikunci, kamu **resmi boleh**:

- Mendesain **smart contract crowdfunding**
    
- Mendesain **certificate registry**
    
- Mendesain **API skeleton backend**
    

Tapi **harus urut**.

---


---

# H. LOGIKA BACKEND DAN INTEGRASI API

### H.0.a. Validasi dulu: apakah certificate sudah _bind_ ke course?

**Jawaban:**  
👉 **Ya, HARUS bind secara eksplisit ke Course.**  
Dan dalam desain MVP yang sehat, **certificate tidak berdiri sendiri**.

#### H.0.a.i. Binding minimal yang _wajib ada_

Secara logika sistem, **certificate = bukti kelulusan atas course tertentu oleh user tertentu**.

Relasi konseptualnya:

```
Certificate
- certificate_id (on-chain hash / id)
- user_id (student)
- course_id
- completion_hash (progress + final task)
- issued_at
```

#### H.0.a.ii. Implikasi penting

1. **Satu certificate ↔ satu course**
    
    - Tidak ada “general certificate”
        
2. **Course menentukan aturan kelulusan**
    
    - progress 100%
        
    - final task approved
        
3. **Certificate tidak transferable**
    
    - bind ke wallet + user_id
        
4. **Certificate tidak bisa dicetak ulang untuk course lain**
    
    - hash course_id masuk ke metadata
        

👉 Dengan ini:

- **Anti abuse**
    
- **Audit jelas**
    
- **On-chain proof valid**
    

✅ **Saya anggap ini FIX dan kamu sudah sepakat.**  
Kita lanjut ke **C → Desain Smart Contract Crowdfunding**.

---

### H.0.b. C → Desain Smart Contract Crowdfunding

**(Textual Design, State, Function — MVP, tidak over-engineered)**

---

### H.0.c. Prinsip Desain (biar tidak salah arah)

1. **Campaign tidak berdiri sendiri**
    
    - Selalu menempel ke:
        
        - `student`
            
        - `course`
            
2. **Vault dikontrol penuh oleh smart contract**
    
    - Tidak ada admin withdraw manual
        
3. **Tidak ada parameter bebas**
    
    - harga course = target
        
4. **Refund aman jika gagal**
    
5. **Eksekusi dana hanya satu arah**
    
    - dari vault → teacher + platform fee

---

### H.0.d. Entity On-Chain (Minimal)

#### H.0.d.i. CrowdfundCampaign (struct)

```
campaign_id
student_wallet
course_id
course_price
teacher_wallet
platform_wallet
total_funded
state
created_at
```

#### H.0.d.ii. CampaignState (enum)

```
PENDING
TARGET_REACHED
EXECUTED
CANCELLED
```

> Catatan:

- `CANCELLED` hanya jika course ditutup atau student diban sebelum executed

---

### H.0.e. State Definition (Logika Ketat)

#### H.0.e.i. `PENDING`

- total_funded < course_price
    
- user lain bisa fund
    
- student **tidak bisa fund now**
    

#### H.0.e.ii. `TARGET_REACHED`

- total_funded >= course_price
    
- funding otomatis berhenti
    
- **menunggu aksi student**
    

#### H.0.e.iii. `EXECUTED`

- student set `fundNow`
    
- dana:
    
    - `(99%) → teacher`
        
    - `(1%) → platform`
        
- campaign terkunci permanen
    

#### H.0.e.iv. `CANCELLED`

- refund enabled
    
- tidak bisa dieksekusi

---

### H.0.f. Function Design (Textual)

#### H.0.f.i. `createCampaign(student, course)`

**Dipanggil oleh backend / relayer**

Syarat:

- student.status == `tidak_mampu`
    
- course.status == `published`
    
- student belum enroll course ini
    

Efek:

- campaign dibuat
    
- state = `PENDING`

---

#### H.0.f.ii. `fundCampaign(campaign_id)`

**Dipanggil oleh siapa pun**

Syarat:

- state == `PENDING`
    
- msg.value > 0
    

Efek:

- total_funded += msg.value
    
- jika total_funded >= course_price:
    
    - state → `TARGET_REACHED`

---

#### H.0.f.iii. `fundNow(campaign_id)`

**Dipanggil oleh student owner**

Syarat:

- msg.sender == student_wallet
    
- state == `TARGET_REACHED`
    

Efek:

- state → `EXECUTED`
    
- distribute funds:
    
    - teacher_wallet ← 99%
        
    - platform_wallet ← 1%

---

#### H.0.f.iv. `refund(campaign_id)`

**Dipanggil oleh funder**

Syarat:

- state == `PENDING` atau `CANCELLED`
    
- campaign belum executed
    

Efek:

- funder menerima dana sesuai kontribusi

---

#### H.0.f.v. `cancelCampaign(campaign_id)`

**Dipanggil oleh system (admin via backend)**

Syarat:

- student diban / course closed
    
- state != EXECUTED
    

Efek:

- state → `CANCELLED`

---

### H.0.g. Invariant Penting (Wajib Dijaga)

1. **Dana tidak pernah:
    
    - masuk ke wallet admin
        
    - bisa diambil manual**
        
2. **EXECUTED tidak bisa di-revert**
    
3. **Refund hanya sebelum EXECUTED**
    
4. **Campaign tidak bisa dibuat tanpa course valid**

---

### H.0.h. Kenapa desain ini efisien & realistis?

- Tidak perlu DAO
    
- Tidak perlu multisig
    
- Tidak perlu NFT crowdfund
    
- Aman secara logika
    
- Murah gas
    
- Cocok MVP → scale later

---

### H.0.i. Status Sekarang

✔ Certificate binding → **valid & fix**  
✔ Campaign state machine → **clean**  
✔ Dana flow → **aman & audit-friendly**

---


---

# I. SMART CONTRACT ENROLLMENT + CERTIFICATE ISSUANCE FLOW

### I.0.a. Prinsip Desain (ini kunci, jangan dilanggar)

1. **Enrollment = bukti hak akses course**
    
    - Bukan sekadar data off-chain
        
2. **Certificate = konsekuensi dari enrollment + completion**
    
    - Tidak bisa ada tanpa enrollment
        
3. **On-chain hanya menyimpan bukti, bukan proses belajar**
    
    - Progress detail tetap off-chain
        
4. **Teacher tidak bisa “menerbitkan” certificate sesuka hati**
    
    - Teacher hanya _approve final task_
        
5. **Certificate tidak transferable & tidak spekulatif**
    
    - Sesuai kesepakatan: hash + metadata on-chain

---

### I.0.b. Boundary Web2 vs Web3 (supaya tidak rancu)

#### I.0.b.i. On-chain menangani:

- Enrollment validity
    
- Payment proof
    
- Certificate issuance hash
    
- Ownership (wallet)
    

#### I.0.b.ii. Off-chain menangani:

- Progress calculation
    
- Task submission
    
- Teacher review
    
- UI logic
    

👉 Smart contract **tidak menghitung progress**, hanya menerima **hasil final yang sudah tervalidasi sistem**.

---

### I.0.c. Entity On-Chain (Minimal & Tegas)

#### I.0.c.i. Enrollment (struct)

```
enrollment_id
student_wallet
course_id
teacher_wallet
payment_type (direct | crowdfund)
status
enrolled_at
```

#### I.0.c.ii. EnrollmentStatus (enum)

```
ENROLLED
COMPLETED
CERT_ISSUED
```

---

#### I.0.c.iii. Certificate (struct)

```
certificate_id
student_wallet
course_id
enrollment_id
completion_hash
issued_at
```

> `completion_hash` = hash dari:
> 
> - progress summary
>     
> - final task approval
>     
> - timestamp
>

---

### I.0.d. Enrollment Flow

#### I.0.d.i. 1 Direct Enrollment (tanpa crowdfund)

##### Function: `enrollDirect(course_id)`

**Syarat:**

- course.status == `published`
    
- msg.value == course_price
    
- student belum enroll
    

**Efek:**

- transfer:
    
    - 99% → teacher
        
    - 1% → platform
        
- create Enrollment
    
- status = `ENROLLED`

---

#### I.0.d.ii. 2 Crowdfund Enrollment

Enrollment **tidak otomatis** saat campaign sukses.

Enrollment terjadi **SETELAH**:

- campaign `EXECUTED`
    

##### Trigger:

- smart contract crowdfund memanggil `enrollFromCrowdfund(...)`
    

**Efek:**

- Enrollment dibuat
    
- payment_type = `crowdfund`
    
- status = `ENROLLED`
    

👉 Ini penting:

- **Enrollment = bukti legal akses**
    
- Crowdfund hanya alat bayar, bukan enrollment itu sendiri

---

### I.0.e. Completion & Certificate Flow

Ini bagian yang paling sering salah di sistem lain.

---

#### I.0.e.i. 1 Progress Tracking (Off-chain)

- Sistem menghitung:
    
    - module selesai
        
    - progress 100%
        
- Final task:
    
    - dikirim student
        
    - **teacher approve**
        

Setelah semua valid → backend siap _commit result_ ke chain.

---

#### I.0.e.ii. 2 Commit Completion

##### Function: `markCourseCompleted(enrollment_id, completion_hash)`

**Dipanggil oleh:**  
👉 backend relayer (bukan teacher langsung)

**Syarat:**

- enrollment.status == `ENROLLED`
    
- backend sudah:
    
    - progress = 100%
        
    - final task approved teacher
        

**Efek:**

- enrollment.status → `COMPLETED`
    
- simpan `completion_hash`
    

> Teacher **tidak punya akses langsung ke smart contract**  
> → menghindari abuse & dispute

---

#### I.0.e.iii. 3 Certificate Issuance

##### Function: `issueCertificate(enrollment_id)`

**Syarat:**

- enrollment.status == `COMPLETED`
    
- certificate belum ada
    

**Efek:**

- create Certificate
    
- bind:
    
    - student_wallet
        
    - course_id
        
    - enrollment_id
        
- enrollment.status → `CERT_ISSUED`

---

### I.0.f. Certificate Characteristics (sesuai MVP)

1. **Non-transferable**
    
2. **1 enrollment → 1 certificate**
    
3. **Course-bound**
    
4. **Wallet-bound**
    
5. **Verifiable on-chain**
    

Tidak ada:

- marketplace
    
- royalty
    
- speculation

---

### I.0.g. Critical Invariants (Wajib Dijaga)

1. Certificate **tidak bisa terbit tanpa enrollment**
    
2. Enrollment **tidak bisa tanpa pembayaran sah**
    
3. Certificate **tidak bisa double**
    
4. Teacher **tidak bisa self-issue**
    
5. Backend **tidak bisa memalsukan enrollment**

---

### I.0.h. Kenapa desain ini efisien?

- Gas rendah
    
- Trust boundary jelas
    
- Aman dari manipulasi teacher & student
    
- Mudah di-extend ke:
    
    - Soulbound NFT
        
    - Credential standard
        
    - DID

---

### I.0.i. Status Setelah D

✔ Enrollment flow clean  
✔ Payment → Enrollment → Completion → Certificate **linear & audit-friendly**  
✔ Tidak ada state ambigu  
✔ Cocok untuk solo fullstack dev

---


---

# J. WEB2 BACKEND RESPONSIBILITY

### J.0.a. Prinsip Dasar (pegangan supaya tidak over-engineering)

1. **Web2 = orkestrator & validator**
    
2. **Web3 = source of truth finansial & sertifikat**
    
3. Backend **tidak dipercaya penuh**, tapi:
    
    - memverifikasi
        
    - menyaring
        
    - memutuskan kapan data boleh dikirim ke chain
        
4. Semua keputusan kritikal **punya bukti jejak**

---

### J.0.b. Responsibility Matrix (Ringkas & Tegas)

|Area|Web2 Backend|On-chain|
|---|---|---|
|Auth & session|✅|❌|
|Role (student / teacher / admin)|✅|❌|
|Status “tidak mampu”|✅|❌|
|Course content|✅|❌|
|Progress calculation|✅|❌|
|Task submission & review|✅|❌|
|Enrollment proof|❌|✅|
|Payment settlement|❌|✅|
|Certificate hash|❌|✅|

---

### J.0.c. API Layer (yang benar-benar perlu)

#### J.0.c.i. 1 Auth & Identity

```
POST   /auth/register
POST   /auth/login
POST   /auth/connect-wallet
GET    /me
```

Backend:

- JWT / session
    
- wallet ↔ user binding (1 wallet utama)

---

#### J.0.c.ii. 2 Course

```
POST   /courses
PUT    /courses/:id
POST   /courses/:id/publish
GET    /courses
GET    /courses/:id
```

Catatan:

- **Teacher hanya boleh edit course miliknya**
    
- `is_crowdfundable` hanya flag metadata

---

#### J.0.c.iii. 3 Enrollment & Payment Sync

```
POST /enroll/direct/prepare
POST /enroll/crowdfund/prepare
POST /enroll/sync-onchain
```

Flow:

1. Backend validasi:
    
    - user role
        
    - status course
        
2. Frontend trigger tx
    
3. Backend **sync tx hash**
    
4. Backend cek:
    
    - tx sukses
        
    - event valid
        
5. Backend simpan enrollment_ref (off-chain mirror)

---

#### J.0.c.iv. 4 Crowdfunding (Web2 control layer)

```
POST   /campaign/init
POST   /campaign/fund
POST   /campaign/execute
POST   /campaign/refund
GET    /campaign/:id
```

Backend:

- tidak menyimpan dana
    
- hanya:
    
    - state mirror
        
    - eligibility check (`tidak mampu == true`)
        
    - anti-abuse

---

#### J.0.c.v. 5 Progress & Completion

```
POST /progress/update
POST /task/submit
POST /task/:id/review
POST /course/:id/complete
```

Aturan:

- progress **dihitung sistem**
    
- teacher hanya:
    
    - approve / reject final task

---

#### J.0.c.vi. 6 Certificate

```
POST /certificate/commit
GET  /certificate/:id
```

`/commit`:

- backend:
    
    - generate completion_hash
        
    - call smart contract

---

### J.0.d. Database Design (Minimal tapi Aman)

#### J.0.d.i. Core Tables

##### users

```
id
email
password_hash
role
wallet_address
is_scholarship
status
```

##### courses

```
id
teacher_id
price
is_crowdfundable
status
```

##### enrollments (mirror)

```
id
user_id
course_id
onchain_enrollment_id
status
tx_hash
```

##### campaigns (mirror)

```
id
student_id
course_id
target_amount
state
vault_address
```

##### progress

```
enrollment_id
percentage
completed_at
```

##### certificates (mirror)

```
id
enrollment_id
onchain_cert_id
hash
```

> Semua mirror table → **read-only secara logika**, write hanya lewat event / verified call.

---

### J.0.e. Security Layer (WAJIB, bukan opsional)

#### J.0.e.i. 1 Trust Boundaries

- User → Backend → Blockchain
    
- **User tidak pernah kirim data completion ke chain langsung**

---

#### J.0.e.ii. 2 Hard Rules

1. Backend **tidak pernah menyimpan private key**
    
2. Semua tx:
    
    - user signed **atau**
        
    - relayer limited scope
        
3. Admin action:
    
    - audit log wajib

---

#### J.0.e.iii. 3 Abuse Prevention

##### Crowdfund

- max 1 active campaign / student / course
    
- rate limit funding
    
- cooldown refund
    

##### Course

- teacher tidak bisa enroll course sendiri
    
- teacher tidak bisa approve dirinya
    

##### Certificate

- hanya 1 issuance / enrollment
    
- completion hash immutable

---

### J.0.f. Anti-Cheat & Anti-Fraud Logic

|Area|Mitigasi|
|---|---|
|Fake completion|progress auto + task approval|
|Teacher collusion|teacher tidak trigger chain|
|Wallet swapping|wallet bound ke user|
|Refund abuse|state machine strict|
|Double certificate|on-chain invariant|

---

### J.0.g. Logging & Audit (ini sering diabaikan)

Minimal:

- user_action_log
    
- admin_action_log
    
- tx_sync_log
    

Tujuan:

- dispute handling
    
- legal readiness
    
- debugging on-chain mismatch

---

### J.0.h. Kenapa ini cocok untuk solo dev?

- Clear boundary → otak tidak terbakar
    
- Backend tetap sederhana
    
- Blockchain hanya dipanggil di **momen penting**
    
- Mudah diuji secara lokal

---

### J.0.i. Status Sistem Setelah E

✔ Web2 tidak over-power  
✔ Web3 tetap trust anchor  
✔ Flow jelas dari UI → API → Chain  
✔ Siap MVP production

---


---

# K. END-TO-END USER FLOW

### K.0.a. Prinsip Umum Flow

1. **Semua flow berbasis state**
    
2. **Tidak ada action lompat state**
    
3. **Web2 memvalidasi → Web3 mengunci**
    
4. Setiap role **punya jalur sempit (guardrail)**

---

### K.0.b. Student Flow (Pelajar)

#### K.0.b.i. 1 Entry & Identity

**State awal**

```
guest
```

**Flow**

1. Guest → Register
    
2. Login
    
3. Connect wallet
    
4. Backend bind:
    

```
user_id ↔ wallet_address
```

**Guard**

- 1 wallet = 1 user
    
- wallet tidak bisa dipindah tanpa admin

---

#### K.0.b.ii. 2 Explore Course

Student bisa:

- lihat semua course
    
- lihat detail:
    
    - price
        
    - crowdfundable (true / false)
        
    - status (open / closed)
        

**Tidak ada state change**

---

#### K.0.b.iii. 3 Enrollment Path (Cabang Penting)

##### Direct Enrollment

**Precondition**

- course.status = open
    
- user aktif
    

**Flow**

1. Klik `Enroll`
    
2. Backend `/enroll/direct/prepare`
    
3. Frontend trigger tx
    
4. Smart contract:
    
    - split fee
        
    - emit `EnrollmentCreated`
        
5. Backend sync event
    

**State**

```
enrollment = active
progress = 0%
```

---

##### Crowdfund Enrollment

**Precondition**

- is_scholarship = true
    
- course.is_crowdfundable = true
    
- tidak ada campaign aktif
    

**Flow**

1. Klik `Fund this course`
    
2. Backend `/campaign/init`
    
3. Campaign state:
    

```
pending
```

---

#### K.0.b.iv. 4 Crowdfunding Lifecycle (Student Side)

##### Funding Phase

- Student / donor fund campaign
    
- Smart contract:
    
    - simpan di vault
        
    - emit funding event
        
- Backend mirror total
    

**State transition**

```
pending → target_reached
```

---

##### Execution Phase

**Only student can execute**

1. Student klik `Fund Now`
    
2. Backend `/campaign/execute`
    
3. Smart contract:
    
    - transfer ke teacher
        
    - emit `CampaignExecuted`
        
4. Enrollment auto-created
    

**State**

```
campaign = executed
enrollment = active
```

---

##### Refund Phase (jika gagal)

**Condition**

- campaign expired
    
- target tidak tercapai
    

1. User withdraw
    
2. Smart contract refund
    
3. Backend sync

---

#### K.0.b.v. 5 Learning & Progress

**Progress engine**

- lesson completion
    
- quiz auto-grade
    
- final task → manual review
    

**Rule**

- teacher **tidak** bisa menaikkan progress manual
    

**State**

```
progress 0% → 100%
```

---

#### K.0.b.vi. 6 Completion & Certificate

**Trigger**

- progress = 100%
    
- final task approved
    

**Flow**

1. Backend generate `completion_hash`
    
2. Call certificate contract
    
3. Emit `CertificateIssued`
    

**Result**

- certificate bound to:
    

```
(student, course)
```

---

### K.0.c. Teacher Flow

#### K.0.c.i. 1 Onboarding

1. Register
    
2. Connect wallet
    
3. Role = teacher
    

**No verification flow dulu (MVP)**

---

#### K.0.c.ii. 2 Course Creation

**State**

```
draft
```

Teacher:

- input metadata
    
- syllabus
    
- tasks
    
- price
    
- crowdfundable flag

---

#### K.0.c.iii. 3 Publish Course

**Precondition**

- minimal content valid
    

**State**

```
draft → published
```

Course now visible & enrollable.

---

#### K.0.c.iv. 4 Crowdfund Interaction

Teacher:

- **tidak pegang dana**
    
- **tidak approve campaign**
    
- hanya menerima hasil jika executed

---

#### K.0.c.v. 5 Teaching & Review

Teacher can:

- review final task
    
- approve / reject
    

Teacher cannot:

- modify progress
    
- issue certificate
    
- trigger payment

---

#### K.0.c.vi. 6 Income Flow

- Direct enrollment → instant wallet
    
- Crowdfund → wallet after execution
    

No withdrawal request, no custodial step.

---

### K.0.d. Admin Flow

#### K.0.d.i. 1 User Control

Admin actions:

- set `is_scholarship = true`
    
- set user inactive
    

**Audit log mandatory**

---

#### K.0.d.ii. 2 Moderation

- ban abusive teacher
    
- freeze suspicious user
    

**Effect**

- backend deny new actions
    
- on-chain tetap immutable

---

#### K.0.d.iii. 3 Dispute Handling

Admin:

- lihat logs
    
- lihat tx hash
    
- **tidak bisa reverse chain**

---

### K.0.e. State Summary (Mental Model)

#### K.0.e.i. Enrollment

```
none → active → completed
```

#### K.0.e.ii. Campaign

```
pending → target_reached → executed
pending → expired → refunded
```

#### K.0.e.iii. Certificate

```
none → issued (immutable)
```

---

### K.0.f. Kenapa Flow Ini Aman & Efisien

- Tidak ada dual authority
    
- Semua dana → chain
    
- Semua logic berat → Web2
    
- Semua bukti final → Web3

---

### K.0.g. Checklist MVP Readiness

✔ Tidak ada circular dependency  
✔ Tidak ada ambiguous ownership  
✔ Semua role punya batas jelas  
✔ Bisa dikoding bertahap

---

Baik. Kita masuk ke **G → MVP Feature Slice & Build Order (mingguan untuk solo dev)**.  
Tujuan bagian ini **sangat praktis**: _kapan ngerjain apa, urutan salah = proyek mati_.

Aku akan pakai prinsip:

- **vertikal slice**, bukan layer-based
    
- **tiap minggu harus “usable”**
    
- **chain disentuh paling akhir yang perlu**

---


---

# L. MVP FEATURE SLICE & BUILD ORDER

### L.0.a. Prinsip Build Order (Pegangan Wajib)

1. **User & state dulu, fitur belakangan**
    
2. **Web2 dulu sampai mentok**
    
3. **Web3 hanya saat benar-benar dibutuhkan**
    
4. Jangan bangun fitur yang:
    
    - belum punya user action jelas
        
    - belum punya state final

---

### L.0.b. WEEK 0 — Foundation (wajib, cepat, jelek boleh)

**Target:** sistem bisa “hidup”, walau belum cantik.

#### L.0.b.i. Scope

- Repo setup
    
- Monorepo / split FE–BE
    
- ENV config
    
- DB schema final (ERD MVP)
    

#### L.0.b.ii. Deliverable

- Auth login basic
    
- Role (student / teacher / admin)
    
- Wallet connect (dummy accepted)
    

> ⚠️ Belum ada blockchain sungguhan

---

### L.0.c. WEEK 1 — Course Core (Teacher → Student Read)

**Target:** course bisa dibuat & dilihat.

#### L.0.c.i. Scope

- Course CRUD
    
- Publish / unpublish
    
- Course listing
    
- Detail page
    

#### L.0.c.ii. Done Criteria

- Teacher bisa publish
    
- Student bisa lihat detail
    
- Tidak bisa enroll

---

### L.0.d. WEEK 2 — Enrollment Direct (Web2 first, Web3 mock)

**Target:** flow uang & enroll sudah jelas.

#### L.0.d.i. Scope

- Enroll direct flow
    
- Enrollment table
    
- Progress engine (0%)
    

#### L.0.d.ii. Web3

- Mock tx hash
    
- Simulasi event listener
    

#### L.0.d.iii. Done Criteria

- Enrollment aktif
    
- Progress tercatat

---

### L.0.e. WEEK 3 — Real Payment (Web3 minimal)

**Target:** uang sungguhan jalan.

#### L.0.e.i. Scope

- Smart contract enrollment
    
- Fee split 1%
    
- Event sync ke backend
    

#### L.0.e.ii. Done Criteria

- Wallet teacher terima dana
    
- Enrollment auto-created
    
- Backend mirror valid
    

> Jangan sentuh crowdfund dulu

---

### L.0.f. WEEK 4 — Learning & Completion

**Target:** course bisa diselesaikan.

#### L.0.f.i. Scope

- Lesson progress
    
- Task submission
    
- Final task review
    
- Progress auto → 100%
    

#### L.0.f.ii. Done Criteria

- Course bisa selesai
    
- Tidak ada certificate dulu

---

### L.0.g. WEEK 5 — Certificate (Hash-only, non-transferable)

**Target:** trust anchor pertama.

#### L.0.g.i. Scope

- Completion hash
    
- Certificate contract
    
- Certificate view page
    

#### L.0.g.ii. Done Criteria

- 1 enrollment = 1 certificate
    
- Immutable

---

### L.0.h. WEEK 6 — Crowdfunding MVP

**Target:** fitur pembeda platform.

#### L.0.h.i. Scope

- Campaign init (restricted)
    
- Funding
    
- Vault contract
    
- Execute / refund
    

#### L.0.h.ii. Done Criteria

- Campaign state valid
    
- Enrollment tercipta setelah executed

---

### L.0.i. WEEK 7 — Admin & Anti-Abuse

**Target:** sistem tidak gampang rusak.

#### L.0.i.i. Scope

- Admin dashboard
    
- Scholarship flag
    
- Rate limit
    
- Audit log

---

### L.0.j. WEEK 8 — Hardening & Cut Scope

**Target:** layak dipakai orang luar.

#### L.0.j.i. Scope

- Error handling
    
- Gas failure
    
- UX clarity
    
- Docs singkat

---

### L.0.k. Feature Kill List (JANGAN DIBUAT)

❌ DAO  
❌ Voting  
❌ Fiat conversion  
❌ Multi-wallet  
❌ NFT marketplace  
❌ Reputation score

Semua ini **pasca-MVP**.

---

### L.0.l. Mental Model Mingguan (penting)

Setiap minggu tanyakan:

> “Jika aku berhenti minggu ini, apakah sistem masih masuk akal?”

Jika jawabannya “tidak” → urutan salah.

---

### L.0.m. Estimasi Realistis (solo dev)

|Minggu|Beban|
|---|---|
|0–2|ringan|
|3–4|berat (chain + logic)|
|5–6|kritikal|
|7–8|stabilisasi|

---

### L.0.n. Status Akhir Setelah G

✔ Kamu tahu **apa dikerjakan dulu**  
✔ Tidak lompat fitur  
✔ Tidak kehabisan energi di analisis  
✔ MVP siap validasi pasar

---


---

# M. TABEL PRIORITAS DAN DEFINITION OF DONE

### M.0.a. Tabel Pengerjaan MVP (Single Table, Scope Grouped)

> Catatan format:
> 
> - **Scope** diulang tapi _concise_ (grouping visual lewat isi, bukan section terpisah)
>     
> - **Features / Criteria / TODO** = bullet per baris
>     
> - **FE/BE** = enum (`FE`, `BE`, `FE+BE`)
>     
> - **Priority Sort** = 1 (tertinggi) → besar (lebih rendah)
>     

| SCOPE               | FEATURES                                                       | DESC                                                                                                                                                                        | CRITERIA                                                                                        | TODO LIST                                                         | FRONTEND / BACKEND | DoD                                                                                                                           | Priority Sort |
| ------------------- | -------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- | ----------------------------------------------------------------- | ------------------ | ----------------------------------------------------------------------------------------------------------------------------- | ------------- |
| Foundation          | - Auth basic<br>- Role system<br>- Wallet bind                 | Menyediakan fondasi identitas pengguna yang stabil dengan autentikasi, role yang eksplisit, dan binding wallet sebagai dasar semua aksi on-chain dan otorisasi selanjutnya. | - User bisa register & login<br>- Role konsisten (student/teacher/admin)<br>- 1 user ↔ 1 wallet | - Setup auth flow<br>- Role middleware<br>- Wallet connect & bind | FE+BE              | User dapat login, role dikenali sistem, wallet terikat permanen dan digunakan sebagai identitas blockchain tanpa error state. | 1             |
| Course Core         | - Course CRUD<br>- Publish workflow<br>- Course listing        | Memungkinkan teacher membuat dan mempublikasikan course dengan metadata yang cukup untuk dipelajari dan dievaluasi student sebelum enrollment.                              | - Draft tidak publik<br>- Published bisa dilihat student<br>- Teacher hanya edit miliknya       | - Course form<br>- Publish action<br>- Listing & detail page      | FE+BE              | Course dapat dibuat, diedit, dipublish, dan ditampilkan dengan status yang konsisten tanpa akses ilegal.                      | 2             |
| Enrollment (Direct) | - Direct enroll<br>- Enrollment record<br>- Progress init      | Menyediakan jalur enrollment langsung berbayar sebagai baseline monetisasi dan validasi flow sebelum crowdfunding.                                                          | - Payment valid<br>- Enrollment tercipta<br>- Progress mulai 0%                                 | - Prepare enroll API<br>- Trigger tx<br>- Sync tx event           | FE+BE              | Student berhasil enroll setelah pembayaran, enrollment tercatat on-chain & off-chain, progress siap dilacak.                  | 3             |
| Payment On-chain    | - Fee split<br>- Event sync<br>- Error handling                | Mengintegrasikan smart contract pembayaran sebagai sumber kebenaran transaksi dan memastikan backend hanya melakukan sinkronisasi, bukan kontrol dana.                      | - Dana masuk wallet teacher<br>- Fee platform konsisten<br>- Tx failure ter-handle              | - Deploy contract<br>- Event listener<br>- Tx verification        | BE                 | Pembayaran on-chain sukses, backend mencerminkan state chain tanpa mismatch atau manipulasi.                                  | 4             |
| Learning Flow       | - Progress tracking<br>- Task submission<br>- Review flow      | Mengelola proses belajar sepenuhnya off-chain dengan aturan ketat agar completion hanya terjadi melalui proses yang sah dan terukur.                                        | - Progress otomatis<br>- Task bisa direview<br>- Tidak ada manual override                      | - Progress engine<br>- Task API<br>- Review UI                    | FE+BE              | Progress bergerak deterministik sampai 100%, task review tercatat, tanpa shortcut state.                                      | 5             |
| Certificate         | - Completion hash<br>- Issue certificate<br>- Certificate view | Memberikan bukti kelulusan immutable yang terikat ke enrollment dan course sebagai trust anchor utama sistem.                                                               | - 1 enrollment = 1 cert<br>- Cert immutable<br>- Bisa diverifikasi                              | - Hash generator<br>- Issue tx<br>- Cert page                     | FE+BE              | Certificate terbit hanya setelah completion sah, dapat diverifikasi on-chain, dan tidak bisa diduplikasi.                     | 6             |
| Crowdfunding        | - Campaign init<br>- Funding<br>- Execute / refund             | Menyediakan mekanisme pembiayaan alternatif yang terkontrol ketat untuk student tidak mampu tanpa mencederai alur enrollment.                                               | - Target jelas<br>- Dana aman di vault<br>- Enrollment pasca execute                            | - Campaign API<br>- Vault contract<br>- State sync                | FE+BE              | Campaign mengikuti state machine benar, dana aman, enrollment hanya terjadi setelah eksekusi sah.                             | 7             |
| Admin & Security    | - Scholarship flag<br>- Moderation<br>- Audit log              | Memberikan kontrol minimal namun penting untuk menjaga integritas sistem tanpa mengintervensi data on-chain.                                                                | - Admin action logged<br>- Abuse bisa dihentikan<br>- Tidak ada chain override                  | - Admin UI<br>- Audit table<br>- Rate limit                       | FE+BE              | Admin dapat mengelola risiko dan abuse dengan jejak audit lengkap tanpa melanggar trust boundary.                             | 8             |

---

### M.0.b. Koreksi & Catatan Kritis (Penting)

#### M.0.b.i. Kekurangan yang **sering fatal** jika tidak disadari

- **Tidak ada explicit “TX Sync Reliability Layer”**
    
    - Saran: tambahkan _retry + reconciliation job_ (cron / queue)
        
- **Belum ada “chain reorg / tx dropped handling”**
    
    - Minimal: status `PENDING_SYNC`, jangan asumsi tx final
        
- **Belum ada cut-scope UX rule**
    
    - Saran: tandai jelas di FE state:
        
        - `awaiting_tx`
            
        - `confirmed`
            
        - `failed`
            

#### M.0.b.ii. Tambahan kecil tapi berdampak besar

- Tambahkan **DoD global**:
    
    > “Tidak ada state yang hanya hidup di frontend tanpa sumber backend atau on-chain.”
    
- Tambahkan **priority guard**:
    
    - Priority 1–3 = **tidak boleh tertunda**
        
    - Priority ≥6 = **boleh dipotong jika waktu habis**
        

#### M.0.b.iii. Validasi terhadap goal solo dev

Struktur ini:

- **Tidak tumpang tindih**
    
- Bisa dikerjakan **vertikal**
    
- Aman jika proyek berhenti di minggu mana pun
---
