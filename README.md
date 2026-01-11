# ProvIDe - Bank-Verified Digital Identity Platform

A next-generation digital identity infrastructure that revolutionizes how third-party platforms verify user identity. Instead of requiring users to upload identity documents, ProvIDe leverages the user's existing bank relationship as a trusted identity anchor.

## Overview

ProvIDe is a digital identity platform that securely delegates authentication to regulated banks via **OpenFinance.ai** and returns cryptographically signed identity assertions that meet enterprise security and compliance standards.

### Key Value Propositions

- **Bank-Level Security:** Leverage existing bank KYC verification without storing sensitive documents
- **Zero Friction:** Instant verification eliminates document uploads and reduces abandonment
- **Regulatory Compliance:** Built on OAuth 2.0 and OpenID Connect standards for enterprise use

## Team

**Students:**
- Amit Zamir
- Noa Almakais
- May Gorvitz
- Hai Tal

**Supervisor:** Ari Ben Ephraim

**Repository:** [https://github.com/Amit-Za/provide.git](https://github.com/Amit-Za/provide.git)

## Problem Statement

Traditional KYC processes create significant friction:
- **High Friction:** Document-based KYC causes 30-40% user abandonment
- **Security Risk:** Storing identity documents creates breach liability
- **Redundant Verification:** Users verify identity repeatedly across services
- **Insufficient Alternatives:** Social login lacks legal assurance for regulated use

## Solution

ProvIDe bridges the gap between bank-level identity verification and third-party service needs, enabling instant, secure identity verification without document storage.

### How It Works

1. User clicks "Authenticate with Bank" on a digital service
2. Secure redirect to bank via OpenFinance.ai
3. Strong authentication at bank (password, OTP, biometrics)
4. Bank confirms identity and returns digital assertion
5. Service receives verified identity confirmation - no documents needed

### Operating Modes

- **Identity Verification Mode:** One-time or ongoing verification with cryptographically signed assertions
- **OAuth IdP Mode:** Full OAuth 2.0 / OpenID Connect provider for seamless third-party login

## Core Use Cases

### 1. Loan & Financial Services
Eliminate document uploads and selfie verification. Enable instant account creation with bank-verified identity for loans, credit applications, and financial products.

### 2. E-commerce & Trading
Verify customers and sellers instantly. Reduce identity fraud, enable verified account creation, and streamline onboarding for trading platforms and marketplaces.

### 3. Regulated Services
Insurance, cryptocurrency platforms, age-restricted services, and highly regulated industries requiring verified identity with legal assurance.

## Functional Requirements

- Third-party platform registration and approval
- OAuth authorization and token issuance
- Explicit user consent with clear scope definition
- Policy-based attribute disclosure
- Time-limited and revocable identity assertions
- Identity assertion generation and validation
- Token management and lifecycle handling
- Audit logging for compliance and security
- OpenFinance.ai integration
- RTL (Right-to-Left) UI support
- Responsive design
- No storage of sensitive data
- Dual mode operation (verification and IdP)

## Architecture

### System Components

The system architecture consists of three main components:

1. **Client Application** - Angular or React frontend with RTL support
2. **ProvIDe Platform** - Microservices-based backend
3. **Bank Authentication Layer** - OAuth 2.0 via OpenFinance.ai

### Microservices

- **OAuth Authorization Server** - OAuth 2.0/OpenID Connect flows, token issuance
- **Client Registry Service** - Service registration and onboarding
- **Consent Orchestration Service** - User consent management
- **OpenFinance.ai Integration Layer** - Bank OAuth flow orchestration
- **Identity Assertion Engine** - JWT assertion generation with cryptographic signatures
- **Audit & Compliance Module** - Event logging and compliance reporting

### Database Schema

- **users** - Authentication status, encrypted bank_user_id (no PII)
- **services** - Registered digital services (client_id, client_secret)
- **authorizations** - User consent records (scopes, timestamps)
- **tokens** - Token management (only hashes stored, not actual tokens)
- **audit_logs** - Immutable compliance logs
- **banks** - Bank configuration and integration settings

### Inter-Service Communication

- **RabbitMQ** - Asynchronous communication (audit logs, token revocation, notifications)
- **HTTP/REST** - Synchronous communication (OAuth flows, service registration)

## Technology Stack

### Backend
- **Runtime:** Node.js 18+
- **Framework:** Express.js
- **Database:** PostgreSQL 15+ with Prisma ORM
- **Caching:** Redis (token blacklist, rate limiting, session storage)
- **Message Queue:** RabbitMQ (async processing, event-driven communication)

### Frontend
- **Framework:** Angular or React
- **Styling:** Tailwind CSS
- **Features:** RTL support, OAuth redirect handling, responsive design

### Security Libraries
- **JWT:** jsonwebtoken / jose
- **OAuth:** node-oauth2-server / oauth2orize
- **Crypto:** Node crypto (built-in)
- **Hashing:** bcrypt

### Security & Encryption
- **TLS 1.3** - All external communications
- **AES-256-GCM** - Data encryption at rest
- **Bcrypt (cost 12)** - Client secret hashing
- **SHA-256** - Token hashing for revocation tracking
- **RSA-2048 / ECDSA-P256** - JWT signing keys
- **JWKS** - Secure key management with rotation

## Project Structure

```
provide/
├── index.html    # Main project documentation webpage
└── README.md     # This file
```

## Security & Compliance

### Data Privacy
- **No PII Storage:** System stores only authentication metadata, not personal information
- **No Document Storage:** Identity documents are never stored
- **No Financial Data:** Bank financial data is never accessed or stored
- **Token Hashing:** Only token hashes are stored, not actual tokens

### Security Measures
- **OAuth 2.0 with PKCE** - Prevents authorization code interception
- **Short-lived Tokens** - Access tokens expire quickly, refresh tokens for renewal
- **Scope-based Access** - Fine-grained permission control
- **Rate Limiting** - Per-client, per-endpoint protection
- **CORS** - Strict origin validation
- **Audit Logging** - Immutable logs for compliance

### Compliance
- **GDPR Compliant** - Data minimization, consent management, right to deletion
- **Financial Regulation** - Adheres to financial service regulations
- **Audit Trails** - Complete event logging for regulatory requirements

## Related Work

Current solutions have limitations:
- **Traditional KYC Providers:** Rely on document upload and biometrics, introducing high friction and security risks
- **Open Banking Platforms:** Expose financial data but do not provide identity assurance or verification services
- **Global Identity Providers (Social Login):** Convenient but not suitable for regulated use cases requiring legal assurance
- **Bank Identity Gap:** Banks perform strictest verification but don't serve as identity providers for external services

### Technical Foundation
- **OAuth 2.0:** Authorization framework for secure authentication flows
- **OpenID Connect:** Identity layer on top of OAuth 2.0 for identity verification
- **JWT (JSON Web Token):** Cryptographically signed identity assertions
- **JWS (JSON Web Signature):** Digital signatures for token integrity

## References

- [OAuth 2.0 Specification](https://oauth.net/2/)
- [OpenID Connect Core 1.0](https://openid.net/specs/openid-connect-core-1_0.html)
- [RFC 7636: PKCE](https://tools.ietf.org/html/rfc7636)
- [JSON Web Token (JWT)](https://jwt.io/)
- [OpenFinance.ai Documentation](https://openfinance.ai)
- [GDPR Compliance Guide](https://gdpr.eu/)

---

**Note:** This is an academic project. For production use, additional security audits, penetration testing, and regulatory approvals would be required.

For detailed documentation, see [index.html](index.html).
