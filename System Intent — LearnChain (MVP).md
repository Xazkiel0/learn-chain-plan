

## 1. Tujuan Sistem

- Membuka akses bagi pengajar sebagai penyedia course.
    
- Menyediakan pembayaran course berbasis kriptokurensi tanpa kustodi (non-custodial).
    
- Memberikan sertifikat penyelesaian course yang immutable (NFT atau hash on-chain).
    
- Menyediakan mekanisme crowdfunding terkontrol bagi user dengan status "tidak mampu" yang menempel pada entitas user.
    

## 2. Role & Hak Akses

### Guest (dan semua role sebelum login)

- Melihat daftar course dan detail course.
    
- Registrasi dan login.
    
- Connect wallet.
    

### Pelajar (extend Guest)

- Enroll dan mengikuti course.
    
- Menginisiasi campaign crowdfunding (hanya jika status "tidak mampu").
    
- Mencetak / mengklaim sertifikat setelah course selesai.
    

### Pengajar

- Membuat dan mengelola course.
    
- Menandai course sebagai crowdfundable.
    
- Menetapkan course sebagai closed (tidak menerima enrollment baru).
    

### Admin

- Menetapkan status pelajar sebagai "tidak mampu".
    
- Menonaktifkan (ban) user.
    

## 3. Alur Dana

- Semua user harus connect wallet untuk melakukan enrollment.
    
- Pembayaran enrollment course langsung masuk ke wallet pengajar melalui transaksi blockchain (tanpa kustodi).
    
- Platform mengambil fee 1% dari pembayaran course ke wallet perusahaan.
    
- Dana crowdfunding disimpan di vault crowdfunding.
    
- Jika target crowdfunding tidak tercapai, user dapat menarik dana tanpa dikenakan fee.
    

## 4. Definisi Course Selesai

- Course dianggap selesai jika pelajar mencapai progress 100%.
    
- Pelajar telah menyelesaikan sylabus terakhir dan tugas akhir.
    

## 5. Definisi Campaign Sukses

- Campaign dianggap sukses ketika total funding mencapai harga course.
    
- Pelajar secara eksplisit menyetujui dan mengeksekusi aksi "fund now".