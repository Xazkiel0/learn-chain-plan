Ini penting untuk menjaga FE-BE tetap sinkron.

```
/packages/types
│
├── api/
│   ├── auth.types.ts
│   └── user.types.ts
│
├── entities/
├── common/
└── index.ts
```

Contoh:
```ts title:packages/types/api/auth.types.ts

export interface LoginRequest {
  email: string
  password: string
}

export interface LoginResponse {
  accessToken: string
  refreshToken: string
  user: User
}
``` 

FE import:
```ts title:import-example.ts
import { LoginResponse } from '@repo/types'
``` 
