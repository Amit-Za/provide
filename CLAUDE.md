# CLAUDE.md - ProvIDe Project Guide

## Project Overview

**ProvIDe** is a bank-verified digital identity platform — an academic fintech project (Final Project in CS, Fintech & Algorithmic Trading specialization). It enables third-party services to verify user identity through existing bank relationships via OpenFinance.ai, eliminating document-based KYC friction.

**Repository:** https://github.com/Amit-Za/provide.git
**Team:** Amit Zamir, Noa Almakais, May Gorvitz, Hai Tal
**Supervisor:** Ari Ben Ephraim

## Current State

The project is in the **documentation/specification phase**. The repository currently contains:
- `index.html` — Interactive documentation website (Tailwind CSS, Mermaid diagrams, 3D shadow effects)
- `README.md` — Project overview and technical specification
- `logo-dark-mode.html` / `logo-light-mode.html` — Brand logo components
- `ProvIDe Project Definition.pdf` — Formal project specification

No backend or frontend application code has been implemented yet.

## Planned Tech Stack

### Backend
- **Runtime:** Node.js 18+
- **Framework:** Express.js
- **Database:** PostgreSQL 15+ with Prisma ORM
- **Caching:** Redis (token blacklist, rate limiting, sessions)
- **Message Queue:** RabbitMQ (async processing, event-driven)
- **Containerization:** Docker
- **Load Balancing:** NGINX

### Frontend
- **Framework:** Angular or React (TBD)
- **Styling:** Tailwind CSS
- **Features:** RTL (Hebrew) support, responsive design, dark mode

### Security
- OAuth 2.0 with PKCE, OpenID Connect
- JWT with RS256 (RSA-2048 / ECDSA-P256)
- AES-256-GCM encryption at rest, TLS 1.3 in transit
- bcrypt for secret hashing, SHA-256 for token hashing
- JWKS with key rotation

## Planned Architecture

Microservices-based:
1. **OAuth Authorization Server** — OAuth 2.0/OIDC flows, token issuance
2. **Client Registry Service** — Third-party service registration
3. **Consent Orchestration Service** — User consent management
4. **OpenFinance.ai Integration Layer** — Bank OAuth flow orchestration
5. **Identity Assertion Engine** — JWT assertion generation
6. **Audit & Compliance Module** — Event logging

### Database Tables
`users`, `services`, `authorizations`, `tokens`, `audit_logs`, `banks`

### Inter-Service Communication
- RabbitMQ for async (audit logs, token revocation, notifications)
- HTTP/REST for sync (OAuth flows, service registration)

## Documentation Site (index.html)

The documentation site uses:
- **Tailwind CSS** via CDN
- **Mermaid.js** for architecture diagrams (with custom zoom/pan)
- **Vanilla JS** for interactivity (mobile menu, smooth scrolling, active link highlighting)
- 3D shadow effects and card-based layout
- Mobile-responsive with breakpoints at 640px and 768px

### Logo Design
- Lock icon with gradient (`sky-400` to `emerald-400`)
- "ProvIDe" text with gradient accent on "ID"
- Dark and light mode variants

## Key Design Principles

- **Security-first:** No PII storage, no document storage, no financial data access — only authentication metadata
- **Data minimization:** GDPR-compliant by design
- **Standards-based:** OAuth 2.0, OpenID Connect, JWT/JWS
- **Zero friction:** Bank-delegated authentication eliminates document uploads
- **Auditability:** Immutable audit logs for regulatory compliance

## Development Conventions

### Git
- Branch: `master`
- Commit messages: imperative mood, concise descriptions
- **Never** add `Co-Authored-By` or any AI attribution/watermark to commit messages
- Deploy docs via GitHub Pages (static HTML)

### Code Style (Documentation Site)
- Tailwind utility-first CSS
- Semantic HTML with proper heading hierarchy
- Arrow functions, addEventListener for event handling
- querySelector/querySelectorAll for DOM access

### When Implementation Begins
- Follow microservices separation
- Use design patterns: Repository, Factory, Strategy, Observer, Circuit Breaker
- RESTful API design with consistent error format
- All tokens stored as hashes only
- Rate limiting per-client, per-endpoint
- Strict CORS origin validation

## Local Development

```bash
# Serve documentation site locally (VS Code Live Server on port 5501)
# Or any static file server:
npx serve .
```

## Important Notes

- This is an academic project — production use would require additional security audits
- The platform integrates with OpenFinance.ai for bank connectivity
- RTL support is required for Hebrew language UI
- No sensitive data (PII, documents, financial data) should ever be stored
