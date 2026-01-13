# Installation & Setup Guide

Complete step-by-step guide to set up MAIO for development and production.

---

## 📋 Table of Contents

- [System Requirements](#system-requirements)
- [Backend Setup](#backend-setup)
- [Frontend Setup](#frontend-setup)
- [Admin Dashboard Setup](#admin-dashboard-setup)
- [Database Configuration](#database-configuration)
- [Environment Variables](#environment-variables)
- [Running All Services](#running-all-services)
- [Troubleshooting](#troubleshooting)
- [Production Deployment](#production-deployment)

---

## 💻 System Requirements

### Minimum Requirements

- **Operating System**: Windows, macOS, or Linux
- **Node.js**: v18.0.0 or higher
- **npm**: v9.0.0 or higher
- **MongoDB**: v9.0 or higher
- **Git**: v2.0 or higher

### Recommended Requirements

- **Node.js**: v20+ (LTS)
- **RAM**: 4GB minimum (8GB recommended)
- **Storage**: 2GB free space
- **Internet**: 10 Mbps+ connection

### Verify Installations

```bash
# Check Node.js version
node --version
# Should output v18.0.0 or higher

# Check npm version
npm --version
# Should output 9.0.0 or higher

# Check Git version
git --version
# Should output 2.0.0 or higher
```

---

## 🔧 Backend Setup

### Step 1: Navigate to Backend Directory

```bash
cd MAIO-Backend
```

### Step 2: Install Dependencies

```bash
npm install
```

This will install all required packages:

- express (web framework)
- mongoose (MongoDB ORM)
- socket.io (real-time communication)
- stripe (payment processing)
- nodemailer (email service)
- And 7+ other dependencies

### Step 3: Create Environment File

```bash
# Copy the example environment file
cp .env.example .env
```

### Step 4: Configure Environment Variables

Edit `.env` file with your configuration:

```env
# ==================
# Server Configuration
# ==================
PORT=5000
NODE_ENV=development

# ==================
# Database Configuration
# ==================
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/maio
# Or for local MongoDB:
# MONGODB_URI=mongodb://localhost:27017/maio

# ==================
# Authentication
# ==================
JWT_SECRET=your_super_secret_jwt_key_change_this
JWT_EXPIRE=7d
JWT_REFRESH_SECRET=your_refresh_token_secret_change_this
JWT_REFRESH_EXPIRE=30d

# ==================
# Email Configuration (Gmail)
# ==================
EMAIL_SERVICE=gmail
EMAIL_USER=your-email@gmail.com
EMAIL_PASSWORD=your-app-specific-password
# Note: Use Google App Passwords, not your Gmail password

# Or use alternative email service:
# EMAIL_SERVICE=sendgrid
# SENDGRID_API_KEY=your_sendgrid_api_key

# ==================
# Stripe Configuration
# ==================
STRIPE_PUBLIC_KEY=pk_test_xxxxxxxxxxxxx
STRIPE_SECRET_KEY=sk_test_xxxxxxxxxxxxx
STRIPE_WEBHOOK_SECRET=whsec_xxxxxxxxxxxxx

# ==================
# File Upload Configuration
# ==================
MAX_FILE_SIZE=5242880  # 5MB in bytes
UPLOAD_DIR=./uploads
ALLOWED_FILE_TYPES=pdf,doc,docx,jpg,jpeg,png,txt

# ==================
# CORS Configuration
# ==================
CORS_ORIGIN=http://localhost:3173,http://localhost:3000,https://yourdomain.com
CORS_CREDENTIALS=true

# ==================
# API Configuration
# ==================
API_VERSION=v1
API_TIMEOUT=30000  # 30 seconds

# ==================
# Socket.io Configuration
# ==================
SOCKET_PING_TIMEOUT=60000
SOCKET_PING_INTERVAL=25000

# ==================
# Logging (Optional)
# ==================
LOG_LEVEL=debug
LOG_FILE=logs/app.log

# ==================
# Additional Services
# ==================
REDIS_URL=redis://localhost:6379  # Optional, for caching
RATE_LIMIT_WINDOW_MS=900000  # 15 minutes
RATE_LIMIT_MAX_REQUESTS=100
```

### Step 5: Verify MongoDB Connection

**Option A: Local MongoDB**

```bash
# Ensure MongoDB is running
# Windows: mongod
# macOS: brew services start mongodb-community
# Linux: sudo systemctl start mongod

# Test connection
mongo
# Press Ctrl+C to exit
```

**Option B: MongoDB Atlas (Cloud)**

1. Create account at [mongodb.com](https://www.mongodb.com)
2. Create a cluster
3. Get connection string
4. Add to `.env` as `MONGODB_URI`

### Step 6: Create Upload Directory

```bash
mkdir -p uploads
```

### Step 7: Start Backend Server

```bash
npm start
```

You should see:

```
Server running on port 5000
MongoDB connected successfully
```

### Backend is Ready!

Access API at: `http://localhost:5000/api`

---

## 🎨 Frontend Setup

### Step 1: Navigate to Frontend Directory

```bash
cd MAIO-front
```

### Step 2: Install Dependencies

```bash
npm install
```

Dependencies include:

- react & react-dom (UI library)
- react-router-dom (routing)
- axios (HTTP client)
- socket.io-client (real-time communication)
- stripe.js (payment)
- tailwindcss (styling)
- And 15+ other dependencies

### Step 3: Create Environment File

```bash
cp .env.example .env.local
```

### Step 4: Configure Environment Variables

Edit `.env.local`:

```env
# ==================
# API Configuration
# ==================
VITE_API_BASE_URL=http://localhost:5000/api
VITE_SOCKET_URL=http://localhost:5000
VITE_API_TIMEOUT=10000  # 10 seconds

# ==================
# Stripe Configuration
# ==================
# Get keys from https://dashboard.stripe.com/apikeys
VITE_STRIPE_PUBLIC_KEY=pk_test_xxxxxxxxxxxxx

# ==================
# App Configuration
# ==================
VITE_APP_NAME=MAIO
VITE_APP_VERSION=1.0.0
VITE_APP_ENV=development

# ==================
# Feature Flags
# ==================
VITE_ENABLE_CHAT=true
VITE_ENABLE_PAYMENTS=true
VITE_ENABLE_VIDEO_CALL=false
VITE_ENABLE_ANALYTICS=true

# ==================
# Theme Configuration
# ==================
VITE_THEME_PRIMARY_COLOR=#3B82F6
VITE_THEME_SECONDARY_COLOR=#10B981

# ==================
# Logging
# ==================
VITE_LOG_LEVEL=debug
VITE_DEBUG_MODE=true
```

### Step 5: Start Development Server

```bash
npm run dev
```

You should see:

```
Local:   http://localhost:5173/
```

### Step 6: Verify Installation

1. Open browser to `http://localhost:5173`
2. You should see the MAIO landing page
3. Try to login (it will connect to backend)

### Frontend is Ready!

Access frontend at: `http://localhost:5173`

---

## 🎛️ Admin Dashboard Setup

### Step 1: Navigate to Admin Directory

```bash
cd maiodashboard
```

### Step 2: Install Dependencies

```bash
npm install
```

### Step 3: Create Environment File

```bash
cp .env.example .env.local
```

### Step 4: Configure Environment Variables

Edit `.env.local`:

```env
# ==================
# API Configuration
# ==================
NEXT_PUBLIC_API_BASE_URL=http://localhost:5000/api
NEXT_PUBLIC_API_TIMEOUT=10000

# ==================
# App Configuration
# ==================
NEXT_PUBLIC_APP_NAME=MAIO Admin
NEXT_PUBLIC_APP_VERSION=1.0.0
NEXT_PUBLIC_ENV=development

# ==================
# Feature Flags
# ==================
NEXT_PUBLIC_ENABLE_ANALYTICS=true
NEXT_PUBLIC_ENABLE_EXPORT=true
NEXT_PUBLIC_ENABLE_2FA=false

# ==================
# Security
# ==================
NEXT_PUBLIC_SESSION_TIMEOUT=3600000  # 1 hour
NEXT_PUBLIC_MAX_LOGIN_ATTEMPTS=5
NEXT_PUBLIC_LOCKOUT_DURATION=900000  # 15 minutes
```

### Step 5: Build Next.js Configuration

```bash
npm run build
```

### Step 6: Start Development Server

```bash
npm run dev
```

You should see:

```
> Local:        http://localhost:3000
```

### Step 7: Access Admin Dashboard

1. Open browser to `http://localhost:3000`
2. You should see admin login page
3. Use admin credentials to login

### Admin Dashboard is Ready!

Access admin at: `http://localhost:3000`

---

## 🗄️ Database Configuration

### MongoDB Setup

#### Local MongoDB (Windows)

1. **Download MongoDB Community**

   - Go to [mongodb.com/try/download](https://www.mongodb.com/try/download/community)
   - Download Windows installer

2. **Install MongoDB**

   - Run installer
   - Choose "Install MongoDB as a Service"
   - Finish installation

3. **Start MongoDB**

   ```bash
   net start MongoDB
   ```

4. **Connect via Mongo Shell**
   ```bash
   mongosh
   # Connected! Type help for commands
   ```

#### Local MongoDB (macOS)

```bash
# Install via Homebrew
brew tap mongodb/brew
brew install mongodb-community

# Start MongoDB
brew services start mongodb-community

# Connect
mongosh
```

#### MongoDB Atlas (Cloud)

1. **Create Account**

   - Visit [mongodb.com/cloud/atlas](https://www.mongodb.com/cloud/atlas)
   - Sign up for free account

2. **Create Cluster**

   - Click "Build a Cluster"
   - Choose free tier
   - Select region (closest to your users)
   - Click "Create Cluster"

3. **Get Connection String**

   - Go to "Database" section
   - Click "Connect"
   - Choose "Drivers"
   - Copy connection string

4. **Add to .env**
   ```env
   MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/maio
   ```

### Database Initialization

The backend automatically creates collections on first run. No manual setup needed.

---

## 🌍 Environment Variables Summary

### Backend (.env)

| Variable          | Example                        | Description           |
| ----------------- | ------------------------------ | --------------------- |
| PORT              | 5000                           | Server port           |
| MONGODB_URI       | mongodb://localhost:27017/maio | Database URL          |
| JWT_SECRET        | secret_key_here                | JWT signing secret    |
| EMAIL_USER        | your@email.com                 | Email service account |
| STRIPE_SECRET_KEY | sk_test_xxx                    | Stripe secret key     |

### Frontend (.env.local)

| Variable               | Example                   | Description       |
| ---------------------- | ------------------------- | ----------------- |
| VITE_API_BASE_URL      | http://localhost:5000/api | Backend API URL   |
| VITE_SOCKET_URL        | http://localhost:5000     | WebSocket URL     |
| VITE_STRIPE_PUBLIC_KEY | pk_test_xxx               | Stripe public key |

### Admin Dashboard (.env.local)

| Variable                 | Example                   | Description      |
| ------------------------ | ------------------------- | ---------------- |
| NEXT_PUBLIC_API_BASE_URL | http://localhost:5000/api | Backend API URL  |
| NEXT_PUBLIC_APP_NAME     | MAIO Admin                | App display name |

---

## 🚀 Running All Services

### Option 1: Multiple Terminal Windows

**Terminal 1 - Backend:**

```bash
cd MAIO-Backend
npm start
```

**Terminal 2 - Frontend:**

```bash
cd MAIO-front
npm run dev
```

**Terminal 3 - Admin:**

```bash
cd maiodashboard
npm run dev
```

### Option 2: Using a Process Manager

Install PM2:

```bash
npm install -g pm2
```

Create `ecosystem.config.js`:

```javascript
module.exports = {
  apps: [
    {
      name: "maio-backend",
      cwd: "./MAIO-Backend",
      script: "npm",
      args: "start",
    },
    {
      name: "maio-frontend",
      cwd: "./MAIO-front",
      script: "npm",
      args: "run dev",
    },
    {
      name: "maio-admin",
      cwd: "./maiodashboard",
      script: "npm",
      args: "run dev",
    },
  ],
};
```

Start all:

```bash
pm2 start ecosystem.config.js
pm2 status
```

---

## 🆘 Troubleshooting

### Backend Issues

**Error: connect ECONNREFUSED 127.0.0.1:27017**

- MongoDB is not running
- Solution: Start MongoDB service

**Error: EADDRINUSE :::5000**

- Port 5000 is already in use
- Solution: Change PORT in .env or kill process on port 5000

**Error: .env is not defined**

- dotenv not loaded
- Solution: Ensure `require("dotenv").config();` at top of index.js

### Frontend Issues

**Error: Cannot find module 'axios'**

- Dependencies not installed
- Solution: Run `npm install`

**VITE_API_BASE_URL not recognized**

- Environment variables not prefixed correctly
- Solution: Ensure variable names start with `VITE_`

**Port 5173 already in use**

- Another Vite app is running
- Solution: Kill process or use `npm run dev -- --port 3001`

### Admin Dashboard Issues

**Error: Cannot GET /**

- Next.js not built
- Solution: Run `npm run build` then `npm start`

**Pages showing 404**

- File names or paths incorrect
- Solution: Check file structure matches routing

### Database Issues

**Error: MongoDB connection timeout**

- MongoDB service not running
- Solution: Start MongoDB or check MongoDB Atlas status

**Error: Authentication failed**

- Wrong credentials in MONGODB_URI
- Solution: Verify username and password in connection string

### General Troubleshooting

1. **Clear Cache & Reinstall**

   ```bash
   rm -rf node_modules package-lock.json
   npm install
   ```

2. **Check Node Version**

   ```bash
   node --version  # Should be v18+
   ```

3. **Verify All Ports Are Available**

   ```bash
   # Windows
   netstat -ano | findstr :5000

   # macOS/Linux
   lsof -i :5000
   ```

4. **Check Environment Variables**

   - Verify .env files exist in each directory
   - Check for typos in variable names
   - Ensure sensitive values are correct

5. **Check Logs**
   - Backend: Console output from `npm start`
   - Frontend: Browser console (F12)
   - Admin: Browser console and Next.js terminal

---

## 🚀 Production Deployment

### Backend Deployment (Heroku)

1. **Install Heroku CLI**
2. **Create Heroku App**

   ```bash
   heroku create maio-backend
   ```

3. **Set Environment Variables**

   ```bash
   heroku config:set JWT_SECRET=production_secret
   heroku config:set MONGODB_URI=production_mongo_uri
   # ... set all production variables
   ```

4. **Deploy**
   ```bash
   git push heroku main
   ```

### Frontend Deployment (Vercel)

1. **Connect GitHub to Vercel**
2. **Import MAIO-front Repository**
3. **Set Environment Variables**

   - VITE_API_BASE_URL
   - VITE_STRIPE_PUBLIC_KEY
   - etc.

4. **Deploy**
   - Automatic on GitHub push
   - Or manual via Vercel CLI

### Admin Dashboard Deployment (Vercel)

Same as frontend deployment.

---

## ✅ Verification Checklist

- [ ] Node.js v18+ installed
- [ ] npm v9+ installed
- [ ] Git installed and configured
- [ ] MongoDB running (local or Atlas)
- [ ] Backend .env configured
- [ ] Frontend .env.local configured
- [ ] Admin .env.local configured
- [ ] All dependencies installed
- [ ] Backend running on port 5000
- [ ] Frontend running on port 5173
- [ ] Admin running on port 3000
- [ ] Can login to each application
- [ ] Database connection working
- [ ] Email service configured
- [ ] Stripe keys configured

---

**Need Help?**

- Check [CONTRIBUTING.md](CONTRIBUTING.md)
- Review individual README files
- Create GitHub issue

---

**Last Updated**: January 2026 | **Version**: 1.0.0
