# Authentication Guide

SecureAPI uses JSON Web Tokens (JWT) for authentication. This guide covers
token generation, usage, and troubleshooting.

## Overview

All API requests (except login and password reset) require a valid JWT token
in the Authorization header:

    Authorization: Bearer <your-token>

## Getting a Token

### Login Endpoint

    POST /api/v2/auth/login

**Request Body:**

```json
{
  "email": "user@example.com",
  "password": "your-password"
}
```

**Successful Response (200):**

```json
{
  "token": "eyJhbGciOiJIUzI1NiIs...",
  "expiresIn": "48h",
  "tokenType": "Bearer"
}
```

## Token Configuration

| Parameter            | Value          | Description                       |
|----------------------|----------------|-----------------------------------|
| Token Type           | Bearer         | Only Bearer tokens are supported  |
| Expiry Duration      | 48 hours       | Tokens expire after 48 hours      |
| Algorithm            | HS256          | HMAC with SHA-256                 |
| Max Login Attempts   | 10             | Account locks after 10 failures   |
| Lockout Duration     | 15 minutes     | Automatic unlock after 15 minutes |
| Min Password Length  | 10 characters  | Minimum password requirement      |

## Refreshing a Token

Before your token expires, you can refresh it:

    POST /api/v2/auth/refresh

Include the current valid token in the Authorization header. A new token will
be returned with a fresh 48-hour expiry.

## Google OAuth Authentication

SecureAPI supports Google OAuth for authentication:

    POST /api/v2/auth/oauth/google

**Request Body:**

```json
{
  "googleToken": "ya29.a0AfH6SMB..."
}
```

**Successful Response (200):**

```json
{
  "token": "eyJhbGciOiJIUzI1NiIs...",
  "expiresIn": "48h",
  "tokenType": "Bearer",
  "provider": "google"
}
```

The `googleToken` should be obtained from Google's OAuth flow. The returned JWT token works the same as standard login tokens.

## Error Codes

| Status Code | Error          | Description                                   |
|-------------|----------------|-----------------------------------------------|
| 401         | UNAUTHORIZED   | Missing or invalid token                      |
| 403         | FORBIDDEN      | Token expired or insufficient permissions     |
| 423         | ACCOUNT_LOCKED | Too many failed login attempts                |

## Security Best Practices

1. Never expose your JWT token in URLs or client-side code
2. Always use HTTPS for API requests
3. Refresh tokens before they expire to avoid service interruption
4. Store tokens securely (httpOnly cookies recommended)
5. Implement token rotation for long-running sessions

## Code Examples

### cURL

```bash
curl -X POST https://api.secureapi.example.com/v2/auth/login \
  -H "Content-Type: application/json" \
  -d '{"email":"user@example.com","password":"your-password"}'
```

### JavaScript (fetch)

```javascript
const response = await fetch('https://api.secureapi.example.com/v2/auth/login', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ email: 'user@example.com', password: 'your-password' })
});
const { token } = await response.json();
```

### Python (requests)

```python
import requests

response = requests.post(
    'https://api.secureapi.example.com/v2/auth/login',
    json={'email': 'user@example.com', 'password': 'your-password'}
)
token = response.json()['token']
```
