<div align="center">

```
███████╗██╗███╗   ██╗███████╗██╗      ██████╗ ██╗    ██╗
██╔════╝██║████╗  ██║██╔════╝██║     ██╔═══██╗██║    ██║
█████╗  ██║██╔██╗ ██║█████╗  ██║     ██║   ██║██║ █╗ ██║
██╔══╝  ██║██║╚██╗██║██╔══╝  ██║     ██║   ██║██║███╗██║
██║     ██║██║ ╚████║██║     ███████╗╚██████╔╝╚███╔███╔╝
╚═╝     ╚═╝╚═╝  ╚═══╝╚═╝     ╚══════╝ ╚═════╝  ╚══╝╚══╝
```

**Personal Finance Ecosystem — Built with the MERN Stack**

Track every rupee. Manage every asset. Project your future wealth.

![Node](https://img.shields.io/badge/Node.js-18+-339933?style=flat-square&logo=node.js&logoColor=white)
![React](https://img.shields.io/badge/React-18-61DAFB?style=flat-square&logo=react&logoColor=black)
![MongoDB](https://img.shields.io/badge/MongoDB-Atlas-47A248?style=flat-square&logo=mongodb&logoColor=white)
![Express](https://img.shields.io/badge/Express-4-000000?style=flat-square&logo=express&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-D4A843?style=flat-square)
![Status](https://img.shields.io/badge/Status-Active%20Development-22C55E?style=flat-square)

</div>

---

## 🚧 Currently Working On This

> This project is under active development. Below is the live status of every module.

| Module | Status | Notes |
|--------|--------|-------|
| 💰 Dashboard Overview | ✅ Complete | Live API, real charts |
| 📋 Expense Tracker | ✅ Complete | CRUD, Need/Want filter |
| 📈 Stock Portfolio | ✅ Complete | CMP inline edit, P&L |
| 🔵 Mutual Funds | ✅ Complete | Units, NAV, returns |
| 🏛️ Fixed Deposits | ✅ Complete | Maturity calc, progress bar |
| 🏦 Liquid Cash | ✅ Complete | Balance update via API |
| 📊 Wealth Projection | ✅ Complete | SIP formula, debounced sliders |
| 🔐 Authentication | 🔄 In Progress | JWT login/signup — replacing `demo_user` hardcode |
| 👤 User Profiles | 🔄 In Progress | Per-user data isolation |
| 📬 Monthly Budget Alerts | 🔜 Planned | Email alert when spend exceeds budget |
| 🔄 Live Stock Price Sync | ✅ Complete | Cron job to auto-fetch CMP from NSE API |
| 📱 Mobile Responsive UI | 🔜 Planned | Sidebar collapses, touch-friendly forms |
| 📤 Export to CSV / PDF | 🔜 Planned | Download expense reports and portfolio snapshot |
| 🌙 Light Mode Toggle | 🔜 Planned | Currently dark-only |

---

## ✨ Features

### 📋 Expense Tracker
- Add daily expenses with date, category, amount, and description
- Classify every entry as a **Need** or a **Want**
- Delete entries with instant UI update
- Visual bar chart breaking down spend by category
- Filter transaction list by type (All / Need / Want)
- Real-time totals for Needs, Wants, and entry count

### 📊 Dashboard
- Full portfolio wealth snapshot pulled from a single `/api/summary` call
- Monthly expense area chart built from MongoDB aggregation
- Asset allocation donut chart (Liquid / Stocks / MF / FDs)
- **Needs vs Wants** progress bars with percentage breakdown
- **50-30-20 Rule** health indicator (Needs / Wants / Savings ratios)
- All metrics are live — no hardcoded sample data

### 📈 Stock Portfolio
- Add holdings with ticker, quantity, average buy price, and sector
- Inline CMP (Current Market Price) editor — click any price to update it
- Automated P&L calculation per stock: `(CMP − Avg Price) × Qty`
- P&L percentage per holding
- Total invested vs current value vs overall return
- Color-coded green/red for profit/loss

### 🔵 Mutual Funds
- Track funds by name, type (Equity / Debt / Hybrid / Index / ELSS), and units
- Stores NAV at buy date vs current NAV
- Auto-calculates current value as `Units × Current NAV`
- Return % displayed per fund
- Aggregated P&L across all funds

### 🏛️ Fixed Deposits
- Add FDs with bank, principal, interest rate, tenure, and start date
- **Compound interest maturity calculator**: `P × (1 + r)^n`
- Visual progress bar showing how far into the tenure you are
- Maturity date auto-calculated from start date + tenure
- Interest earned breakdown per FD

### 💵 Liquid Cash
- Single balance field synced to MongoDB
- Update with one click — persists across sessions
- Included in total wealth calculation and asset allocation chart

### 🚀 Wealth Projection (SIP Calculator)
- Three interactive sliders: Monthly SIP amount, Expected return %, Time horizon
- **SIP compound growth formula**: `M × [(1 + r)^n − 1] / r`
- API-driven — calculations run server-side at `/api/summary/projection`
- Sliders are debounced (400ms) to avoid hammering the API
- Area chart showing corpus growth vs amount invested over time
- Milestone cards at 5, 10, 15, 20 year marks
- Wealth multiplier shown (e.g. `6.7×`)

---

## 🗂️ Project Structure

```
finance-ecosystem/
│
├── backend/
│   ├── models/
│   │   └── index.js              # All 5 Mongoose schemas with virtual fields
│   ├── routes/
│   │   ├── expenses.js           # CRUD + /analytics aggregation
│   │   ├── stocks.js             # Holdings + /pl + /cmp PATCH
│   │   ├── portfolio.js          # mfRouter + fdRouter + liquidRouter
│   │   └── summary.js            # Full snapshot + /projection
│   ├── server.js                 # Express entry, MongoDB connect, route mount
│   ├── package.json
│   └── .env                      # MONGO_URI, PORT, CLIENT_URL
│
└── frontend/
    ├── src/
    │   ├── api.js                # All axios calls — single source of truth
    │   ├── shared.jsx            # C palette, fmt(), MetricCard, Spinner, ErrorBox
    │   ├── App.jsx               # Shell — sidebar, topbar, page routing
    │   ├── main.jsx              # React root
    │   └── pages/
    │       ├── Dashboard.jsx     # /api/summary + /api/expenses/analytics
    │       ├── ExpenseTracker.jsx# Full CRUD on /api/expenses
    │       ├── Portfolio.jsx     # Stocks / MF / FD / Liquid tabs
    │       └── WealthProjection.jsx # /api/summary/projection + sliders
    ├── index.html
    ├── vite.config.js            # Proxy /api → localhost:5000
    └── package.json
```

---

## 🔌 API Reference

### Expenses — `/api/expenses`
| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/api/expenses` | List all (filters: `type`, `category`, `from`, `to`, `page`, `limit`) |
| `POST` | `/api/expenses` | Create a new expense |
| `PUT` | `/api/expenses/:id` | Update an expense |
| `DELETE` | `/api/expenses/:id` | Delete an expense |
| `GET` | `/api/expenses/analytics` | Monthly Need vs Want aggregation |

### Stocks — `/api/stocks`
| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/api/stocks` | All holdings |
| `POST` | `/api/stocks` | Add a holding |
| `PUT` | `/api/stocks/:id` | Edit a holding |
| `PATCH` | `/api/stocks/:id/cmp` | Update current market price only |
| `DELETE` | `/api/stocks/:id` | Remove a holding |
| `GET` | `/api/stocks/pl` | P&L summary across all holdings |

### Mutual Funds — `/api/mutualfunds`
| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/api/mutualfunds` | All funds |
| `POST` | `/api/mutualfunds` | Add a fund |
| `PUT` | `/api/mutualfunds/:id` | Update a fund |
| `DELETE` | `/api/mutualfunds/:id` | Remove a fund |
| `GET` | `/api/mutualfunds/pl` | Returns summary across all funds |

### Fixed Deposits — `/api/fds`
| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/api/fds` | All FDs with virtual maturity values |
| `POST` | `/api/fds` | Create a new FD |
| `PUT` | `/api/fds/:id` | Update a FD |
| `DELETE` | `/api/fds/:id` | Delete a FD |

### Liquid Cash — `/api/liquid`
| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/api/liquid` | Get current balance |
| `PUT` | `/api/liquid` | Update balance `{ balance: Number }` |

### Summary — `/api/summary`
| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/api/summary` | Full portfolio snapshot — all asset classes + expense stats |
| `GET` | `/api/summary/projection` | SIP wealth projection `?monthly=&rate=&years=` |

---

## 🧮 Core Calculations

### Fixed Deposit Maturity
```
Maturity = Principal × (1 + Rate/100) ^ (Tenure / 12)
Interest = Maturity − Principal
```

### SIP Corpus (Compound Monthly Growth)
```
Corpus = Monthly × [(1 + r)^n − 1] / r
  where  r = Annual Rate / 100 / 12
         n = Years × 12
```

### Stock P&L
```
Current Value = Qty × CMP
P&L Amount   = (CMP − Avg Price) × Qty
P&L %        = (P&L Amount / Invested Value) × 100
```

### 50-30-20 Budget Rule
```
Needs   → target ≤ 50% of monthly income
Wants   → target ≤ 30% of monthly income
Savings → target ≥ 20% of monthly income
```

---

## 🗄️ Data Models

### Expense
```json
{
  "userId":   "demo_user",
  "date":     "2025-03-01",
  "category": "Rent",
  "label":    "House Rent",
  "amount":   15000,
  "type":     "need",
  "notes":    ""
}
```

### Stock
```json
{
  "userId":   "demo_user",
  "ticker":   "RELIANCE",
  "qty":      10,
  "avgPrice": 2450,
  "cmp":      2780,
  "sector":   "Energy",
  "exchange": "NSE"
}
```

### Mutual Fund
```json
{
  "userId":     "demo_user",
  "name":       "Axis Bluechip",
  "type":       "Equity",
  "invested":   50000,
  "units":      1234.56,
  "navAtBuy":   40.50,
  "currentNav": 51.40,
  "sipAmount":  5000
}
```

### Fixed Deposit
```json
{
  "userId":    "demo_user",
  "bank":      "SBI",
  "principal": 100000,
  "rate":      7.5,
  "tenure":    12,
  "startDate": "2024-06-01"
}
```

### Liquid
```json
{
  "userId":      "demo_user",
  "balance":     125000,
  "lastUpdated": "2026-03-24T10:00:00.000Z"
}
```

---

## 🚀 Quick Start

### Prerequisites
- Node.js 18+
- npm 9+
- MongoDB Atlas account (free tier works)

### 1 — Install dependencies

```bash
# Backend
cd backend && npm install

# Frontend
cd ../frontend && npm install
```

### 2 — Configure environment

Create `backend/.env`:
```env
MONGO_URI=mongodb+srv://<user>:<password>@cluster.mongodb.net/finflow
PORT=5000
CLIENT_URL=http://localhost:5173
NODE_ENV=development
```

> In MongoDB Atlas → Network Access → add `0.0.0.0/0` for development.

### 3 — Run both servers

```bash
# Terminal 1
cd backend && npm run dev      # ✅ FinFlow API running on port 5000

# Terminal 2
cd frontend && npm run dev     # → http://localhost:5173
```

### 4 — Verify

| Check | URL |
|-------|-----|
| Frontend loads | `http://localhost:5173` |
| API health | `http://localhost:5000/health` |
| Full snapshot | `http://localhost:5000/api/summary` |
| Projection test | `http://localhost:5000/api/summary/projection?monthly=20000&rate=12&years=20` |

---

## 🛠️ Tech Stack

| Layer | Technology | Version |
|-------|-----------|---------|
| Frontend framework | React | 18 |
| Build tool | Vite | 5 |
| Charts | Recharts | 2 |
| HTTP client | Axios | 1.7 |
| Backend framework | Express | 4 |
| Runtime | Node.js | 18+ |
| Database | MongoDB Atlas | — |
| ODM | Mongoose | 8 |
| Dev server | Nodemon | 3 |

---

## 📦 Environment Variables

| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `MONGO_URI` | ✅ Yes | — | MongoDB Atlas connection string |
| `PORT` | No | `5000` | Backend server port |
| `CLIENT_URL` | No | `http://localhost:5173` | Frontend origin for CORS |
| `NODE_ENV` | No | `development` | `development` or `production` |

---

## 🤝 Contributing

1. Fork the repo
2. Create a feature branch: `git checkout -b feat/your-feature`
3. Commit your changes: `git commit -m "feat: add your feature"`
4. Push: `git push origin feat/your-feature`
5. Open a Pull Request

---

## 📄 License

MIT © 2026 FinFlow — Personal Finance Ecosystem

---

<div align="center">
  Built with ☕ and compound interest.
</div>
