# 🚀 Deployment Guide - Expense Tracker

## Quick Deploy Options (Free)

### Option 1: Railway (Recommended)

1. **Push to GitHub**: `git add . && git commit -m "Ready for deployment" && git push`
2. **Go to**: [railway.app](https://railway.app)
3. **Sign up** with GitHub
4. **Create Project** → "Deploy from GitHub repo"
5. **Add Database**: Click "+" → "Database" → "PostgreSQL"
6. **Set Environment Variables**:
   ```
   DB_HOST=<from database tab>
   DB_USER=<from database tab>
   DB_PASSWORD=<from database tab>
   DB_NAME=<from database tab>
   DB_PORT=5432
   NODE_ENV=production
   ```
7. **Deploy**: Railway will automatically build and deploy
8. **Run Migrations**: In Railway dashboard → "Deployments" → "View Logs" → Run:
   ```bash
   npm run db:migrate
   npm run db:seed
   ```

### Option 2: Render (Detailed Guide)

#### Step 1: Prepare Your Repository

1. **Push to GitHub** (if not already done):
   ```bash
   git add .
   git commit -m "Ready for Render deployment"
   git push origin main
   ```

#### Step 2: Create Render Account

1. **Go to**: [render.com](https://render.com)
2. **Sign up** with GitHub (recommended) or email
3. **Verify your email** if using email signup

#### Step 3: Create Web Service

1. **Click "New +"** → **"Web Service"**
2. **Connect GitHub**:
   - Click "Connect GitHub account"
   - Authorize Render to access your repositories
   - Select your expense tracking repository
3. **Configure Service**:
   - **Name**: `expense-tracker` (or your preferred name)
   - **Environment**: `Node`
   - **Region**: Choose closest to your users
   - **Branch**: `main` (or your default branch)
   - **Root Directory**: Leave empty (uses root)
   - **Build Command**: `npm run build`
   - **Start Command**: `npm run start`

#### Step 4: Add PostgreSQL Database

1. **Click "New +"** → **"PostgreSQL"**
2. **Configure Database**:
   - **Name**: `expense-tracker-db`
   - **Database**: `expense_tracker`
   - **User**: `expense_user` (or auto-generated)
   - **Region**: Same as your web service
3. **Click "Create Database"**
4. **Wait for database to be ready** (takes 1-2 minutes)

#### Step 5: Configure Environment Variables

1. **Go to your Web Service** → **"Environment"** tab
2. **Add these variables**:
   ```
   DB_HOST=<from database dashboard>
   DB_USER=<from database dashboard>
   DB_PASSWORD=<from database dashboard>
   DB_NAME=expense_tracker
   DB_PORT=5432
   NODE_ENV=production
   PORT=10000
   ```
3. **Get database credentials**:
   - Go to your PostgreSQL service dashboard
   - Copy the "External Database URL" or individual values
   - Format: `postgresql://user:password@host:port/database`

#### Step 6: Deploy

1. **Click "Create Web Service"**
2. **Wait for build** (3-5 minutes):
   - Render will install dependencies
   - Run `npm run build`
   - Start your application
3. **Check build logs** for any errors

#### Step 7: Setup Database

1. **Go to "Shell"** in your web service dashboard
2. **Run migrations**:
   ```bash
   npm run db:migrate
   ```
3. **Seed initial data**:
   ```bash
   npm run db:seed
   ```

#### Step 8: Access Your App

- **Your app URL**: `https://expense-tracker.onrender.com`
- **Custom domain**: Available in Pro plan
- **SSL**: Automatically enabled

#### Render Free Tier Limits:

- **750 hours/month** (usually enough for small apps)
- **Sleeps after 15 minutes** of inactivity (wakes up on next request)
- **Cold start**: 30-60 seconds after sleep
- **Bandwidth**: 100GB/month
- **Database**: 1GB storage, 1GB RAM

#### Troubleshooting Render:

- **Build fails**: Check Node.js version in package.json
- **Database connection**: Verify environment variables match database credentials
- **App crashes**: Check logs in "Logs" tab
- **Slow startup**: Normal for free tier (sleeps when inactive)
- **Environment variables**: Make sure they're set in "Environment" tab, not in code

### Option 3: Vercel + Neon

1. **Database**: [neon.tech](https://neon.tech) (free PostgreSQL)
2. **Hosting**: [vercel.com](https://vercel.com)
3. **Connect GitHub** and deploy
4. **Set environment variables** in Vercel dashboard

## Environment Variables Needed

```bash
DB_HOST=your_postgres_host
DB_USER=your_postgres_user
DB_PASSWORD=your_postgres_password
DB_NAME=your_postgres_database
DB_PORT=5432
NODE_ENV=production
```

## After Deployment

1. **Run migrations**: `npm run db:migrate`
2. **Seed data**: `npm run db:seed`
3. **Test your app**: Visit the provided URL

## Troubleshooting

- **Build fails**: Check Node.js version (use 20.x)
- **Database connection**: Verify environment variables
- **Migrations**: Run them after first deployment
- **Logs**: Check deployment platform logs for errors

## Your App Will Be Available At:

- Railway: `https://your-app-name.railway.app`
- Render: `https://your-app-name.onrender.com`
- Vercel: `https://your-app-name.vercel.app`
