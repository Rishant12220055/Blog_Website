# 🚀 Vercel Deployment Guide

This guide will walk you through deploying your React BlogSpace application to Vercel.

## 📋 Prerequisites

- [Vercel Account](https://vercel.com/signup)
- [GitHub Account](https://github.com)
- [MongoDB Atlas Account](https://www.mongodb.com/atlas) (for database)

## 🎯 Deployment Strategy

We'll deploy this as **two separate projects**:
1. **Frontend** (React app) → Vercel
2. **Backend** (Express API) → Vercel

## 📦 Step 1: Prepare Your Repository

### 1.1 Update Backend for Vercel

Your backend already has a `vercel.json` file, but let's ensure it's optimized:

```json
{
    "version": 2,
    "builds": [
        {
            "src": "server.js",
            "use": "@vercel/node"
        }
    ],
    "routes": [
        {
            "src": "/(.*)",
            "dest": "server.js"
        }
    ]
}
```

### 1.2 Update Backend Server

Make sure your `backend/server.js` handles Vercel's serverless environment:

```javascript
const express = require('express');
const mongoose = require('mongoose');
const cors = require('cors');
require('dotenv').config();

const authRoutes = require('./routes/auth');
const fileRoutes = require('./routes/files');
const blogRoutes = require('./routes/blogs');

const app = express();

// Middleware
app.use(cors({
  origin: process.env.CORS_ORIGIN || 'http://localhost:5173',
  credentials: true
}));
app.use(express.json());

// Routes
app.use('/api/auth', authRoutes);
app.use('/api/files', fileRoutes);
app.use('/api/blogs', blogRoutes);

// Health check endpoint
app.get('/api/health', (req, res) => {
  res.json({ status: 'OK', timestamp: new Date().toISOString() });
});

// Database connection
mongoose.connect(process.env.MONGODB_URI)
  .then(() => {
    console.log('Connected to MongoDB');
    if (process.env.NODE_ENV !== 'production') {
      const PORT = process.env.PORT || 5000;
      app.listen(PORT, () => {
        console.log(`Server running on port ${PORT}`);
      });
    }
  })
  .catch((error) => {
    console.error('MongoDB connection error:', error);
  });

module.exports = app;
```

## 🌐 Step 2: Deploy Backend to Vercel

### 2.1 Create Backend Repository

1. **Create a new repository** for your backend:
   ```bash
   # Create a new directory for backend
   mkdir blogspace-backend
   cd blogspace-backend
   
   # Copy backend files
   cp -r ../wordloom/backend/* .
   
   # Initialize git
   git init
   git add .
   git commit -m "Initial backend commit"
   
   # Push to GitHub
   git remote add origin https://github.com/yourusername/blogspace-backend.git
   git push -u origin main
   ```

### 2.2 Deploy Backend to Vercel

1. **Go to [Vercel Dashboard](https://vercel.com/dashboard)**
2. **Click "New Project"**
3. **Import your backend repository**
4. **Configure the project**:
   - **Framework Preset**: Node.js
   - **Root Directory**: `./` (or leave empty)
   - **Build Command**: Leave empty (not needed for Node.js)
   - **Output Directory**: Leave empty
   - **Install Command**: `npm install`

### 2.3 Set Environment Variables

In your Vercel project settings, add these environment variables:

```env
# MongoDB Configuration
MONGODB_URI=mongodb+srv://your-username:your-password@your-cluster.mongodb.net/blogspace?retryWrites=true&w=majority

# JWT Configuration
JWT_SECRET=your-super-secret-jwt-key-here
JWT_EXPIRE=7d

# CORS Configuration
CORS_ORIGIN=https://your-frontend-domain.vercel.app

# Node Environment
NODE_ENV=production
```

### 2.4 Deploy

Click **"Deploy"** and wait for the deployment to complete. Note your backend URL (e.g., `https://blogspace-backend.vercel.app`).

## ⚛️ Step 3: Deploy Frontend to Vercel

### 3.1 Create Frontend Repository

1. **Create a new repository** for your frontend:
   ```bash
   # Create a new directory for frontend
   mkdir blogspace-frontend
   cd blogspace-frontend
   
   # Copy frontend files
   cp -r ../wordloom/frontend/* .
   
   # Initialize git
   git init
   git add .
   git commit -m "Initial frontend commit"
   
   # Push to GitHub
   git remote add origin https://github.com/yourusername/blogspace-frontend.git
   git push -u origin main
   ```

### 3.2 Update Frontend API Configuration

Create a `.env` file in your frontend directory:

```env
# Production Backend URL
VITE_BACKEND_URL=https://your-backend-domain.vercel.app/api
```

### 3.3 Deploy Frontend to Vercel

1. **Go to [Vercel Dashboard](https://vercel.com/dashboard)**
2. **Click "New Project"**
3. **Import your frontend repository**
4. **Configure the project**:
   - **Framework Preset**: Vite
   - **Root Directory**: `./` (or leave empty)
   - **Build Command**: `npm run build`
   - **Output Directory**: `dist`
   - **Install Command**: `npm install`

### 3.4 Set Environment Variables

In your frontend Vercel project settings, add:

```env
VITE_BACKEND_URL=https://your-backend-domain.vercel.app/api
```

### 3.5 Deploy

Click **"Deploy"** and wait for the deployment to complete.

## 🔧 Step 4: Configure MongoDB Atlas

### 4.1 Create MongoDB Atlas Cluster

1. **Sign up for [MongoDB Atlas](https://www.mongodb.com/atlas)**
2. **Create a new cluster** (free tier is fine)
3. **Set up database access**:
   - Create a database user with read/write permissions
   - Note the username and password

### 4.2 Configure Network Access

1. **Go to Network Access** in Atlas
2. **Add IP Address**: `0.0.0.0/0` (allows all IPs)
3. **Or add specific IPs** for better security

### 4.3 Get Connection String

1. **Click "Connect"** on your cluster
2. **Choose "Connect your application"**
3. **Copy the connection string**
4. **Replace `<password>`** with your actual password
5. **Add database name**: `?retryWrites=true&w=majority&dbName=blogspace`

## 🔗 Step 5: Connect Everything

### 5.1 Update Backend Environment Variables

In your backend Vercel project:

1. **Go to Settings → Environment Variables**
2. **Update `MONGODB_URI`** with your Atlas connection string
3. **Update `CORS_ORIGIN`** with your frontend URL
4. **Redeploy** the backend

### 5.2 Test Your Deployment

1. **Visit your frontend URL**
2. **Try to register/login**
3. **Create a blog post**
4. **Check if everything works**

## 🚨 Troubleshooting

### Common Issues

#### 1. CORS Errors
- Ensure `CORS_ORIGIN` in backend matches your frontend URL exactly
- Check that the frontend URL includes `https://`

#### 2. MongoDB Connection Issues
- Verify your Atlas connection string
- Check if your IP is whitelisted in Atlas
- Ensure database user has correct permissions

#### 3. Environment Variables Not Working
- Redeploy after adding environment variables
- Check variable names match exactly (case-sensitive)
- Restart the deployment

#### 4. Build Errors
- Check if all dependencies are in `package.json`
- Ensure Node.js version compatibility
- Check for TypeScript errors

### Debugging Steps

1. **Check Vercel logs** in the deployment dashboard
2. **Test API endpoints** directly using Postman or curl
3. **Verify environment variables** are set correctly
4. **Check MongoDB Atlas** connection and permissions

## 📊 Monitoring

### Vercel Analytics

- **Go to your Vercel dashboard**
- **View deployment logs**
- **Monitor performance metrics**
- **Check error rates**

### MongoDB Atlas Monitoring

- **Monitor database performance**
- **Check connection counts**
- **View query performance**

## 🔄 Continuous Deployment

### Automatic Deployments

Both frontend and backend will automatically redeploy when you push to your GitHub repositories.

### Manual Deployments

- **Frontend**: Push to `main` branch
- **Backend**: Push to `main` branch
- **Environment Variables**: Update in Vercel dashboard

## 🎉 Success!

Your React BlogSpace is now live on Vercel! 

- **Frontend**: `https://your-frontend.vercel.app`
- **Backend**: `https://your-backend.vercel.app`
- **Database**: MongoDB Atlas

## 📚 Additional Resources

- [Vercel Documentation](https://vercel.com/docs)
- [MongoDB Atlas Documentation](https://docs.atlas.mongodb.com/)
- [Express.js Deployment Guide](https://expressjs.com/en/advanced/best-practices-performance.html)
- [React Deployment Best Practices](https://create-react-app.dev/docs/deployment/)

---

**Need help?** Check the troubleshooting section or open an issue on GitHub! 