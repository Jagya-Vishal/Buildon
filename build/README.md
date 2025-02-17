VITE_API_URL=https://your-backend-url.com
```

### Backend (.env)
```
DATABASE_URL=your-database-url
SESSION_SECRET=your-session-secret
FRONTEND_URL=https://your-netlify-url.com
PORT=5000
```

## Deployment Steps

### Frontend Deployment (Netlify)

1. Create a new site in Netlify:
   - Connect to your Git repository
   - Set the build command to: `npm run build`
   - Set the publish directory to: `dist/public`

2. Configure environment variables in Netlify:
   - Go to Site settings > Build & deploy > Environment
   - Add the following variable:
     ```
     VITE_API_URL=https://your-backend-url.com
     ```

3. Enable forms if using Netlify Forms:
   - Add `forms` attribute to your HTML forms
   - Configure form notifications in Netlify

4. Deploy triggers:
   - Enable automatic deploys from your main branch
   - Configure build hooks if needed

### Backend Deployment (Render, Railway, or similar)

1. Choose a hosting provider (Render recommended for easy PostgreSQL setup)
2. Set up environment variables:
   ```
   DATABASE_URL=your-database-url
   SESSION_SECRET=your-session-secret
   FRONTEND_URL=https://your-netlify-url.com
   PORT=5000
   ```

3. Configure build settings:
   - Build command: `npm install && npm run build`
   - Start command: `npm start`
   - Node version: 20.x

4. Configure your database:
   - Create a new PostgreSQL instance
   - Set up the database URL in your environment variables
   - Run migrations using `npm run db:push`

### Domain Configuration

1. Set up custom domain in Netlify (optional):
   - Go to Site settings > Domain management
   - Add your custom domain
   - Configure DNS settings

2. Update CORS settings:
   - Add your Netlify domain to the backend's CORS configuration
   - Update the frontend API URL to point to your backend

## Quick Deployment Steps

1. Frontend (Netlify):
   ```bash
   # In your local repository
   git push origin main
   ```
   Netlify will automatically deploy from your main branch

2. Backend:
   ```bash
   # Deploy to your chosen platform (e.g., Render)
   git push
   ```

3. Verify deployment:
   - Check frontend URL
   - Test API endpoints
   - Verify database connections
   - Test authentication flow

## Local Development

1. Frontend:
   ```bash
   npm install
   npm run dev
   ```

2. Backend:
   ```bash
   cd backend
   npm install
   npm run dev