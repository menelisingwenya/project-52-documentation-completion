# Capstone Production Deployment Guide

**Emganwini Nedbank Hub | Master Project Portfolio**  
*Capstone Documentation Deliverable*

---

## 🚀 Architecture & Environments

The Nedbank SmartFin AI Platform utilizes modern cloud hosting with automated CI/CD pipelines:
- **Frontend SPA**: Hosted on **Vercel** with worldwide CDN edge distribution.
- **Backend API Server**: Containerized and deployed on **Render** (Node.js 20 LTS runtime).
- **Relational Database**: Serverless PostgreSQL 16 hosted on **Neon.tech** with SSL encryption.

---

## 🛠️ Step 1: Database Setup (Neon PostgreSQL)
1. Create a PostgreSQL 16 serverless instance on [Neon.tech](https://neon.tech).
2. Note the secure connection string:
   ```env
   DATABASE_URL="postgresql://user:password@ep-sample-12345.eu-central-1.aws.neon.tech/capstone_db?sslmode=require"
   ```
3. Run migrations and database seeding from the backend directory:
   ```bash
   npx prisma migrate deploy
   npx prisma db seed
   ```

---

## 🛠️ Step 2: Backend API Deployment (Render)
1. Link your GitHub repository to [Render.com](https://render.com).
2. Create a **Web Service** with the following configuration:
   - **Root Directory**: `phase-02-backend-development/backend`
   - **Build Command**: `npm install && npx prisma generate`
   - **Start Command**: `node index.js`
3. Set environment variables in Render Dashboard:
   ```env
   PORT=10000
   NODE_ENV=production
   DATABASE_URL=<your_neon_database_url>
   JWT_SECRET=<secure_random_string>
   JWT_EXPIRES_IN=7d
   CORS_ORIGIN=https://nedbank-smartfin-portal.vercel.app
   OPENAI_API_KEY=<your_openai_key>
   ```
4. Confirm health check: `GET https://<your-render-service>.onrender.com/` returns `200 OK`.

---

## 🛠️ Step 3: Frontend Deployment (Vercel)
1. Import repository into [Vercel](https://vercel.com).
2. Configure project settings:
   - **Root Directory**: `phase-03-frontend-development/client`
   - **Framework Preset**: `Vite`
   - **Build Command**: `npm run build`
   - **Output Directory**: `dist`
3. Set environment variables:
   ```env
   VITE_API_URL=https://<your-render-service>.onrender.com/api
   ```
4. Deploy and verify HTTPS URL.
