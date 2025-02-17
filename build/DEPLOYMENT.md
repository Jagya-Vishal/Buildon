# Deployment Guide for B2B Textile Printing Platform

## Prerequisites
1. A Netlify account
2. A hosting platform for the backend (Render, Railway, or similar)
3. PostgreSQL database (can be provisioned on Render or Railway)

## Step 1: Database Setup
1. Create a new PostgreSQL database on your chosen platform
2. Note down the following credentials:
   - Database URL
   - Database name
   - Username
   - Password
   - Host
   - Port

## Step 2: Backend Deployment
1. Choose a hosting platform (Render recommended)
2. Create a new Web Service
3. Configure environment variables:
   ```
   DATABASE_URL=postgresql://username:password@host:port/database
   SESSION_SECRET=your-secure-random-string
   FRONTEND_URL=https://your-netlify-domain.netlify.app
   PORT=5000
   ```
4. Set build configuration:
   - Build Command: `npm install && npm run build`
   - Start Command: `npm start`
   - Node Version: 20.x

5. Deploy the backend:
   - Connect your repository
   - Trigger deployment
   - Note down your backend URL (e.g., https://your-app.onrender.com)

## Step 3: Frontend Deployment (Netlify)
1. Login to Netlify
2. Create new site from Git:
   - Connect to your repository
   - Configure build settings:
     - Build Command: `npm run build`
     - Publish Directory: `dist/public`
     - Node Version: 20.x

3. Configure environment variables:
   - Go to Site Settings > Build & Deploy > Environment
   - Add the following variables:
     ```
     VITE_API_URL=https://your-backend-url.com
     ```

4. Deploy:
   - Trigger deployment from Netlify dashboard
   - Wait for build completion

## Step 4: Final Configuration
1. Update CORS settings:
   - Go to your backend hosting platform
   - Update FRONTEND_URL to match your Netlify domain

2. Verify deployment:
   - Visit your Netlify URL
   - Test user registration/login
   - Verify product catalog loads
   - Test all features requiring database access

## Troubleshooting
1. If database connection fails:
   - Verify DATABASE_URL format
   - Check if database credentials are correct
   - Ensure database is accessible from backend host

2. If authentication doesn't work:
   - Verify SESSION_SECRET is set
   - Check CORS configuration
   - Ensure cookies are being set properly

3. If frontend can't connect to backend:
   - Verify VITE_API_URL is correct
   - Check if backend is running
   - Verify CORS settings

## Local Development
1. Clone the repository
2. Install dependencies:
   ```bash
   npm install
   ```
3. Create .env files:
   - Frontend (.env.local):
     ```
     VITE_API_URL=http://localhost:5000
     ```
   - Backend (.env):
     ```
     DATABASE_URL=your-local-db-url
     SESSION_SECRET=development-secret
     FRONTEND_URL=http://localhost:3000
     PORT=5000
     ```
4. Start development servers:
   ```bash
   # Start backend
   npm run dev

   # In another terminal, start frontend
   npm run dev
   ```

## CI/CD Setup
1. Enable automatic deploys in Netlify
2. Configure build hooks if needed
3. Set up branch deploy previews (optional)
