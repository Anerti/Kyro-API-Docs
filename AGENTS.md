# Kyro

Personal finance management API — transactions, categories, user auth, IP tracking.

## Stack

- **OpenAPI 3.0.3** — API specification first, no backend code yet
- **Obsidian Canvas** — MCD (Modèle Conceptuel de Données) in `mcd.canvas`
- **Git** — single `main` branch

## Project structure

```
tetibola/
  openapi.yaml      — Full API spec (23 endpoints, 45+ schemas)
  mcd.canvas        — MCD diagram (Obsidian Canvas)
  .obsidian/        — Obsidian vault config + plugins
```

## Endpoints

| Group | Endpoints |
|-------|-----------|
| Auth | `POST /auth/register`, `/login`, `/forgot-password`, `/reset-password` |
| Users | `GET/PATCH/DELETE /users/me`, `POST /users/me/change-password`, `PATCH /users/me/email` |
| Transactions | `GET/POST /transactions`, `GET /transactions/summary`, `GET/PATCH/DELETE /transactions/{transactionId}` |
| Categories | `GET/POST /categories`, `GET/PATCH/DELETE /categories/{categoryId}` |
| IP Addresses | `GET /users/me/ip-addresses`, `PATCH/DELETE /users/me/ip-addresses/{ipAddressId}` |

## Conventions

- **US English** field names (organization, color)
- **camelCase** for API fields (firstName, createdAt)
- **UUID** primary keys on all entities
- **Composite PKs** on junction tables (transaction_category, user_ip_address, user_password)
- **Soft delete** is not used; entities have a `status` field (active/inactive)
- **Password history** — stored in a dedicated `password` table; reuse is blocked server-side
- **Email enumeration prevention** — forgot-password always returns 200

## Common commands

```bash
# Validate the spec
npx @apidevtools/swagger-cli validate openapi.yaml

# Commit convention
git commit -m "feat: add …"
git commit -m "fix: correct …"
git commit -m "refactor: move …"
git commit -m "docs: update …"
```

## Common pitfalls

- The MCD uses junction tables (user_transaction, transaction_category) as **conceptual reading aids** — they are NOT physical DB tables except when they carry extra attributes (user_ip_address has `last_seen_at`, transaction_category has timestamps). When unsure, check the canvas edges.
- `user.password` was removed from the MCD — password is now a dedicated table linked via `user_password`.
- OpenAPI spec uses `3.0.3` for compatibility with the Obsidian OpenAPI Renderer plugin.
- Do NOT use `yaml.dump()` to rewrite hand-crafted YAML — it destroys formatting and comments.
