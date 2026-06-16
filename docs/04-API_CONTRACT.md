# Retail Scan & Go - API Contract

Base URL

/api/v1

---

# AUTH MODULE

## Send OTP

POST /auth/send-otp

Request

{
"mobileNumber": "9876543210"
}

Response

{
"success": true,
"message": "OTP sent successfully"
}

---

## Verify OTP

POST /auth/verify-otp

Request

{
"mobileNumber": "9876543210",
"otp": "123456"
}

Response

{
"success": true,
"accessToken": "jwt_token",
"user": {}
}

---

## Admin Login

POST /auth/admin/login

Request

{
"email": "[admin@example.com](mailto:admin@example.com)",
"password": "password"
}

Response

{
"success": true,
"accessToken": "jwt_token"
}

---

## Guard Login

POST /auth/guard/login

Request

{
"email": "[guard@example.com](mailto:guard@example.com)",
"password": "password"
}

Response

{
"success": true,
"accessToken": "jwt_token"
}

---

# STORE MODULE

## Get Stores

GET /stores

Response

{
"success": true,
"data": []
}

---

## Create Store

POST /stores

Response

{
"success": true,
"data": {}
}

---

## Update Store

PUT /stores/:id

---

## Delete Store

DELETE /stores/:id

---

# PRODUCT MODULE

## Get Products

GET /products

Query Params

page

limit

search

storeId

---

## Get Product

GET /products/:id

---

## Scan Product

GET /products/barcode/:barcode

Response

{
"success": true,
"data": {}
}

---

## Create Product

POST /products

---

## Update Product

PUT /products/:id

---

## Delete Product

DELETE /products/:id

---

# INVENTORY MODULE

## Get Inventory

GET /inventory

---

## Update Inventory

PUT /inventory/:productId

---

# CART MODULE

## Get Cart

GET /cart

---

## Add To Cart

POST /cart/items

Request

{
"productId": "uuid",
"quantity": 1
}

---

## Update Cart Item

PUT /cart/items/:id

---

## Remove Cart Item

DELETE /cart/items/:id

---

## Clear Cart

DELETE /cart

---

# ORDER MODULE

## Create Order

POST /orders

Response

{
"success": true,
"orderId": "uuid"
}

---

## Get Order

GET /orders/:id

---

## Order History

GET /orders/history

---

# PAYMENT MODULE

## Create Payment

POST /payments/initiate

Request

{
"orderId": "uuid"
}

---

## Verify Payment

POST /payments/verify

Request

{
"orderId": "uuid",
"transactionId": "txn123"
}

---

# QR MODULE

## Generate QR

POST /qr/generate

Request

{
"orderId": "uuid"
}

---

## Validate QR

POST /qr/validate

Request

{
"token": "encrypted_token"
}

---

# GUARD MODULE

## Verify Exit

POST /guards/verify-exit

Request

{
"token": "encrypted_token"
}

Response

{
"success": true,
"order": {},
"paymentStatus": "paid"
}

---

# STANDARD RESPONSE FORMAT

Success

{
"success": true,
"message": "Success",
"data": {}
}

Error

{
"success": false,
"message": "Something went wrong"
}

---

# AUTHORIZATION

Protected APIs require:

Authorization: Bearer <token>

---

# API VERSIONING

All APIs must start with:

/api/v1

Future versions:

/api/v2

/api/v3

Never break existing versions.

---

# Pagination Format

{
"success": true,
"data": [],
"meta": {
"page": 1,
"limit": 10,
"total": 100
}
}
