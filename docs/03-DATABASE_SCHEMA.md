# Retail Scan & Go - Database Schema

## Database

PostgreSQL

---

# users

Purpose:

Stores all users of the system.

Roles:

* customer
* admin
* guard

Fields:

id (UUID) PK

mobile_number (VARCHAR 20) NULL

email (VARCHAR 255) NULL

password_hash (TEXT) NULL

full_name (VARCHAR 255)

role (ENUM)

is_active (BOOLEAN)

created_at (TIMESTAMP)

updated_at (TIMESTAMP)

Rules:

Customer:

* mobile_number required
* password_hash optional

Admin:

* email required
* password_hash required

Guard:

* email required
* password_hash required

---

# stores

Purpose:

Retail stores using the platform.

Fields:

id (UUID) PK

name (VARCHAR 255)

store_code (VARCHAR 50) UNIQUE

address (TEXT)

city (VARCHAR 100)

state (VARCHAR 100)

country (VARCHAR 100)

phone_number (VARCHAR 20)

status (BOOLEAN)

created_at (TIMESTAMP)

updated_at (TIMESTAMP)

---

# products

Purpose:

Store products.

Fields:

id (UUID) PK

store_id (UUID) FK

barcode (VARCHAR 255) UNIQUE

name (VARCHAR 255)

description (TEXT)

price (DECIMAL 10,2)

image_url (TEXT)

status (BOOLEAN)

created_at (TIMESTAMP)

updated_at (TIMESTAMP)

Relations:

Many Products → One Store

---

# inventory

Purpose:

Current stock quantity.

Fields:

id (UUID) PK

product_id (UUID) FK

quantity (INTEGER)

created_at (TIMESTAMP)

updated_at (TIMESTAMP)

Relations:

One Product → One Inventory Record

---

# carts

Purpose:

Customer active shopping cart.

Fields:

id (UUID) PK

user_id (UUID) FK

store_id (UUID) FK

created_at (TIMESTAMP)

updated_at (TIMESTAMP)

Relations:

One User → Many Carts

---

# cart_items

Purpose:

Products inside cart.

Fields:

id (UUID) PK

cart_id (UUID) FK

product_id (UUID) FK

quantity (INTEGER)

unit_price (DECIMAL 10,2)

created_at (TIMESTAMP)

updated_at (TIMESTAMP)

Relations:

One Cart → Many Cart Items

---

# orders

Purpose:

Customer orders.

Fields:

id (UUID) PK

order_number (VARCHAR 100) UNIQUE

user_id (UUID) FK

store_id (UUID) FK

total_amount (DECIMAL 10,2)

status (ENUM)

created_at (TIMESTAMP)

updated_at (TIMESTAMP)

Order Status:

pending

paid

cancelled

completed

Relations:

One User → Many Orders

One Store → Many Orders

---

# order_items

Purpose:

Products purchased.

Fields:

id (UUID) PK

order_id (UUID) FK

product_id (UUID) FK

product_name (VARCHAR 255)

quantity (INTEGER)

unit_price (DECIMAL 10,2)

total_price (DECIMAL 10,2)

created_at (TIMESTAMP)

updated_at (TIMESTAMP)

Relations:

One Order → Many Order Items

---

# transactions

Purpose:

Payment records.

Fields:

id (UUID) PK

order_id (UUID) FK

gateway_transaction_id (VARCHAR 255)

amount (DECIMAL 10,2)

status (ENUM)

payment_method (VARCHAR 100)

created_at (TIMESTAMP)

updated_at (TIMESTAMP)

Transaction Status:

pending

success

failed

Relations:

One Order → One Transaction

---

# qr_tokens

Purpose:

Secure exit QR.

Fields:

id (UUID) PK

order_id (UUID) FK

token (TEXT)

is_used (BOOLEAN)

expires_at (TIMESTAMP)

created_at (TIMESTAMP)

updated_at (TIMESTAMP)

Relations:

One Order → One QR Token

---

# otp_verifications

Purpose:

Store login OTP requests.

Fields:

id (UUID) PK

mobile_number (VARCHAR 20)

otp_code (VARCHAR 10)

expires_at (TIMESTAMP)

is_verified (BOOLEAN)

created_at (TIMESTAMP)

updated_at (TIMESTAMP)

Rules:

OTP expires in 5 minutes.

OTP becomes verified after successful validation.

---

# store_guards

Purpose:

Assign guards to stores.

Fields:

id (UUID) PK

store_id (UUID) FK

guard_id (UUID) FK

created_at (TIMESTAMP)

updated_at (TIMESTAMP)

Relations:

Store → Many Guards

Guard → Many Stores

---

# Indexes

Create indexes on:

users.mobile_number

users.email

stores.store_code

products.barcode

orders.order_number

transactions.gateway_transaction_id

---

# Future Expansion

Future modules should create new tables.

Do NOT modify existing tables unless necessary.

Examples:

rfid_tags

recommendations

theft_alerts

analytics_events

These future modules must remain independent.

---

# Database Naming Convention

Tables:

snake_case

Examples:

order_items

cart_items

qr_tokens

Columns:

snake_case

Examples:

created_at

updated_at

mobile_number

store_id

Use UUID as primary key for all tables.
