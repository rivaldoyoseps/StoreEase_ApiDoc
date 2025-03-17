### Membuat Transaksi Pembayaran

Endpoint : POST /vi/api/payments/{transactiondId}

HEADERS:

```json
{
    "Authorization": "Bearer <JWT_TOKEN>",
    "Content-Type": "application/json"
}
```

REQUEST BODY:

```json
{
    "payment_method": "midtrans"
}
```

RESPONSE SUCCESS:

```json
{
    "status": 201,
    "message": "Payment transaction created successfully",
    "data": {
        "payment_id": "pay-001",
        "transaction_id": "trx-123",
        "payment_method": "midtrans",
        "amount": 75000,
        "status": "pending",
        "redirect_url": "https://midtrans.com/payment-link"
    }
}
```

RESPONSE ERROR

1. Jika data tidak lengkap

```json
{
    "status": 400,
    "message": "Invalid Input",
    "errors": {
        "payment_method": "Payment method is required"
    }
}
```

2. Jika transaksi tidak ditemukan (404 - Not Found)

```json
{
    "status": 404,
    "message": "Transaction not found"
}
```

3. Jika token tidak valid (401 - Unauthorized)

```json
{
    "status": 401,
    "message": "Unauthorized. Token is required"
}
```

### Ambil Status Pembayaran

Endpoint: GET /v1/api/payments/{transactionsId}

HEADER :

```json
{
    "Authorization": "Bearer <JWT_TOKEN>",
    "Content-Type": "application/json"
}
```

RESPONSE SUCCESS (200) :

```json
{
    "status": 200,
    "message": "Payment status retrieved successfully",
    "data": {
        "payment_id": "pay-001",
        "transaction_id": "trx-123",
        "payment_method": "midtrans",
        "amount": 75000,
        "status": "settlement",
        "paid_at": "2025-03-14T12:30:00Z"
    }
}
```

RESPONSE ERROR

1. Jika transaksi pembayaran tidak ditemukan (404 - Not Found)

```json
{
    "status": 404,
    "message": "Payment transaction not found"
}
```

2. Jika token tidak valid

```json
{
    "status": 401,
    "message": "Unauthorized. Token is required"
}
```

### Webhook Midtrans

Endpoint POST /v1/api/payments/webhook
request body:

Headers:

```json
{
    "Content-Type": "application/json"
}
```

REQUEST BODY:

```json
{
    "order_id": "INV-20240312-001",
    "transaction_status": "settlement",
    "gross_amount": "50000"
}
```

RESPONSE BODY:

```json
{
    "status": 200,
    "message": "webhook process successfully"
}
```

RESPONSE ERROR:

1. Jika format request tidak valid (400 - Bad Request)

```json
{
    "status": 400,
    "message": "Invalid webhook payload"
}
```

2. Jika transaksi tidak ditemukan (404 - Not Found)

```json
{
    "status": 404,
    "message": "transaction not found"
}
```
