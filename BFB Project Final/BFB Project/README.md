# Agrimarket — Supply Chain Technology Web Application

This repository is a small multi-page static web application prototype demonstrating a farm-to-market supply chain flow. It uses client-side JavaScript and localStorage to simulate a backend for demo purposes.

Contents
- `index.html`, `marketplace.html`, `farmer-upload.html`, `orders.html`, `logistics.html`, `analytics.html`, `login.html`, `register.html` — main pages.
- `app.js`, `assets/app.js` — core client-side domain logic (DB wrapper, orders, logistics, pricing helpers).
- `assets/auth.js` — authentication helpers (localStorage-based demo users).
- `assets/styles.css` — styling.

# Agrimarket — Supply Chain Technology Web Application

This repository is a small multi-page static web application prototype demonstrating a farm-to-market supply chain flow. It uses client-side JavaScript and localStorage to simulate a backend for demo purposes.

Contents
- `index.html`, `marketplace.html`, `farmer-upload.html`, `orders.html`, `logistics.html`, `analytics.html`, `login.html`, `register.html` — main pages.
- `app.js`, `assets/app.js` — core client-side domain logic (DB wrapper, orders, logistics, pricing helpers).
- `assets/auth.js` — authentication helpers (localStorage-based demo users).
- `assets/styles.css` — styling.

How to run
1. From the project folder, run a static server (Python recommended):

```powershell
python -m http.server 8000
```

2. Open `http://localhost:8000/index.html` in your browser.

Seed users (demo)
- farmer@example.com / pass123
- buyer@example.com / pass123
- dist@example.com / pass123

What this delivers (rubric mapping)
- Frontend: semantic HTML, Bootstrap layout, consistent navigation across pages.
- Database: simulated localStorage schema and a SQL schema file provided for demonstration.
- Documentation: this README, schema, ERD, and migration sample are included in `database/`.

Notes and limitations
- This is a client-side demo; for production, replace localStorage with a real server and DB.

## ERD (Entity Relationship Diagram)

The application uses the following entities (textual ERD):

- users (id PK)
	- id
	- name
	- email
	- password
	- role

- stock (id PK)
	- id
	- farmer_id (FK -> users.id)
	- crop
	- variety
	- qty_kg
	- location
	- harvest_date
	- price_per_kg
	- status

- orders (id PK)
	- id
	- stock_id (FK -> stock.id)
	- buyer_id (FK -> users.id)
	- qty_kg
	- price_per_kg
	- total
	- status
	- capacity_ok
	- logistics_id

- logistics (id PK)
	- id
	- order_id (FK -> orders.id)
	- mode
	- cost
	- carrier
	- status

Relationships:
- users 1---* stock (one farmer can list many stock items)
- stock 1---* orders (one stock listing can generate many orders)
- users 1---* orders (one buyer can place many orders)
- orders 1---1 logistics (each order may have associated logistics record)
