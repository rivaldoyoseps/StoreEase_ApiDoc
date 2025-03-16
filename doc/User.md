# User API Spec

## Update Password

Endpoints : PATCH /api/users/update-password

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
    "oldPassword": "Rahasia123!",
    "newPassword": "PasswordBaru123!"
}
```

Response Body Success (200):

```json
{
    "status": "success",
    "message": "Password updated successfully"
}
```

Response Body Error :

1. Jika password baru tidak valid (400)

```json
{
    "status": "error",
    "message": "Invalid password format",
    "errors": {
        "newPassword": "Password must be at least 8 characters and contain a number"
    }
}
```

2.JIka password lama salah (401)

```json
{
    "status": "error",
    "message": "Old password is incorrect"
}
```

## Update Detail User

ENDPOINT: PATCH /api/users/me

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
    "phoneNumber": "08109340193480",
    "email": "yosep@gmail.com",
    "profilePicture": "https://storage.example.com/uploads/profile123.jpg",
    "address": {
        "street": "Jl. Merdeka No. 10",
        "city": "Jakarta",
        "postalCode": "12345",
        "address_detail": "di depan indomaret"
    }
}
```

Response Body Success (200)

```json
{
    "status": "success",
    "message": "Profile updated successfully",
    "data": {
        "fullname": "Yosep R Silaban",
        "phoneNumber": "08109340193480",
        "email": "yosep@gmail.com",
        "birthDate": "1999-09-09",
        "profilePicture": "https://storage.example.com/uploads/profile123.jpg",
        "address": {
            "street": "Jl. Merdeka No. 10",
            "city": "Jakarta",
            "postalCode": "12345"
        }
    }
}
```

Response Body Error:

1. Jika User Tidak ditemukan (404)

```json
{
    "status": "error",
    "message": "User not found"
}
```

2. Jika Format Data Tidak Valid (400)

```json
{
    "status": "error",
    "message": "Invalid input",
    "errors": {
        "email": "Email format is incorrect",
        "phoneNumber": "Phone number must be numeric"
    }
}
```

3. Jika Token Tidak Ada (401)

```json
{
    "status": "error",
    "message": "Unauthorized. Token is required"
}
```

## Delete User Account

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
{ "status": "error", "message": "Incorrect password" }
```

1. Tidak Login / toke tidak ada

```json
{ "status": "error", "message": "Unauthorized. Token is required" }
```

1. Password Salah / token kadaluarsa

```json
{ "status": "error", "message": "Invalid or expired token" }
```

1. UserAccount tidak ditemukan

```json
{ "status": "error", "message": "User not found" }
```

### Get Address for Current Logged-in User

Endpoint: GET /api/users/me/address

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
    "status": "success",
    "message": "User addresses retrieved successfully",
    "data": {
        "userAccountId": "qetqewtqweteqwt34123",
        "username": "yoseprivaldos",
        "addresses": {
            "id": "addr-123",
            "street": "Jl. Merdeka No. 10",
            "city": "Jakarta",
            "postalCode": "12345",
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
{ "status": "error", "message": "No address found for this user" }
```
