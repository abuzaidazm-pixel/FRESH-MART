# FRESH-MART Deployment Guide

## Overview
This guide covers deploying FRESH-MART to various platforms. The app is built with Next.js and uses Supabase for backend services.

---

## 📋 Prerequisites
- Node.js 18+
- npm or yarn
- Supabase account and database setup
- Git repository initialized

---

## 🚀 Deployment Options

### Option 1: Vercel (Recommended for Next.js)

**Why Vercel?** Native Next.js support, automatic deployments, serverless, fast.

#### Steps:
1. **Push to GitHub:**
   ```bash
   git push origin main
   ```

2. **Connect to Vercel:**
   - Go to [vercel.com](https://vercel.com)
   - Click "New Project"
   - Import your GitHub repository
   - Select `abuzaidazm-pixel/FRESH-MART`

3. **Configure Environment Variables:**
   - In Vercel dashboard, go to **Settings > Environment Variables**
   - Add:
     - `NEXT_PUBLIC_SUPABASE_URL`
     - `NEXT_PUBLIC_SUPABASE_ANON_KEY`
     - `SUPABASE_SERVICE_ROLE_KEY`

4. **Deploy:**
   - Click "Deploy"
   - Vercel will automatically build and deploy on every push to `main`

**Cost:** Free tier available, $20/month for pro features

---

### Option 2: Docker + Railway

**Why Railway?** Simple, affordable, good for full-stack apps.

#### Steps:
1. **Install Railway CLI:**
   ```bash
   npm i -g @railway/cli
   ```

2. **Login to Railway:**
   ```bash
   railway login
   ```

3. **Create Project:**
   ```bash
   railway init
   ```

4. **Add Environment Variables:**
   ```bash
   railway variables set NEXT_PUBLIC_SUPABASE_URL=your_url
   railway variables set NEXT_PUBLIC_SUPABASE_ANON_KEY=your_key
   railway variables set SUPABASE_SERVICE_ROLE_KEY=your_key
   ```

5. **Deploy:**
   ```bash
   railway up
   ```

**Cost:** Pay-as-you-go, typically $5-20/month

---

### Option 3: Docker + Heroku

**Why Heroku?** Popular, reliable, good documentation.

#### Steps:
1. **Install Heroku CLI:**
   ```bash
   npm install -g heroku
   ```

2. **Login & Create App:**
   ```bash
   heroku login
   heroku create fresh-mart-app
   ```

3. **Add Environment Variables:**
   ```bash
   heroku config:set NEXT_PUBLIC_SUPABASE_URL=your_url
   heroku config:set NEXT_PUBLIC_SUPABASE_ANON_KEY=your_key
   heroku config:set SUPABASE_SERVICE_ROLE_KEY=your_key
   ```

4. **Deploy:**
   ```bash
   git push heroku main
   ```

**Cost:** $50/month minimum (basic dyno)

---

### Option 4: Docker + AWS EC2

**Why AWS EC2?** Full control, scalable, pay-per-use.

#### Steps:
1. **Launch EC2 Instance:**
   - Ubuntu 22.04 LTS, t3.micro or larger
   - Security group: Allow ports 80, 443, 3000

2. **SSH into Instance:**
   ```bash
   ssh -i your-key.pem ubuntu@your-instance-ip
   ```

3. **Install Docker & Docker Compose:**
   ```bash
   sudo apt update
   sudo apt install -y docker.io docker-compose
   sudo usermod -aG docker ubuntu
   ```

4. **Clone Repository:**
   ```bash
   git clone https://github.com/abuzaidazm-pixel/FRESH-MART.git
   cd FRESH-MART
   ```

5. **Create .env.production:**
   ```bash
   nano .env.production
   ```
   Add your Supabase credentials

6. **Run with Docker Compose:**
   ```bash
   docker-compose up -d
   ```

7. **Setup Nginx Reverse Proxy (Optional):**
   ```bash
   sudo apt install -y nginx
   ```

**Cost:** $4-20/month depending on instance type

---

### Option 5: Docker + DigitalOcean App Platform

**Why DigitalOcean?** Affordable, simple, good documentation.

#### Steps:
1. **Push code to GitHub**

2. **DigitalOcean Dashboard:**
   - Click "Create" > "App"
   - Connect GitHub repository
   - Select "FRESH-MART"
   - Configure:
     - Build command: `npm ci && npm run build`
     - Run command: `npm start`
     - HTTP port: `3000`

3. **Add Environment Variables in DO Dashboard:**
   - `NEXT_PUBLIC_SUPABASE_URL`
   - `NEXT_PUBLIC_SUPABASE_ANON_KEY`
   - `SUPABASE_SERVICE_ROLE_KEY`

4. **Deploy** - DigitalOcean will auto-deploy

**Cost:** $12/month minimum

---

## 📊 Comparison Table

| Platform | Cost | Setup Time | Best For | Auto Deploy |
|----------|------|-----------|----------|:-----------:|
| **Vercel** | Free/$20 | 5 min | Next.js apps | ✅ |
| **Railway** | Pay-as-you-go | 10 min | Full-stack | ✅ |
| **Heroku** | $50+ | 10 min | Production | ✅ |
| **AWS EC2** | $4-20 | 20 min | High scale | ❌ |
| **DigitalOcean** | $12+ | 10 min | General | ✅ |

---

## ✅ Local Testing Before Deploy

```bash
# Install dependencies
npm install

# Setup environment
cp .env.example .env.local
# Edit .env.local with your values

# Run development server
npm run dev
# Visit http://localhost:3000

# Build for production
npm run build

# Test production build
npm start

# Test with Docker
docker build -t fresh-mart .
docker run -p 3000:3000 fresh-mart
```

---

## 🔒 Security Checklist

- [ ] Never commit `.env` files (use `.env.example` as template)
- [ ] Rotate Supabase keys regularly
- [ ] Use HTTPS only (all platforms provide this)
- [ ] Enable branch protection on GitHub
- [ ] Set up GitHub secrets for CI/CD
- [ ] Use environment-specific secrets
- [ ] Review Supabase RLS policies
- [ ] Setup database backups

---

## 🐛 Troubleshooting

### Build Fails
```bash
# Clear cache and rebuild
rm -rf .next node_modules
npm ci
npm run build
```

### Port Already in Use
```bash
# Change port
PORT=3001 npm start
```

### Supabase Connection Issues
- Verify credentials in environment variables
- Check Supabase project is active
- Verify network policies allow connection

### Performance Issues
- Enable ISR (Incremental Static Regeneration) in Next.js
- Add caching headers
- Optimize images with Next.js Image component
- Monitor with platform analytics

---

## 📞 Support

For issues:
1. Check GitHub Issues
2. Review Supabase documentation
3. Check deployment platform docs
4. Create detailed issue with logs

---

## 🔄 CI/CD Setup

The repository includes GitHub Actions workflows:
- `.github/workflows/test.yml` - Runs on every PR
- `.github/workflows/deploy.yml` - Auto-deploys to Vercel on main push

### Setup GitHub Secrets:

1. Go to **Settings > Secrets and variables > Actions**
2. Add secrets:
   - `VERCEL_TOKEN` - From Vercel account settings
   - `VERCEL_ORG_ID` - Your Vercel org ID
   - `VERCEL_PROJECT_ID` - Your Vercel project ID
   - `NEXT_PUBLIC_SUPABASE_URL`
   - `NEXT_PUBLIC_SUPABASE_ANON_KEY`
   - `SUPABASE_SERVICE_ROLE_KEY`

---

**Last Updated:** 2026-08-20
**Status:** Ready for deployment ✅
