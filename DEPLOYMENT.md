# Deployment Guide

## Docker Deployment

### Using Docker Compose

Create a `docker-compose.yml` file:

```yaml
version: '3.8'

services:
  backend:
    build: ./tshirt-store-backend
    ports:
      - "8000:8000"
    environment:
      - DEBUG=False
      - SECRET_KEY=your-secret-key
      - ALLOWED_HOSTS=localhost,127.0.0.1
      - DATABASE_URL=postgresql://user:password@db:5432/tshirtstore
    depends_on:
      - db
    volumes:
      - ./media:/app/media
      - ./staticfiles:/app/staticfiles

  frontend:
    build: ./tshirt-store-frontend
    ports:
      - "80:80"
    depends_on:
      - backend

  db:
    image: postgres:15
    environment:
      - POSTGRES_DB=tshirtstore
      - POSTGRES_USER=user
      - POSTGRES_PASSWORD=password
    volumes:
      - postgres_data:/var/lib/postgresql/data

volumes:
  postgres_data:
```

Run with:
```bash
docker-compose up -d
```

## Railway Deployment

### Backend on Railway

1. Install Railway CLI:
```bash
npm install -g @railway/cli
```

2. Login and deploy:
```bash
cd tshirt-store-backend
railway login
railway init
railway up
```

3. Add environment variables in Railway dashboard:
- `SECRET_KEY`
- `DEBUG=False`
- `ALLOWED_HOSTS`
- `DATABASE_URL` (auto-configured with Railway PostgreSQL)

### Frontend on Vercel

1. Install Vercel CLI:
```bash
npm install -g vercel
```

2. Deploy:
```bash
cd tshirt-store-frontend
vercel
```

3. Set environment variable:
- `VITE_API_URL=https://your-backend.railway.app/api`

## Heroku Deployment

### Backend

1. Create `Procfile`:
```
web: gunicorn tshirt_store.wsgi:application
```

2. Deploy:
```bash
heroku create tshirt-store-backend
heroku addons:create heroku-postgresql:mini
git push heroku main
heroku run python manage.py migrate
heroku run python manage.py createsuperuser
```

### Frontend

Deploy to Netlify:
```bash
npm run build
netlify deploy --prod --dir=dist
```

## AWS Deployment

### Backend on EC2

1. Launch EC2 instance (Ubuntu)
2. SSH into instance
3. Install dependencies:
```bash
sudo apt update
sudo apt install python3-pip python3-venv nginx
```

4. Clone and setup:
```bash
git clone https://github.com/Aryankaushik541/tshirt-store-backend.git
cd tshirt-store-backend
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
pip install gunicorn
```

5. Configure Nginx and Gunicorn
6. Setup SSL with Let's Encrypt

### Frontend on S3 + CloudFront

1. Build the app:
```bash
npm run build
```

2. Upload to S3:
```bash
aws s3 sync dist/ s3://your-bucket-name
```

3. Configure CloudFront distribution
4. Setup custom domain

## Environment Variables

### Backend (.env)
```env
SECRET_KEY=your-secret-key-here
DEBUG=False
ALLOWED_HOSTS=yourdomain.com,www.yourdomain.com
DATABASE_URL=postgresql://user:pass@host:5432/dbname
CORS_ALLOWED_ORIGINS=https://yourdomain.com
STRIPE_SECRET_KEY=your-stripe-key
```

### Frontend (.env)
```env
VITE_API_URL=https://api.yourdomain.com/api
```

## Post-Deployment Checklist

- [ ] Set DEBUG=False in production
- [ ] Configure proper database (PostgreSQL)
- [ ] Set up static file serving
- [ ] Configure ALLOWED_HOSTS
- [ ] Set up CORS properly
- [ ] Enable HTTPS/SSL
- [ ] Set up monitoring and logging
- [ ] Configure backup strategy
- [ ] Set up CI/CD pipeline
- [ ] Test all endpoints
- [ ] Monitor performance
- [ ] Set up error tracking (Sentry)

## Monitoring

### Backend Monitoring
- Use Django logging
- Set up Sentry for error tracking
- Monitor database performance
- Track API response times

### Frontend Monitoring
- Google Analytics
- Sentry for error tracking
- Lighthouse for performance
- Real User Monitoring (RUM)

## Backup Strategy

### Database Backups
```bash
# PostgreSQL backup
pg_dump dbname > backup.sql

# Restore
psql dbname < backup.sql
```

### Media Files Backup
- Use S3 or similar object storage
- Set up automated backups
- Test restore procedures

## Security Checklist

- [ ] Use HTTPS everywhere
- [ ] Set secure headers
- [ ] Enable CSRF protection
- [ ] Sanitize user inputs
- [ ] Use environment variables for secrets
- [ ] Regular security updates
- [ ] Rate limiting on API
- [ ] SQL injection prevention
- [ ] XSS protection
- [ ] Secure password storage

## Performance Optimization

### Backend
- Enable database query optimization
- Use Redis for caching
- Implement pagination
- Optimize database indexes
- Use CDN for static files

### Frontend
- Enable code splitting
- Lazy load images
- Minimize bundle size
- Enable gzip compression
- Use CDN for assets
- Implement service workers

## Scaling

### Horizontal Scaling
- Use load balancer
- Multiple backend instances
- Database replication
- CDN for static content

### Vertical Scaling
- Increase server resources
- Optimize database queries
- Use caching effectively
- Monitor and optimize bottlenecks
