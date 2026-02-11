# 1️⃣ Shared UI Component Strategy (FE + Docs tanpa duplikasi)

Semua komponen UI reusable ditempatkan di:

```
/packages/ui
```

Baik FE maupun Docs akan mengimpor dari:

```
@repo/ui
```

Struktur UI package:

```
/packages/ui
│
├── components/
│   ├── atoms/
│   ├── molecules/
│   ├── organisms/
│   └── layouts/
│
├── hooks/
├── styles/
├── theme/
└── index.ts
```

Ini memastikan:

- Tidak ada double component
    
- FE dan Docs menggunakan source yang sama
    
- Dokumentasi selalu sinkron dengan production component
