# AUTHENTICATION

## Register ADMIN & USER API

Endpoints: POST /v1/api/auth/register/{admin/user}

Headers:

```json
{
    "Content-Type": "application/json",
    "Authorization": "Bearer <superadmin-token>"
}
```

Request Body :

```json
{
    "fullname": "Yosep R Silaban",
    "phoneNumber": "08109340193480",
    "email": "yosep@gmail.com",
    "username": "yoseprivaldos",
    "password": "rahasia"
}
```

Response Body Success :

```json
{
    "status": "success created (201)",
    "message": "Admin account registerd successfully",
    "data": {
        "id": "a1b2c3d4-e5f6-7890-gh12-ijkl34567890",
        "username": "yoseprivaldos",
        "name": "Yosep R Silaban",
        "email": "yosep@gmail.com",
        "phoneNumber": "08109340193480",
        "createdAt": "2025-03-16T10:00:00Z"
    }
}
```

Response Body Error:

1. Email atau Username Sudah terdaftar (409)

```json
{
    "status": "error",
    "message": "Email or username already registered"
}
```

2. Password Tidak memenuhi syarat (400)

```json
{
    "status": "error",
    "message": "Password must be at least 8 characters long and include uppercase, lowercase, number, and special character"
}
```

3. Data tidak valid (400)

```json
{
    "status": "error",
    "message": "Invalid input",
    "errors": {
        "email": "Invalid email format",
        "password": "Password is too weak"
    }
}
```

4. Tidak memiliki Izin (403)

```json
{
    "status": "error",
    "message": "You do not have permission to register an admin"
}
```

### RE

## Login User API

Endpoinst : POST /v1/api/{user/login}/login

Headers:

```json
{
    "Content-Type": "application/json"
}
```

Request Body:

```json
{
    "username": "yoseprivaldos",
    "password": "rahasia"
}
```

1. Response Body Success (200):

```json
{
    "status": "success",
    "message": "Login successful",
    "data": {
        "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
    }
}
```

JWT YANG DIHASILKAN

```json
{
    "id": "a1b2c3d4-e5f6-7890-gh12-ijkl34567890",
    "username": "yoseprivaldos",
    "role": "admin",
    "exp": 1710804600
}
```

Response Body Error:

1. Email atau Password Salah (401)

```json
{
    "status": "error",
    "message": "Invalid email or password"
}
```

2. Input Tidak Valid (400)

```json
{
    "status": "error",
    "message": "Invalid input",
    "errors": {
        "email": "Email format is incorrect"
    }
}
```

## LogOut User API (Kalau Pakai)

Endpoint : Endpoint: POST /v1/api/auth/logout

Headers:

```json
{
    "Authorization": "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

Response Success (200 OK)

```json
{
    "status": "success",
    "message": "Logout successful"
}
```
