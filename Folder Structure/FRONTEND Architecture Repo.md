
```
/apps/fe
│
├── app/                    # Next.js / Router
│
├── modules/                # Feature-based structure
│   ├── auth/
│   ├── dashboard/
│   └── user/
│
├── services/               # API layer (fetchers)
├── store/                  # State management
├── lib/                    # App-specific utilities
├── constants/
├── types/                  # Local FE types (jika tidak global)
└── middleware/

```


Prinsip:
- Feature-driven
- UI ambil dari @repo/ui
- Types ambil dari @repo/types
- Tidak boleh import langsung dari BE