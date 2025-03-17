# User API Spec

## Update Password

Endpoints : PATCH /vi/api/users/update-password

Headers:

```json
{
    "Content-Type": "application/json",
    "Authorization": "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

Request Body:

```json
{
    "old_password": "Rahasia123!",
    "new_password": "PasswordBaru123!"
}
```

Response Body Success (200):

```json
{
    "status": 200,
    "message": "Password updated successfully"
}
```

Response Body Error :

1. Jika password baru tidak valid (400)

```json
{
    "status": 400,
    "message": "Invalid password format",
    "errors": {
        "new_password": "Password must be at least 8 characters and contain a number"
    }
}
```

2.JIka password lama salah (400)

```json
{
    "status": 400,
    "message": "Old password is incorrect"
}
```

## Update Detail User

ENDPOINT: PATCH /v1/api/users/me

Header:

```json
{
    "Authorization": "Bearer <user-token>"
}
```

Request Body:

```json
{
    "fullname": "Yosep R Silaban",
    "phone_number": "08109340193480",
    "email": "yosep@gmail.com",
    "profile_picture": "https://storage.example.com/uploads/profile123.jpg",
    "address": {
        "street": "Jl. Merdeka No. 10",
        "city": "Jakarta",
        "postal_code": "12345",
        "address_detail": "di depan indomaret"
    }
}
```

Response Body Success (200)

```json
{
    "status": 200,
    "message": "Profile updated successfully",
    "data": {
        "fullname": "Yosep R Silaban",
        "phone_number": "08109340193480",
        "email": "yosep@gmail.com",
        "birth_date": "1999-09-09",
        "profile_picture": "https://storage.example.com/uploads/profile123.jpg",
        "address": {
            "street": "Jl. Merdeka No. 10",
            "city": "Jakarta",
            "postal_code": "12345"
        }
    }
}
```

Response Body Error:

1. Jika User Tidak ditemukan (404)

```json
{
    "status": 404,
    "message": "User not found"
}
```

2. Jika Format Data Tidak Valid (400)

```json
{
    "status": 400,
    "message": "Invalid input",
    "errors": {
        "email": "Email format is incorrect",
        "phone_number": "Phone number must be numeric"
    }
}
```

3. Jika Token Tidak Ada (401)

```json
{
    "status": 401,
    "message": "Unauthorized. Token is required"
}
```

## Delete User Account

ENDPOINT : DELETE /v1/api/users/{userAccountId}

Header:

```json
{
    "Content-Type": "application/json",
    "Authorization": "Bearer <user-token>"
}
```

Request Body

```json
{
    "password": "rahasia123"
}
```

Response Success

```json
{
    "status": "success",
    "message": "Account deleted successfully"
}
```

Response Error

1. Password Salah

```json
{ "status": 401, "message": "Incorrect password" }
```

1. Tidak Login / toke tidak ada

```json
{ "status": 401, "message": "Unauthorized. Token is required" }
```

1. Password Salah / token kadaluarsa

```json
{ "status": 401, "message": "Invalid or expired token" }
```

1. UserAccount tidak ditemukan

```json
{ "status": 404, "message": "User not found" }
```

### Get Address for Current Logged-in User

Endpoint: GET /v1/api/users/me/address

Headers:

```json
{
    "Content-Type": "application/json",
    "Authorization": "Bearer <user-token>"
}
```

Response Success (200)

```json
{
    "status": 200,
    "message": "User addresses retrieved successfully",
    "data": {
        "use_account_id": "qetqewtqweteqwt34123",
        "username": "yoseprivaldos",
        "addresses": {
            "id": "addr-123",
            "street": "Jl. Merdeka No. 10",
            "city": "Jakarta",
            "postal_code": "12345",
            "country": "Indonesia"
        }
    }
}
```

Response Error

1. Tidak Login/Token tidak ada (sama sepert error token yang lain) (401)
2. Token tidak valid atau expired (sama seperti error token expired yang lain) (401)
3. User AccountId tidak ditemukan (sama seperti error userAccountId yang lain) (404)
4. User ditemukan tapi belum punya alamat

```json
{ "status": 404, "message": "No address found for this user" }
```
