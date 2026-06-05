# Kyro

Personal finance management API.

## Prerequisites

- Node.js 18+ (for Swagger CLI validation)
- Obsidian (optional — to view/edit the MCD canvas)

## Setup

```bash
# Validate the API spec
npx @apidevtools/swagger-cli validate openapi.yaml
```

## Endpoints

Base URL: `http://localhost:8080/api/v1`

| Resource | Endpoints |
|----------|-----------|
| Auth | `POST /auth/register`, `/login`, `/forgot-password`, `/reset-password` |
| Profile | `GET/PATCH/DELETE /users/me`, `POST /users/me/change-password`, `PATCH /users/me/email` |
| Transactions | `GET/POST /transactions`, `GET /transactions/summary`, `GET/PATCH/DELETE /transactions/{id}` |
| Categories | `GET/POST /categories`, `GET/PATCH/DELETE /categories/{id}` |
| IP Addresses | `GET /users/me/ip-addresses`, `PATCH/DELETE /users/me/ip-addresses/{id}` |
| AI Conversations | `GET/POST /users/me/conversations`, `GET/DELETE /users/me/conversations/{id}` |

Full spec at `openapi.yaml`.

---

*Spec-first · OpenAPI 3.0.3 · Obsidian Canvas · 28+ endpoints*
