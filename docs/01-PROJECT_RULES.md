# Retail Scan & Go - Project Rules

## Project Overview

Retail Scan & Go is a self-checkout retail platform that allows customers to:

* Scan products
* Add products to cart
* Pay through UPI
* Generate secure exit QR
* Skip billing queues

The system consists of:

* Admin Dashboard
* Customer Mobile App
* Security Guard App
* Backend API
* PostgreSQL Database

---

## Technology Stack

### Dashboard

* React
* JavaScript
* Vite
* Redux Toolkit
* React Router
* Axios

### Mobile App

* React Native
* JavaScript
* Redux Toolkit
* Axios
* React Navigation

### Backend

* Node.js
* NestJS
* TypeScript
* Prisma ORM
* JWT Authentication
* Socket.IO

### Database

* PostgreSQL

---

## Architecture Rules

### Rule 1

Use Feature-Based Architecture.

Never use a large shared components structure for business modules.

Correct:

src/features/auth
src/features/products
src/features/orders

---

### Rule 2

Business logic must never be placed inside controllers.

Use:

Controller
→ Service
→ Repository
→ Database

---

### Rule 3

Every module must be isolated.

Modules:

* auth
* users
* stores
* products
* inventory
* cart
* orders
* payments
* qr
* guards

---

### Rule 4

Do not change architecture without approval.

---

## Naming Conventions

### Components

Use PascalCase.

Examples:

ProductCard.jsx

OrderHistory.jsx

CartSummary.jsx

---

### Pages

Use PascalCase with Page suffix.

Examples:

LoginPage.jsx

DashboardPage.jsx

ProductsPage.jsx

---

### Hooks

Use use prefix.

Examples:

useAuth.js

useProducts.js

useOrders.js

---

### Functions

Use camelCase.

Examples:

getProducts()

createOrder()

verifyPayment()

---

### Variables

Use camelCase.

Examples:

productList

orderDetails

cartItems

---

### Constants

Use UPPER_CASE.

Examples:

API_BASE_URL

JWT_SECRET

ORDER_STATUS

---

## API Rules

All APIs must be versioned.

Example:

/api/v1/auth/login

/api/v1/products

/api/v1/orders

---

## Frontend Rules

Never call axios directly inside components.

Incorrect:

useEffect(() => {
axios.get("/products");
}, []);

Correct:

api/productsApi.js

Then import API functions.

---

## State Management Rules

Redux Toolkit only.

Slices:

* authSlice
* productSlice
* cartSlice
* orderSlice

---

## Styling Rules

Use CSS Modules.

Examples:

ProductCard.module.css

Cart.module.css

Avoid global CSS except:

* reset
* typography
* theme

---

## Git Rules

Never commit directly to main.

Create feature branches.

Examples:

feature/auth

feature/products

feature/orders

feature/payments

feature/dashboard

feature/mobile

---

## Commit Message Rules

Examples:

feat: add authentication module

feat: add product management

fix: resolve order validation bug

refactor: improve inventory service

---

## Database Rules

All schema changes must be documented.

Update:

docs/03-DATABASE_SCHEMA.md

before applying migrations.

---

## API Rules

All new APIs must be documented.

Update:

docs/04-API_CONTRACT.md

before implementation.

---

## AI Usage Rules

Before generating any code:

Read:

docs/01-PROJECT_RULES.md
docs/02-ARCHITECTURE.md
docs/03-DATABASE_SCHEMA.md
docs/04-API_CONTRACT.md

Do not modify architecture.

Do not rename folders.

Do not introduce new patterns.

Implement only requested modules.
