### CREATE CATEGORY SERVICE

ENDPOINT : POST /v1/api/category

Headers:

```json
{
    "Content-Type": "application/json",
    "Authorization": "Bearer <admin-token>"
}
```

Request Body:

```json
{
    "name": "Small",
    "description": "Safe and secure premium storage service",
    "max_price": 50000,
    "pricing_rule": {
        "base_price": 5000,
        "price_per_kg": 5000,
        "price_per_m3": 10000,
        "min_weight": 1,
        "max_weight": 10
    }
}
```

Response SUccess

```json
{
    "status": "success",
    "message": "Category created successfully",
    "data": {
        "id": "cat-123",
        "name": "Premium Storage",
        "description": "Safe and secure premium storage service",
        "max_price": 500000,
        "pricing_rule": {
            "id": "rule-001",
            "base_price": 50000,
            "price_per_kg": 5000,
            "price_per_m3": 10000,
            "min_weight": 1,
            "max_weight": 10
        }
    }
}
```

Response Error

1. Jika Data Tidak Lengkap (400)

```json
{
    "status": "error",
    "message": "Invalid input",
    "errors": {
        "name": "Category name is required",
        "pricing_rule": "Pricing rule is required"
    }
}
```

2. Jika Admin tidak memiliki akses

```json
{
    "status": "error",
    "message": "Forbidden. Only admins can create categories"
}
```

3. Jika token tidak ada atau tidak valid (401)

```json
{
    "status": "error",
    "message": "Unauthorized. Token is required"
}
```

### UPDATE CATEGORY SERVICE

ENDPOINT : PATCH v1//api/category

Headers:

```json
{
    "Content-Type": "application/json",
    "Authorization": "Bearer <admin-token>"
}
```

Request Body:

```json
{
    "categoryId": "akdgakgsdhgjsdagh8395u1923875",
    "name": "Updated Storage",
    "description": "Updated description",
    "max_price": 600000,
    "pricing_rule": {
        "base_price": 55000,
        "price_per_kg": 5500,
        "price_per_m3": 11000,
        "min_weight": 2,
        "max_weight": 15
    }
}
```

Response SUccess

```json
{
    "status": "success",
    "message": "Category update successfully",
    "data": {
        "id": "cat-123",
        "name": "Premium Storage",
        "description": "Safe and secure premium storage service",
        "max_price": 500000,
        "pricing_rule": {
            "id": "rule-001",
            "base_price": 50000,
            "price_per_kg": 5000,
            "price_per_m3": 10000,
            "min_weight": 1,
            "max_weight": 10
        }
    }
}
```

Response Error

1. Jika Data Tidak Lengkap (400)

```json
{
    "status": "error",
    "message": "Invalid input",
    "errors": {
        "name": "Category name is required",
        "pricing_rule": "Pricing rule is required"
    }
}
```

2. Jika Admin tidak memiliki akses

```json
{
    "status": "error",
    "message": "Forbidden. Only admins can create categories"
}
```

3. Jika Kategori tidak ditemukan (404)

```json
{
    "status": "error",
    "message": "Category not found"
}
```

### GET ALL CATEGORY SERVICE

ENDPOINT : GET /v1/api/categories?page={page}&size={size}

Headers:

```json
{
    "Content-Type": "application/json",
    "Authorization": "Bearer <admin-token>"
}
```

Response SUccess

```json
{
    "status": "success",
    "message": "Categories retrieved successfully",
    "data": [
        {
            "id": "cat-123",
            "name": "Premium Storage",
            "description": "Safe and secure premium storage service",
            "max_price": 500000,
            "pricing_rule": {
                "id": "rule-001",
                "base_price": 50000,
                "price_per_kg": 5000,
                "price_per_m3": 10000,
                "min_weight": 1,
                "max_weight": 10
            }
        },
        {
            "id": "cat-124",
            "name": "Standard Storage",
            "description": "Affordable and reliable storage",
            "max_price": 300000,
            "pricing_rule": {
                "id": "rule-002",
                "base_price": 30000,
                "price_per_kg": 3000,
                "price_per_m3": 7000,
                "min_weight": 1,
                "max_weight": 20
            }
        }
    ],
    "pagination": {
        "current_page": 1,
        "total_pages": 5,
        "total_items": 50,
        "size_per_page": 10
    }
}
```

Response Error

1. Jika halaman tidak ditemukan (404)

```json
{
    "status": "error",
    "message": "Page not found"
}
```

2. Jika Parameter tidak valid (400)

```json
{
    "status": "error",
    "message": "Invalid pagination parameters",
    "errors": {
        "page": "Page must be a positive integer",
        "size": "Size must be between 1 and 100"
    }
}
```

3. Jika Token tidak ada atau tidak valid (401)

```json
{
    "status": "error",
    "message": "Unauthorized. Token is required"
}
```

### GET BY ID CATEGORY SERVICE

ENDPOINT : GET /v1/api/category/{categoryId}

Headers:

```json
{
    "Content-Type": "application/json",
    "Authorization": "Bearer <admin-token>"
}
```

Response SUccess

```json
{
    "status": "success",
    "message": "Category retrieved successfully",
    "data": {
        "id": "cat-123",
        "name": "Premium Storage",
        "description": "Safe and secure premium storage service",
        "max_price": 500000,
        "pricing_rule": {
            "id": "rule-001",
            "base_price": 50000,
            "price_per_kg": 5000,
            "price_per_m3": 10000,
            "min_weight": 1,
            "max_weight": 10
        }
    }
}
```

Response Error

1. Jika Id tidak valid (400)

```json
{
    "status": "error",
    "message": "Invalid category ID"
}
```

2. Jika Admin tidak memiliki akses

```json
{
    "status": "error",
    "message": "Forbidden. Only admins can create categories"
}
```

3. Jika Kategori tidak ditemukan (404)

```json
{
    "status": "error",
    "message": "Category not found"
}
```

4. Jika token tidak ada atau tidak valid (401)

```json
{
    "status": "error",
    "message": "Unauthorized. Token is required"
}
```

### DELETE BY ID CATEGORY SERVICE

ENDPOINT : DELETE /v1/api/category/{categoryId}

Headers:

```json
{
    "Content-Type": "application/json",
    "Authorization": "Bearer <admin-token>"
}
```

Response SUccess

```json
{
    "status": "success",
    "message": "Category deleted successfully"
}
```

Response Error

1. Jika Id tidak valid (400)

```json
{
    "status": "error",
    "message": "Invalid category ID"
}
```

2. Jika Admin tidak memiliki akses

```json
{
    "status": "error",
    "message": "Forbidden. Only admins can create categories"
}
```

3. Jika Kategori tidak ditemukan (404)

```json
{
    "status": "error",
    "message": "Category not found"
}
```

4. Jika token tidak ada atau tidak valid (401)

```json
{
    "status": "error",
    "message": "Unauthorized. Token is required"
}
```
