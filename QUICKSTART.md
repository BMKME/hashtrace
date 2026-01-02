# HashTrace Quick Start Guide

Get HashTrace up and running in 30 minutes.

## Prerequisites

- Node.js 18+
- PostgreSQL 13+
- Redis 6+
- Git

## Installation (5 minutes)

```bash
git clone https://github.com/yourusername/hashtrace.git
cd hashtrace
npm install
cp .env.example .env
npm run db:init
npm start
```

The application will be available at `http://localhost:9000`

## Docker Setup (3 minutes)

```bash
docker-compose up -d
open http://localhost:9000
```

## First Steps (10 minutes)

### 1. Access Dashboard

Open http://localhost:9000 in your browser

### 2. Create API Key

Navigate to Settings → API Keys → Create New Key

### 3. Create Event

Using Node.js SDK:

```javascript
const HashTrace = require('hashtrace');

const client = new HashTrace.Client({
  apiKey: 'your-api-key',
  apiUrl: 'http://localhost:9000'
});

await client.createEvent({
  type: 'login',
  userId: '123',
  source: '192.168.1.1'
});
```

Using cURL:

```bash
curl -X POST http://localhost:9000/api/events \
  -H "Authorization: Bearer your-api-key" \
  -H "Content-Type: application/json" \
  -d '{
    "type": "login",
    "userId": "123",
    "source": "192.168.1.1"
  }'
```

### 4. View Events

Go to Dashboard → Search tab and search for your events

## Common Commands

```bash
npm run dev              # Start with auto-reload
npm test               # Run tests
npm run lint           # Check code style
npm run format         # Format code
npm run db:init        # Initialize database
docker-compose up -d   # Start services
```

## Next Steps

1. Read [README.md](README.md)
2. Check [API Reference](docs/API_REFERENCE.md)
3. Follow [Deployment Guide](docs/DEPLOYMENT.md)
4. Review [Contributing Guidelines](CONTRIBUTING.md)

---

**Ready to go!** Start with the [README.md](README.md) for more information.
