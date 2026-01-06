# HashTrace Deployment Guide

Complete guide for deploying HashTrace to production.

## Prerequisites

- Node.js 18+
- PostgreSQL 13+
- Redis 6+
- Docker and Docker Compose
- SSL/TLS certificates (for production)

## Local Development

### Setup

```bash
git clone https://github.com/yourusername/hashtrace.git
cd hashtrace
npm install
cp .env.example .env
docker-compose up -d
npm run db:init
npm run dev
```

### Verify

```bash
curl http://localhost:9000/api/health
```

## Docker Deployment

### Build Image

```bash
docker build -t hashtrace:2.1.0 .
```

### Run Container

```bash
docker run -d \
  --name hashtrace \
  -p 9000:9000 \
  -e DATABASE_URL=postgresql://user:pass@db:5432/hashtrace \
  -e REDIS_URL=redis://cache:6379 \
  -e JWT_SECRET=your-secret-key \
  hashtrace:2.1.0
```

### Docker Compose

```bash
docker-compose up -d
```

## Production Deployment

### Environment Configuration

Create `.env.production`:

```
NODE_ENV=production
API_PORT=9000
DATABASE_URL=postgresql://user:pass@db.example.com:5432/hashtrace
REDIS_URL=redis://cache.example.com:6379
JWT_SECRET=your-production-secret-key
LOG_LEVEL=info
```

### Database Setup

```bash
npm run db:migrate
npm run db:seed
```

### Start Application

```bash
npm start
```

### Reverse Proxy (Nginx)

```nginx
upstream hashtrace {
  server localhost:9000;
}

server {
  listen 443 ssl http2;
  server_name hashtrace.example.com;

  ssl_certificate /etc/ssl/certs/hashtrace.crt;
  ssl_certificate_key /etc/ssl/private/hashtrace.key;

  location / {
    proxy_pass http://hashtrace;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;
  }
}
```

## Monitoring

### Health Check

```bash
curl https://hashtrace.example.com/api/health
```

### Logs

```bash
tail -f /var/log/hashtrace/application.log
```

### Metrics

Access Prometheus at `http://localhost:9090`

## Backup & Recovery

### Backup Database

```bash
pg_dump hashtrace > backup.sql
```

### Restore Database

```bash
psql hashtrace < backup.sql
```

## Troubleshooting

### Port Already in Use

```bash
lsof -i :9000
kill -9 <PID>
```

### Database Connection Error

```bash
psql -U postgres -d hashtrace
```

### Redis Connection Error

```bash
redis-cli ping
```

---

For more information, see [README.md](../README.md)
