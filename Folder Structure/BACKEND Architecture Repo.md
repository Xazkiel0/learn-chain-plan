```
/apps/be
│
├── src/
│   ├── domain/             # Business core (pure logic)
│   │   ├── entities/
│   │   ├── value-objects/
│   │   ├── repositories/
│   │   └── services/
│   │
│   ├── application/        # Use cases
│   │   ├── auth/
│   │   └── user/
│   │
│   ├── infrastructure/     # DB, external services
│   │   ├── database/
│   │   ├── orm/
│   │   └── repositories/
│   │
│   ├── interfaces/         # Controllers, routes
│   │   ├── http/
│   │   │   ├── controllers/
│   │   │   ├── routes/
│   │   │   └── middlewares/
│   │
│   └── config/
│
├── tests/
└── server.ts
```

Prinsip:
- Domain tidak tahu HTTP
- Application tidak tahu framework
- Infrastructure implement repository
- Interfaces hanya adapt layer