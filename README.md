<div align="center">

# 🚀 NexusAI — Multi-Asset Investment Intelligence Platform

**A production-ready, full-stack investment dashboard built with Next.js 14, Firebase Auth, MongoDB, Finnhub API, and OpenRouter AI.**

[![Next.js](https://img.shields.io/badge/Next.js-14-black?style=flat-square&logo=next.js)](https://nextjs.org)
[![TypeScript](https://img.shields.io/badge/TypeScript-5-blue?style=flat-square&logo=typescript)](https://typescriptlang.org)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind-3-38bdf8?style=flat-square&logo=tailwindcss)](https://tailwindcss.com)
[![Firebase](https://img.shields.io/badge/Firebase-Auth-orange?style=flat-square&logo=firebase)](https://firebase.google.com)
[![MongoDB](https://img.shields.io/badge/MongoDB-Atlas-green?style=flat-square&logo=mongodb)](https://mongodb.com)

</div>

---

## 📸 Features Overview

| Page | Features |
|------|----------|
| **Dashboard** | Live asset prices, portfolio KPIs, area charts, pie chart, holdings table |
| **Markets** | Real-time sortable table + grid view, watchlist, search, live Finnhub data |
| **Portfolio** | Add/remove positions, diversification score, radar chart, risk level |
| **AI Insights** | Real OpenRouter AI chat with conversation memory, markdown rendering |
| **Asset Detail** | Live OHLCV chart, RSI, SMA 20/50, Bollinger Bands, news feed, AI predictions |
| **Simulator** | Interest rate + crash sliders, stress-test scenarios, projected chart |
| **Alerts** | Price/risk alert toggles, notification feed, create custom alerts |
| **Account** | Profile management, password change, preferences, activity log, data export |
| **Auth** | Google OAuth + Email/Password, JWT sessions, forgot password |

---

## 🏗️ Tech Stack

| Layer | Technology |
|-------|-----------|
| **Framework** | Next.js 14 (App Router) |
| **Language** | TypeScript 5 |
| **Styling** | Tailwind CSS 3 |
| **Auth** | Firebase Authentication (free tier) |
| **Database** | MongoDB Atlas + Mongoose |
| **Session** | JWT via `jose` (httpOnly cookie) |
| **Charts** | Recharts |
| **State** | Zustand |
| **Market Data** | Finnhub API (free, 60 req/min) |
| **AI Chat** | OpenRouter (free models available) |
| **AI Analysis** | OpenRouter + structured JSON prompts |
| **Deployment** | Vercel (recommended) |

---

## 📁 Project Structure

```
nexusai/
│
├── app/                          # Next.js App Router pages
│   ├── layout.tsx                # Root layout (AuthProvider + ClientLayout)
│   ├── page.tsx                  # Root redirect → /dashboard
│   ├── globals.css               # Global styles, CSS variables, animations
│   │
│   ├── dashboard/page.tsx        # Main dashboard (live prices, charts)
│   ├── markets/page.tsx          # Market table + grid (live Finnhub)
│   ├── portfolio/page.tsx        # Portfolio manager
│   ├── ai-insights/page.tsx      # AI chat (OpenRouter)
│   ├── simulator/page.tsx        # Scenario stress tester
│   ├── alerts/page.tsx           # Alert management
│   ├── account/page.tsx          # Full account settings
│   │
│   ├── asset/[id]/page.tsx       # Asset detail: chart + news + AI analysis
│   │
│   ├── auth/
│   │   ├── layout.tsx            # Clean layout (no sidebar)
│   │   ├── signin/page.tsx       # Sign In (Google + Email)
│   │   ├── signup/page.tsx       # Sign Up (with password strength)
│   │   └── forgot-password/      # Password reset
│   │
│   └── api/                      # Backend API routes
│       ├── auth/
│       │   ├── session/route.ts  # POST: create JWT session
│       │   ├── me/route.ts       # GET: current user
│       │   └── signout/route.ts  # POST: clear cookie
│       │
│       ├── market/
│       │   ├── quotes/route.ts   # GET: live batch quotes (Finnhub)
│       │   ├── candle/route.ts   # GET: OHLCV + indicators (Finnhub)
│       │   ├── news/route.ts     # GET: asset news (Finnhub)
│       │   └── analyze/route.ts  # POST: AI analysis (OpenRouter)
│       │
│       ├── ai/
│       │   └── chat/route.ts     # POST: AI chat (OpenRouter)
│       │
│       └── user/
│           ├── profile/route.ts        # GET/PATCH: user profile
│           ├── activity/route.ts       # GET: activity log
│           ├── change-password/route.ts# POST: Firebase password update
│           ├── delete/route.ts         # DELETE: full account deletion
│           └── export/route.ts         # GET: data export JSON
│
├── components/
│   ├── ClientLayout.tsx          # App shell (sidebar-aware, auth-aware)
│   ├── Sidebar.tsx               # Collapsible nav with user profile
│   ├── Navbar.tsx                # Top bar: ticker, search, notifications
│   ├── AssetCard.tsx             # Asset card with sparkline chart
│   ├── StatCard.tsx              # KPI stat card
│   └── AuthGuard.tsx             # Loading spinner while auth resolves
│
├── contexts/
│   └── AuthContext.tsx           # Firebase auth state + JWT session manager
│
├── lib/
│   ├── firebase.ts               # Firebase Client SDK (lazy, SSR-safe)
│   ├── firebase-admin.ts         # Firebase Admin SDK (graceful fallback)
│   ├── mongodb.ts                # Mongoose connection (lazy, optional)
│   ├── session.ts                # JWT sign/verify with jose
│   ├── finnhub.ts                # Finnhub API client + indicators
│   ├── openrouter.ts             # OpenRouter AI analysis client
│   ├── mockData.ts               # Fallback mock data for all assets
│   ├── store.ts                  # Zustand stores (portfolio, alerts)
│   ├── utils.ts                  # formatCurrency, formatPercent, cn()
│   ├── activityLogger.ts         # Non-fatal activity logger
│   └── models/
│       ├── User.ts               # MongoDB User schema
│       └── Activity.ts           # MongoDB Activity log schema
│
├── middleware.ts                  # Edge JWT verification + route protection
├── tailwind.config.ts             # Custom colors, animations
├── next.config.js                 # Next.js config (remote images)
├── tsconfig.json
├── package.json
├── .env.local.example             # ← Copy this to .env.local
└── .gitignore
```

---

## ⚙️ Setup & Installation

### Prerequisites

- Node.js 18+ 
- npm or yarn
- Git

### Step 1 — Clone & Install

```bash
git clone https://github.com/your-username/nexusai.git
cd nexusai
npm install
```

### Step 2 — Environment Variables

```bash
cp .env.local.example .env.local
```

Open `.env.local` and fill in all values (see [Environment Variables](#-environment-variables) below).

### Step 3 — Run Development Server

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) — you'll be redirected to the sign-in page.

> **Tip:** The app works with only the Firebase Client SDK keys configured. MongoDB and Finnhub are optional but highly recommended.

---

## 🔑 Environment Variables

### Required (Minimum — for auth to work)

```env
# Firebase Client SDK — from Firebase Console → Project Settings → Web App
NEXT_PUBLIC_FIREBASE_API_KEY=AIzaSy...
NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN=your-project.firebaseapp.com
NEXT_PUBLIC_FIREBASE_PROJECT_ID=your-project-id
NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET=your-project.appspot.com
NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID=123456789
NEXT_PUBLIC_FIREBASE_APP_ID=1:123456789:web:abc123

# Session signing — generate with: openssl rand -base64 32
JWT_SECRET=your-random-32-char-secret-here

# App URL
NEXTAUTH_URL=http://localhost:3000
```

### Optional — Full Database Support

```env
# MongoDB Atlas — mongodb+srv://user:pass@cluster.mongodb.net/nexusai
MONGODB_URI=mongodb+srv://...
```

### Optional — Server-side Token Verification (Recommended for production)

```env
# Firebase Admin SDK — from Firebase Console → Service Accounts → Generate Key
FIREBASE_PROJECT_ID=your-project-id
FIREBASE_CLIENT_EMAIL=firebase-adminsdk-xxx@project.iam.gserviceaccount.com
FIREBASE_PRIVATE_KEY="-----BEGIN RSA PRIVATE KEY-----\nMIIE...\n-----END RSA PRIVATE KEY-----\n"
```

### Optional — Live Market Data & AI Features

```env
# Finnhub — Free at https://finnhub.io/register (60 req/min)
FINNHUB_API_KEY=your_finnhub_key

# OpenRouter — Free models at https://openrouter.ai
OPENROUTER_API_KEY=sk-or-v1-your_key
OPENROUTER_MODEL=meta-llama/llama-3.1-8b-instruct:free
```

---

## 🔥 Firebase Setup (Step-by-Step)

### 1. Create a Firebase Project

1. Go to [console.firebase.google.com](https://console.firebase.google.com)
2. Click **Add project** → enter a name → Create
3. Disable Google Analytics (optional)

### 2. Enable Authentication

1. Sidebar → **Authentication** → **Get started**
2. **Sign-in method** tab → Enable:
   - ✅ **Email/Password**
   - ✅ **Google** (set your project support email)

### 3. Get Client SDK Config

1. **Project Settings** (gear icon) → **Your apps** → **Add app** → Web (</>) 
2. Register app → copy the `firebaseConfig` object values to your `.env.local`

### 4. Get Admin SDK (Optional but recommended)

1. **Project Settings** → **Service accounts** tab
2. Click **Generate new private key** → downloads JSON file
3. Copy `project_id`, `client_email`, `private_key` to `.env.local`

> ⚠️ **Private Key format:** Keep `\n` as literal backslash-n. Wrap the entire value in double quotes.

### 5. Add Authorized Domains (for production)

1. **Authentication** → **Settings** → **Authorized domains**
2. Add your Vercel domain (e.g. `nexusai.vercel.app`)

---

## 🍃 MongoDB Atlas Setup (Step-by-Step)

1. Go to [cloud.mongodb.com](https://cloud.mongodb.com) → Create free account
2. **Build a Database** → **M0 Free** tier → choose region → Create
3. **Database Access** → Add user:
   - Username: `nexusai-user`
   - Password: generate strong password → **Save**
   - Role: `Read and write to any database`
4. **Network Access** → Add IP → `0.0.0.0/0` (allow all for development)
5. **Clusters** → **Connect** → **Drivers** → Node.js
6. Copy connection string → replace `<password>` and `<dbname>` with `nexusai`

```
mongodb+srv://nexusai-user:YOUR_PASSWORD@cluster0.xxxxx.mongodb.net/nexusai?retryWrites=true&w=majority
```

> ⚠️ URL-encode special characters in password: `@` → `%40`, `#` → `%23`

---

## 📈 Finnhub API Setup

1. Register free at [finnhub.io/register](https://finnhub.io/register)
2. Dashboard → copy your **API Key**
3. Add to `.env.local` as `FINNHUB_API_KEY`

**Free tier limits:**
- 60 API calls/minute
- Real-time US stock quotes
- Forex/commodity quotes (via OANDA symbols)
- Company news
- General market news

---

## 🤖 OpenRouter AI Setup

1. Sign up at [openrouter.ai](https://openrouter.ai)
2. **Account** → **Keys** → **Create Key**
3. Add to `.env.local` as `OPENROUTER_API_KEY`

**Recommended free models:**

| Model | Speed | Quality | Use case |
|-------|-------|---------|----------|
| `meta-llama/llama-3.1-8b-instruct:free` | Fast | Good | Chat + analysis |
| `mistralai/mistral-7b-instruct:free` | Fast | Good | Alternative |
| `google/gemma-2-9b-it:free` | Medium | Better | Detailed analysis |

Set in `.env.local`:
```env
OPENROUTER_MODEL=meta-llama/llama-3.1-8b-instruct:free
```

---

## 🔐 Authentication Flow

```
Browser                         Server                    Firebase
   │                               │                         │
   ├─ signInWithGoogle() ─────────►│                         │
   │◄── Firebase User ─────────────│◄─── Google OAuth ───────┤
   │                               │                         │
   ├─ POST /api/auth/session ──────►│                         │
   │   { idToken }                 ├─ verifyIdToken() ───────►│
   │                               │◄─ decoded payload ──────-│
   │                               ├─ MongoDB upsert          │
   │                               ├─ signSession() → JWT     │
   │◄─ Set-Cookie: __session=JWT ──-│                         │
   │                               │                         │
   ├─ GET /dashboard ─────────────►│ middleware verifyJWT     │
   │◄─ 200 OK ─────────────────────│ ✅ Valid → pass through  │
```

### Session Strategy

| Approach | Firebase session cookies | **NexusAI (this project)** |
|----------|------------------------|---------------------------|
| Method | Firebase Identity Platform | Custom JWT via `jose` |
| Cost | **Paid feature** | **Free** ✅ |
| Storage | Managed by Firebase | httpOnly cookie |
| Expiry | Up to 2 weeks | 5 days (configurable) |
| Revocation | Firebase Admin | JWT expiry + logout |

---

## 🚀 Deployment on Vercel

### 1. Push to GitHub

```bash
git init
git add .
git commit -m "Initial commit — NexusAI Platform"
git remote add origin https://github.com/your-username/nexusai.git
git push -u origin main
```

### 2. Deploy to Vercel

```bash
# Install Vercel CLI
npm i -g vercel

# Deploy
vercel

# Follow prompts:
# - Link to existing project or create new
# - Framework: Next.js (auto-detected)
# - Build command: npm run build
# - Output directory: .next
```

### 3. Set Environment Variables

In Vercel Dashboard → **Project** → **Settings** → **Environment Variables**:

Add all variables from `.env.local`. 

> ⚠️ **Important for `FIREBASE_PRIVATE_KEY` on Vercel:** Paste the key with **real newlines** (not `\n`). Vercel's UI handles multiline values correctly.

### 4. Add Vercel Domain to Firebase

Firebase Console → Authentication → Settings → Authorized domains → Add your `.vercel.app` domain.

---

## 🔧 Available Scripts

```bash
npm run dev      # Start development server (http://localhost:3000)
npm run build    # Build for production
npm run start    # Start production server
npm run lint     # Run ESLint
```

---

## 📊 App Behavior Without API Keys

The app is designed to **never crash** even if APIs aren't configured:

| Missing | Behavior |
|---------|----------|
| `FIREBASE_*` client keys | Auth pages show Firebase error on login attempt |
| `FIREBASE_PRIVATE_KEY` etc. (Admin) | Tokens decoded without signature verification (dev mode) |
| `MONGODB_URI` | Sessions work via JWT only — no profile persistence |
| `FINNHUB_API_KEY` | Dashboard shows mock data with "Demo mode" badge |
| `OPENROUTER_API_KEY` | AI Insights shows smart mock responses |

---

## 🗺️ API Reference

### Auth APIs

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/api/auth/session` | Verify Firebase ID token → set JWT cookie |
| `GET`  | `/api/auth/me` | Return current user from session |
| `POST` | `/api/auth/signout` | Clear JWT cookie |

### Market APIs

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/api/market/quotes?ids=gold,aapl` | Batch live quotes |
| `GET` | `/api/market/candle?id=gold&resolution=D` | OHLCV + indicators |
| `GET` | `/api/market/news?id=gold&limit=10` | Asset news |
| `POST` | `/api/market/analyze` | AI price prediction |

### AI APIs

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/api/ai/chat` | OpenRouter chat with full conversation history |

### User APIs

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/api/user/profile` | Get full user profile |
| `PATCH` | `/api/user/profile` | Update name / preferences |
| `GET` | `/api/user/activity` | Activity log |
| `POST` | `/api/user/change-password` | Update Firebase password |
| `DELETE` | `/api/user/delete` | Delete account + all data |
| `GET` | `/api/user/export` | Download data as JSON |

---

## 🧩 Asset ID Reference

| Internal ID | Asset | Finnhub Symbol |
|-------------|-------|----------------|
| `gold` | Gold | `OANDA:XAU_USD` |
| `silver` | Silver | `OANDA:XAG_USD` |
| `crude-oil` | WTI Crude | `OANDA:BCO_USD` |
| `copper` | Copper | `OANDA:XCU_USD` |
| `aapl` | Apple Inc. | `AAPL` |
| `msft` | Microsoft | `MSFT` |
| `nvda` | NVIDIA | `NVDA` |
| `tsla` | Tesla | `TSLA` |

---

## 🔒 Security Notes

- **JWT Secret:** Must be at least 32 random characters. Generate: `openssl rand -base64 32`
- **Firebase Private Key:** Never commit to Git. Never expose publicly.
- **MongoDB URI:** Never commit to Git. Use IP allowlist in production.
- **Cookies:** `httpOnly` + `secure` (in production) + `sameSite: lax` — protected from XSS
- **Route Protection:** Middleware runs at the Edge before any page renders
- **Token Verification:** Full cryptographic verification when Firebase Admin is configured; decode-only fallback in dev

---

## 🐛 Troubleshooting

### "Failed to create server session"
- Check `FIREBASE_PRIVATE_KEY` format — must have `\n` and be wrapped in double quotes
- The app now uses JWT (not Firebase session cookies) — no Identity Platform needed

### Login redirects back to sign-in
- Clear browser cookies and try again
- Check `JWT_SECRET` is set in `.env.local`
- Restart dev server after changing env vars

### "No candle data available"
- Add `FINNHUB_API_KEY` to `.env.local`
- Check Finnhub rate limits (60/min on free tier)
- Some commodity symbols require OANDA subscription

### MongoDB connection fails
- Check IP allowlist in MongoDB Atlas → Network Access
- Ensure password special characters are URL-encoded
- Connection string format: `mongodb+srv://user:pass@cluster.mongodb.net/nexusai`

### AI responses are mock / "add OPENROUTER_API_KEY"
- Sign up at openrouter.ai and create a key
- Set `OPENROUTER_API_KEY=sk-or-v1-...` in `.env.local`
- Restart the dev server

---

## 📦 Dependencies

```json
{
  "next":       "14.2.3",
  "react":      "^18",
  "typescript": "^5",
  "tailwindcss":"^3.4",
  "recharts":   "^2.12",
  "zustand":    "^4.5",
  "firebase":   "latest",
  "firebase-admin": "latest",
  "mongoose":   "latest",
  "jose":       "latest",
  "lucide-react": "^0.383",
  "clsx":       "^2.1",
  "swr":        "latest"
}
```

---

## 🗺️ Roadmap

- [ ] Real-time WebSocket price updates (Finnhub WebSocket)
- [ ] Portfolio profit/loss tracking with historical positions
- [ ] Email notification system (Resend / SendGrid)
- [ ] PWA support with offline mode
- [ ] Multi-currency conversion
- [ ] Advanced screener with custom filters
- [ ] Backtesting engine
- [ ] Team/shared portfolios (Enterprise plan)
- [ ] Mobile app (React Native)

---

## 📄 License

MIT License — free for personal and commercial use.

---

<div align="center">

Built with ❤️ using Next.js, Firebase, MongoDB, and OpenRouter AI

**[Live Demo](https://nexusai-trading-assitant-platform.vercel.app/)** · **[Report Bug](https://github.com/nirmaltodwal7/nexusai-trading-assitant-platform)** · **[Request Feature](https://github.com/your-username/nexusai/issues)**

</div>
