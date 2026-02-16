## 13.1 Tujuan File Ini

File ini mendefinisikan:

- Standar penulisan kode
    
- Struktur repository
    
- Branching strategy
    
- Pull request rules
    
- Code review discipline
    
- Documentation minimum
    

Tujuannya:

- Mencegah chaos saat tim bertambah
    
- Menjaga konsistensi
    
- Mengurangi technical debt
    
- Menghindari konflik integrasi
    

---

## 13.2 Core Principles

1. **Readability > Cleverness**  
    Kode harus mudah dipahami tim lain.
    
2. **Explicit > Implicit**  
    Hindari magic behavior.
    
3. **Small & Modular**  
    Fungsi dan file tidak boleh membengkak.
    
4. **Single Responsibility**  
    Satu modul → satu tanggung jawab utama.
    
5. **No Silent Side Effect**  
    Semua perubahan state harus jelas.
    

---

## 13.3 Repository Structure

### 13.3.1 Frontend

```
/src
  /components
  /features
  /pages (or app/)
  /hooks
  /lib
  /utils
  /types
```

Guideline:

- Jangan campur logic bisnis dengan UI rendering.
    
- Komponen reusable dipisahkan dari feature-specific component.
    

---

### 13.3.2 Backend

```
/src
  /modules
    /auth
    /users
    /courses
    /funding
  /common
  /middleware
  /config
```

Rule:

- Setiap module punya:
    
    - controller
        
    - service
        
    - dto
        
    - entity/model
        

---

## 13.4 Coding Conventions

### 13.4.1 Naming Rules

- camelCase → variable & function
    
- PascalCase → class & component
    
- UPPER_SNAKE_CASE → constant
    
- kebab-case → file non-component
    
- Component file → PascalCase.tsx
    

Contoh:

```
createCourse()
FundingService
FUNDING_LIMIT
course-detail.tsx
```

---

### 13.4.2 Function Rules

- Maksimal ±40–60 baris
    
- Maksimal 3–4 parameter (lebih → gunakan object)
    
- Hindari nested logic dalam
    

---

### 13.4.3 Comment Rules

Comment hanya untuk:

- Business rule penting
    
- Security warning
    
- Non-obvious decision
    

Tidak perlu komentar untuk hal yang jelas.

---

## 13.5 Type Safety (Non-Negotiable)

- Gunakan TypeScript strict mode
    
- Hindari `any`
    
- Gunakan shared type antara frontend & backend jika memungkinkan
    

Type mismatch adalah sumber bug integrasi.

---

## 13.6 Branching Strategy

Gunakan model sederhana berbasis GitFlow ringan.

### Branch utama:

- `main` → production
    
- `develop` → staging / integration
    
- `feature/*`
    
- `fix/*`
    
- `hotfix/*`
    

Flow:

1. Feature dibuat dari `develop`
    
2. PR ke `develop`
    
3. Setelah stabil → merge ke `main`
    

Hotfix:

- Dari `main`
    
- Merge kembali ke `develop`
    

---

## 13.7 Pull Request Rules

PR tidak boleh:

- Lebih dari ±400–500 line perubahan (kecuali migrasi besar)
    
- Tanpa deskripsi
    
- Tanpa test (jika logic signifikan)
    

PR harus berisi:

- Ringkasan perubahan
    
- Alasan perubahan
    
- Screenshot (jika UI)
    
- Dampak ke database (jika ada)
    

---

## 13.8 Code Review Rules

Minimal 1 reviewer untuk merge.

Reviewer harus cek:

1. Logic correctness
    
2. Security implication
    
3. Breaking change
    
4. Edge case
    
5. Naming clarity
    

Reviewer bukan hanya cek formatting.

---

## 13.9 Commit Message Standard

Format:

```
type(scope): short description
```

Contoh:

```
feat(course): add funding validation
fix(auth): prevent nonce reuse
refactor(funding): simplify tx handling
```

Types:

- feat
    
- fix
    
- refactor
    
- chore
    
- docs
    
- test
    

---

## 13.10 Linting & Formatting

Wajib:

- ESLint
    
- Prettier
    
- Pre-commit hook
    

Tidak boleh ada:

- Console log di production
    
- Unused import
    
- Dead code
    

---

## 13.11 Environment Configuration

- Tidak ada secret di repo
    
- Gunakan `.env`
    
- `.env.example` wajib tersedia
    
- Production env terpisah
    

---

## 13.12 Migration Discipline

Setiap perubahan schema:

- Harus melalui migration
    
- Tidak boleh manual edit DB production
    
- Migration harus diuji di staging
    

---

## 13.13 Technical Debt Policy

Jika ada:

- Shortcut untuk MVP
    
- Temporary hack
    

Harus diberi:

```
TODO: explain why and when to fix
```

Dan dicatat dalam backlog.

---

## 13.14 Definition of Done (Developer Level)

Sebuah feature dianggap selesai jika:

- Code sudah direview
    
- Test minimal ada
    
- Tidak ada lint error
    
- Tidak ada console warning
    
- Dokumentasi endpoint diperbarui
    
- Tidak merusak feature lain
    

---

## 13.15 Anti-Pattern yang Dilarang

- Merge langsung ke main
    
- Push force tanpa koordinasi
    
- Bypass review
    
- Copy-paste tanpa pahami logic
    
- Commit besar tanpa deskripsi
    

---

## 13.16 Scaling Team Consideration

Jika tim >5 orang:

- Mulai enforce stricter review
    
- Tambahkan CI pipeline wajib
    
- Pisahkan code ownership per module
    

---

# Kenapa File Ini Penting?

Arsitektur bagus tidak berarti jika:

- Kode berantakan
    
- Tidak ada review
    
- Feature saling merusak
    

Standar development adalah pengaman kualitas jangka panjang.