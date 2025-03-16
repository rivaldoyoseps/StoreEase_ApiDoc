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
    "status": "success",
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
    "status": "error",
    "message": "Invalid Input",
    "errors": {
        "payment_method": "Payment method is required"
    }
}
```

2. Jika transaksi tidak ditemukan (404 - Not Found)

```json
{
    "status": "error",
    "message": "Transaction not found"
}
```

3. Jika token tidak valid (401 - Unauthorized)

```json
{
    "status": "error",
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
    "status": "success",
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
    "status": "error",
    "message": "Payment transaction not found"
}
```

2. Jika token tidak valid

```json
{
    "status": "error",
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
    "status": "success",
    "message": "webhook process successfully"
}
```

RESPONSE ERROR:

1. Jika format request tidak valid (400 - Bad Request)

```json
{
    "status": "error",
    "message": "Invalid webhook payload"
}
```

2. Jika transaksi tidak ditemukan (404 - Not Found)

```json
{
    "status": "error",
    "message": "transaction not found"
}
```
