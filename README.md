# API Security Assessment Project

## Overview

This project documents a comprehensive security assessment conducted on the DummyJSON public API. The assessment identifies real-world API vulnerabilities including authentication bypasses, IDOR (Insecure Direct Object Reference), mass data exposure, missing rate limiting, and input validation gaps.

This project was completed as part of a security analysis assignment, demonstrating skills in:
- API security analysis
- Authentication & authorization assessment
- Risk identification
- Security documentation
- SaaS security fundamentals

## Tools Used

- **Postman** – Manual API testing and request manipulation
- **Browser DevTools** – Traffic capture and endpoint discovery
- **DummyJSON** – Target API (deliberately vulnerable demo API)

## Key Findings

### High Severity Vulnerabilities

| Vulnerability | Description |
|---------------|-------------|
| **Missing Authentication** | The `/users/{id}` endpoint returns complete user profiles without any authentication required |
| **IDOR** | After logging in as User A, the tester could access User B's full profile by changing the ID in the URL |

### Medium Severity Vulnerabilities

| Vulnerability | Description |
|---------------|-------------|
| **Mass Data Exposure** | The `/users` endpoint returns all 30+ user records in a single request without authentication |
| **Missing Rate Limiting** | The API accepts unlimited rapid authentication requests with no 429 errors |

### Positive Security Controls

- Token validation works correctly (`/auth/me` returns 401 without token)
- Authentication system returns valid access tokens
- Basic input validation prevents SQL injection crashes

## Sample Attack Vectors Tested

### IDOR Attack
```http
GET https://dummyjson.com/users/2
Authorization: Bearer [token_from_user_1]
