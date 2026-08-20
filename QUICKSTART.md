# FRESH-MART Quick Start Guide

## 🚀 5-Minute Setup

### 1. Clone & Install
```bash
git clone https://github.com/abuzaidazm-pixel/FRESH-MART.git
cd FRESH-MART
npm install
```

### 2. Setup Environment
```bash
cp .env.example .env.local
```
Edit `.env.local` with your Supabase credentials:
- Get from https://app.supabase.com
- Project Settings > API Keys

### 3. Run Locally
```bash
npm run dev
```
Open http://localhost:3000

---

## 🌐 Deploy in 10 Minutes

### Easiest: Vercel (Free)
1. Push code to GitHub
2. Go to [vercel.com](https://vercel.com)
3. Click "New Project" → Import your repo
4. Add environment variables
5. Click "Deploy" ✅

### Alternative: Railway
1. `npm i -g @railway/cli`
2. `railway login`
3. `railway init` in your project folder
4. `railway variables set ...` (add env vars)
5. `railway up` ✅

---

## 📝 Environment Variables

Get these from [Supabase Dashboard](https://app.supabase.com):

```
NEXT_PUBLIC_SUPABASE_URL=https://xxxx.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=eyJxxxxx
SUPABASE_SERVICE_ROLE_KEY=eyJxxxxx
```

---

## 🏗️ Project Structure
```
src/
├── app/              # Next.js pages & routes
│   ├── admin/        # Admin dashboard
│   └── checkout/     # Checkout flow
├── components/       # Reusable UI components
├── context/          # React Context (State)
└── lib/              # Utilities & Supabase
```

---

## 🎯 Key Features
- ✅ Full e-commerce storefront
- ✅ Admin dashboard
- ✅ Product catalog with search
- ✅ Shopping cart & checkout
- ✅ Order tracking
- ✅ User authentication
- ✅ Real-time updates

---

## 🔗 Useful Links
- [Supabase Docs](https://supabase.com/docs)
- [Next.js Docs](https://nextjs.org/docs)
- [Tailwind CSS](https://tailwindcss.com/docs)

---

## ❓ Help
See `DEPLOYMENT.md` for detailed deployment options and troubleshooting.
