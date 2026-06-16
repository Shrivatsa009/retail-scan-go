# Retail Scan & Go - System Architecture

## System Overview

Retail Scan & Go is a retail self-checkout platform.

The platform consists of:

1. Customer Mobile App
2. Admin Dashboard
3. Guard App
4. Backend API
5. PostgreSQL Database

---

# Core Modules

## Auth Module

Purpose:

Authentication and Authorization.

Responsibilities:

* Login
* JWT Generation
* JWT Validation
* Role Validation

Roles:

* customer
* admin
* guard

Dependencies:

* users

---

## Users Module

Purpose:

Manage system users.

Responsibilities:

* Create User
* Update User
* View User
* User Profile

Dependencies:

None

---

## Stores Module

Purpose:

Manage retail stores.

Responsibilities:

* Create Store
* Update Store
* Delete Store
* View Store

Dependencies:

None

---

## Products Module

Purpose:

Manage products.

Responsibilities:

* Create Product
* Update Product
* Delete Product
* Product Search
* Barcode Lookup

Dependencies:

* stores

---

## Inventory Module

Purpose:

Manage stock.

Responsibilities:

* Add Stock
* Update Stock
* Reduce Stock
* Stock Validation

Dependencies:

* products

---

## Cart Module

Purpose:

Manage customer shopping carts.

Responsibilities:

* Add To Cart
* Remove From Cart
* Update Quantity
* Clear Cart

Dependencies:

* products

---

## Orders Module

Purpose:

Manage purchases.

Responsibilities:

* Create Order
* View Order
* Order History

Dependencies:

* cart
* products
* inventory

---

## Payments Module

Purpose:

Manage payment processing.

Responsibilities:

* Create Transaction
* Verify Payment
* Update Payment Status

Dependencies:

* orders

---

## QR Module

Purpose:

Generate secure exit QR.

Responsibilities:

* Generate QR
* Validate QR
* Mark QR As Used

Dependencies:

* orders
* payments

---

## Guards Module

Purpose:

Verify customer exit.

Responsibilities:

* Scan QR
* Validate Exit
* Approve Exit

Dependencies:

* qr

---

## Dashboard Module

Purpose:

Provide store management interface.

Responsibilities:

* Product Management
* Inventory Management
* Order Management
* Analytics

Dependencies:

All Business Modules

---

# System Flow

Customer

→ Select Store

→ Scan Product

→ Add To Cart

→ Checkout

→ Payment

→ QR Generated

→ Guard Verification

→ Exit

---

# Backend Architecture

Controller

↓

Service

↓

Repository

↓

Database

---

# Mobile App Architecture

Screens

↓

Redux

↓

API Layer

↓

Backend

---

# Dashboard Architecture

Pages

↓

Redux

↓

API Layer

↓

Backend

---

# Future Extensions

Reserved Modules:

* RFID
* Analytics
* AI Recommendations
* Loyalty Program
* Anti Theft

These modules must remain isolated from existing modules.
