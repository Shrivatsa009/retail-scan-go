# Retail Scan & Go - System Architecture

## System Overview

Retail Scan & Go is a retail self-checkout platform that enables customers to:

1. Enter a store
2. Select the store in the app
3. Scan products
4. Add products to cart
5. Make payment
6. Receive secure QR
7. Exit without standing in billing queues

The system consists of:

* Customer Mobile Application
* Admin Dashboard
* Security Guard Application
* Backend API
* PostgreSQL Database

---

# High Level Architecture

Customer App
↓
Backend API
↓
PostgreSQL

Admin Dashboard
↓
Backend API
↓
PostgreSQL

Guard App
↓
Backend API
↓
PostgreSQL

---

# Backend Modules

## Auth Module

Purpose:

Authentication and authorization.

Responsibilities:

* Login
* JWT generation
* JWT validation
* Role management

Roles:

* customer
* admin
* guard

Dependencies:

* Users Module

---

## Users Module

Purpose:

Manage users.

Responsibilities:

* Create User
* Update User
* Get User
* User Profile

Dependencies:

* Auth Module

---

## Stores Module

Purpose:

Manage retail stores.

Responsibilities:

* Create Store
* Update Store
* Delete Store
* Get Store
* List Stores

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
* Search Product
* Get Product By Barcode

Dependencies:

* Stores Module

---

## Inventory Module

Purpose:

Manage stock.

Responsibilities:

* Add Inventory
* Reduce Inventory
* Update Inventory
* Validate Inventory

Dependencies:

* Products Module

---

## Cart Module

Purpose:

Customer shopping cart.

Responsibilities:

* Add Product
* Remove Product
* Update Quantity
* View Cart
* Clear Cart

Dependencies:

* Products Module

---

## Orders Module

Purpose:

Order creation.

Responsibilities:

* Create Order
* Order History
* Order Details
* Order Status

Dependencies:

* Cart Module
* Inventory Module

---

## Payments Module

Purpose:

Process payments.

Responsibilities:

* Initiate Payment
* Verify Payment
* Update Payment Status
* Create Transaction Record

Dependencies:

* Orders Module

---

## QR Module

Purpose:

Generate secure exit QR.

Responsibilities:

* Generate Token
* Encrypt Token
* Generate QR
* Validate QR
* Mark Used

Dependencies:

* Payments Module

---

## Guards Module

Purpose:

Exit verification.

Responsibilities:

* Scan QR
* Validate QR
* Approve Exit
* Mark QR Used

Dependencies:

* QR Module

---

# Dashboard Architecture

Pages:

* Login
* Dashboard
* Products
* Inventory
* Orders
* Transactions
* Guards
* Settings

Dependencies:

Backend API

---

# Customer Mobile App Architecture

Screens:

* Splash
* Login
* OTP Verification
* Store Selection
* Home
* Product Scan
* Cart
* Checkout
* Order History
* Profile

Dependencies:

Backend API

---

# Guard Mobile App Architecture

Screens:

* Login
* Scan QR
* Verification Result
* Approve Exit

Dependencies:

Backend API

---

# Order Flow

Customer
↓
Scan Products
↓
Cart
↓
Checkout
↓
Create Order
↓
Payment
↓
Payment Verification
↓
Generate QR
↓
Exit Verification

---

# Inventory Flow

Product Created
↓
Inventory Added
↓
Customer Purchase
↓
Inventory Reduced

---

# Security Flow

Payment Success
↓
Generate Secure Token
↓
Generate QR
↓
Guard Scans QR
↓
Validate Token
↓
Validate Payment
↓
Mark Token Used
↓
Allow Exit

---

# Realtime Events

Socket.IO Events:

inventory_updated

order_created

payment_success

qr_verified

These events are used for:

* Dashboard updates
* Inventory synchronization
* Order notifications

---

# Future Expansion Rules

Future features must be added as independent modules.

Future modules must not modify:

* Auth Module
* Payments Module
* Orders Module

Future modules should communicate through services or events.

Architecture must remain modular and scalable.
