# HashTrace API Reference

Complete API documentation for HashTrace.

## Base URL

```
http://localhost:9000/api
```

## Authentication

All requests require an API key in the Authorization header:

```
Authorization: Bearer YOUR_API_KEY
```

## Events Endpoint

### Create Event

**POST** `/events`

Create a new event in the audit trail.

**Request Body**:

```json
{
  "type": "login",
  "userId": "123",
  "source": "192.168.1.1",
  "data": {
    "username": "john@example.com"
  }
}
```

**Response**:

```json
{
  "id": "evt_abc123",
  "type": "login",
  "userId": "123",
  "source": "192.168.1.1",
  "timestamp": "2024-12-04T10:30:00Z",
  "hash": "abc123def456...",
  "status": "verified"
}
```

### List Events

**GET** `/events?limit=10&offset=0`

List events with pagination.

**Query Parameters**:
- `limit` - Number of events to return (default: 10)
- `offset` - Number of events to skip (default: 0)
- `type` - Filter by event type
- `userId` - Filter by user ID

**Response**:

```json
{
  "data": [...],
  "total": 100,
  "limit": 10,
  "offset": 0
}
```

### Get Event

**GET** `/events/:id`

Get a specific event by ID.

**Response**:

```json
{
  "id": "evt_abc123",
  "type": "login",
  "userId": "123",
  "timestamp": "2024-12-04T10:30:00Z",
  "hash": "abc123def456...",
  "verified": true
}
```

## Search Endpoint

### Search Events

**POST** `/search`

Search events with advanced query syntax.

**Request Body**:

```json
{
  "query": "type:login AND userId:123",
  "timeRange": {
    "start": "2024-12-01T00:00:00Z",
    "end": "2024-12-04T23:59:59Z"
  },
  "limit": 50
}
```

**Response**:

```json
{
  "results": [...],
  "total": 25,
  "executionTime": "45ms"
}
```

## Health Check

**GET** `/health`

Check API health status.

**Response**:

```json
{
  "status": "healthy",
  "timestamp": "2024-12-04T10:30:00Z",
  "database": "connected",
  "cache": "connected"
}
```

## Error Responses

### 400 Bad Request

```json
{
  "error": "Invalid request",
  "message": "Event type is required"
}
```

### 401 Unauthorized

```json
{
  "error": "Unauthorized",
  "message": "Invalid API key"
}
```

### 500 Internal Server Error

```json
{
  "error": "Internal Server Error",
  "message": "Database connection failed"
}
```

## Rate Limiting

API requests are rate limited to 100 requests per minute per API key.

**Headers**:
- `X-RateLimit-Limit` - Rate limit
- `X-RateLimit-Remaining` - Remaining requests
- `X-RateLimit-Reset` - Reset time

---

For more information, see [README.md](../README.md)
