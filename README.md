# ⚡ ElectroZone: Full-Stack MERN E-Commerce Platform

A feature-rich full-stack **MERN** (MongoDB, Express.js, React, Node.js) e-commerce application with role-based access control for **Clients**, **Administrators**, and **Delivery Partners**.

---

## 🌟 Key Features

### 🛍️ Client Portal
- **Interactive shop catalog:** Real-time product search, category filtering, and live stock tracking.
- **Wishlist & cart:** One-click **Move All to Cart**, live coupon validation (e.g. `DEMO03`), and a **"You Saved ₹XXX"** badge in the order summary.
- **Order tracking stepper:** A 5-stage progress bar (`Placed` → `Confirmed` → `Processed` → `Out for Delivery` → `Received`).
- **Printable tax invoices:** Itemized print/PDF receipt with GSTIN and discount breakdown.

### 👑 Admin Portal
- **Real-time control center:** Live user stats, revenue analytics, and low-stock alerts (stock ≤ 5).
- **Sales report export:** Download sales data as CSV (`electrozone-sales-report.csv`).
- **Quick inventory restock (+10 / +50):** Update stock in one click without opening the full edit modal.
- **Order dispatch & driver management:** Automatic or manual delivery assignment, and driver COD cash settlement.

### 🚚 Delivery Partner Portal
- **Daily quest challenge:** Progress bar for completing 5 deliveries per day to unlock an automatic **₹500 performance bonus**.
- **One-click GPS navigation:** Opens Google Maps directions from the active order card.
- **One-click WhatsApp contact:** Sends a pre-filled arrival message to the customer.
- **Weekly earnings analytics:** 7-day bar chart of payouts and COD cash tracking.

---

## 💻 Tech Stack

- **Frontend:** React (Vite), client-side routing (SPA)
- **Backend:** Node.js, Express.js, JWT authentication
- **Database:** MongoDB (MongoDB Atlas for cloud hosting)
- **Hosting:** Vercel (frontend), Render or Vercel serverless (backend)

---

## 📁 Project Structure

```text
electrozone-ecom/
├── backend/             # Express API, models, routes, seed scripts
│   ├── server.js        # Server entry point
│   ├── vercel.json      # Optional serverless config
│   └── .env.example     # Backend environment template
└── frontend/            # React (Vite) application
    ├── vercel.json      # SPA routing config
    └── .env.example     # Frontend environment template
```

---

## 🛠️ Local Development Setup

**Prerequisites:** Node.js (LTS) and a MongoDB connection string (local or Atlas).

```bash
# 1. Clone the repository
git clone https://github.com/YOUR_USERNAME/electrozone-ecom.git
cd electrozone-ecom

# 2. Backend setup
cd backend
npm install
cp .env.example .env      # Set MONGO_URI and JWT_SECRET
npm run dev

# 3. Seed the database (non-destructive)
npm run seed:admin          # Creates/verifies the admin account
npm run seed:products       # Seeds flagship ElectroZone products
npm run seed:all-products   # Seeds books, electronics, and gadgets
npm run seed:coupons        # Seeds DEMO03, WELCOME10, FLAT100
npm run seed:users          # Seeds test client and delivery accounts

# 4. Frontend setup (in a new terminal)
cd frontend
npm install
cp .env.example .env      # Points to http://localhost:5000/api
npm run dev
```

- **Frontend:** http://localhost:5173
- **Backend API:** http://localhost:5000

---

## ⚙️ Environment Variables

### Backend (`backend/.env`)

| Variable | Description |
| :--- | :--- |
| `MONGO_URI` | MongoDB connection string, e.g. `mongodb+srv://<user>:<password>@cluster.mongodb.net/ecommerce?retryWrites=true&w=majority` |
| `JWT_SECRET` | Long, random secret used to sign auth tokens |
| `PORT` | Server port (default `5000`; Render sets this automatically) |
| `CLIENT_URL` | Frontend URL allowed by CORS, with no trailing slash, e.g. `https://your-app.vercel.app` |

### Frontend (`frontend/.env`)

| Variable | Description |
| :--- | :--- |
| `VITE_API_URL` | Backend API base URL, e.g. `http://localhost:5000/api` locally or `https://your-backend.onrender.com/api` in production |

> Never commit `.env` files. Keep them in `.gitignore`.

---

## 🍃 MongoDB Atlas Setup (Cloud Database)

1. Create a free cluster on [MongoDB Atlas](https://www.mongodb.com/cloud/atlas).
2. Create a database user and a Network Access rule. Cloud hosts use changing IP addresses, so many deployments allow `0.0.0.0/0`. This opens the database to any IP, so use a strong password and restrict access where you can.
3. Copy the connection string and set it as `MONGO_URI` in your backend environment variables.
4. Seed the coupons:
   ```bash
   cd backend
   npm run seed:coupons
   ```

---

## 🖥️ Deploy the Backend

### Option A: Render (recommended for Express)
1. In the [Render Dashboard](https://dashboard.render.com/), create a **Web Service** and connect your GitHub repository.
2. Configure:
   - **Root Directory:** `backend`
   - **Build Command:** `npm install`
   - **Start Command:** `node server.js`
3. Add the backend environment variables listed above (`MONGO_URI`, `JWT_SECRET`, `CLIENT_URL`).

> Free Render instances sleep when idle, so the first request after inactivity can be slow.

### Option B: Vercel serverless
The `backend` folder includes a `vercel.json` and a serverless export in `server.js`. Deploy the `backend` folder as its own Vercel project and add the same environment variables.

---

## ⚡ Deploy the Frontend to Vercel

1. In the [Vercel Dashboard](https://vercel.com/dashboard), click **Add New Project** and import your GitHub repository.
2. Configure:
   - **Framework Preset:** `Vite`
   - **Root Directory:** `frontend`
   - **Build Command:** `npm run build`
   - **Output Directory:** `dist`
3. Add the environment variable `VITE_API_URL` (your deployed backend URL ending in `/api`).
4. Click **Deploy**. Client-side routing is handled by `vercel.json`.

Deploy the backend first, then set `CLIENT_URL` on the backend to your final Vercel URL so CORS allows the frontend.

---

## 🔑 Demo Credentials

These accounts are created by the seed scripts for **local testing and demos only**. Change or remove them before using the app with real users.

| Role | Email | Password | Access |
| :--- | :--- | :--- | :--- |
| **Administrator** | `admin@myapp.com` | `Admin@12345` | Control center, inventory restock, revenue analytics, sales CSV export |
| **Customer** | `client.test@electrozone.com` | `Client@12345` | Storefront, cart, wishlist, order placement, live order tracking |
| **Delivery Driver** | `driver.test@electrozone.com` | `Driver@12345` | Dispatch dashboard, OTP verification, GPS navigation, wallet and payouts |

### 🎟️ Demo Coupons

- `DEMO03`: **20% off** (up to ₹500)
- `WELCOME10`: **10% off** (up to ₹200)
- `FLAT100`: **Flat ₹100 off** on orders above ₹499

---

## ⚠️ Disclaimer

ElectroZone is a demonstration project. Invoices, GSTIN details, and payouts shown in the app are sample data and are not legally valid documents or real financial transactions.

---

## 👥 Credits

Built by **Reddy Website Builders**.   
