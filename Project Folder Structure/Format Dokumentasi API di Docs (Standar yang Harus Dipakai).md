Setiap endpoint harus punya struktur berikut:

---

## 📌 Endpoint: POST /api/auth/login

### Deskripsi

Autentikasi user menggunakan email dan password.

---

### Arguments (Request Body)

|Name|Type|Required|Description|
|---|---|---|---|
|email|string|yes|Email terdaftar|
|password|string|yes|Password user|

Type Definition:

```ts
interface LoginRequest {
  email: string
  password: string
}
```

---

### Returns

Status: `200 OK`

```ts
interface LoginResponse {
  accessToken: string
  refreshToken: string
  user: {
    id: string
    email: string
    role: 'ADMIN' | 'USER'
  }
}

```

---

### Error Responses

|Status|Description|
|---|---|
|401|Invalid credentials|
|400|Validation error|

---

### Tail Notes

- Access token expired: 15m
    
- Refresh token expired: 7d
    
- Rate limit: 5 attempt / 5 menit