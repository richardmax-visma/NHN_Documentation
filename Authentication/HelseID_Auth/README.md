# HelseID Authentication Reference

HelseID is Norway's national authentication service for the health sector, providing secure identity verification for both users and systems.

## When to use

- Any system-to-system (machine-to-machine) API call to NHN/Helsenorge where HelseID is required.
- This document focuses on system-to-system access; end-user login on Helsenorge can still involve other components (see notes below).

See also: [AMQP Authentication](../AMQP_Auth/) for Helsenorge messaging (Tjenestebuss) over mutual TLS.
See also: [Test Environments](../../Test_Environments/) for endpoint URLs per environment.

## ⚠️ Important

**Requirement deadline: 1.12.2025 — HelseID is required for system-to-system access to Helsenorge/NHN APIs (with documented exceptions).**

Notes from the requirement documentation:

- Helsenorge historically had an "Innbygger STS"; HelseID is now the required mechanism for system-to-system access.
- "Innbygger STS" can still be relevant for Helsenorge login flows.
- Exceptions exist for certain clients (see the "Unntak" section in the source).

## Authentication types

### System-to-System (Machine-to-Machine)

- For server-to-server API calls
- Uses OAuth 2.0 client credentials flow
- Required when accessing NHN/Helsenorge APIs in system-to-system context (per requirements)

## Implementation Requirements

### For System-to-System Access

1. Register your system in the HelseID portal
2. Obtain client credentials (client_id, client_secret or certificate)
3. Request appropriate scopes for your API needs
4. Implement token acquisition flow
5. Include bearer token in API requests

## Token Flow

Reference: [HelseID_Auth_Flow.mmd](./HelseID_Auth_Flow.mmd) (click to view flow in Mermaid)

```
┌─────────────┐                          ┌─────────────┐
│   Your      │  1. Request Token        │   HelseID   │
│   System    │ ───────────────────────► │   Server    │
│             │  (client credentials)    │             │
│             │                          │             │
│             │  2. Access Token         │             │
│             │ ◄─────────────────────── │             │
└─────────────┘                          └─────────────┘
       │
       │ 3. API Request with Bearer Token
       ▼
┌─────────────┐
│  NHN API    │
│  (Protected)│
└─────────────┘
```

## Scopes

Request only the scopes required by the specific API(s) you are calling. Scope names and availability are defined by NHN/Helsenorge for each API/client and may vary by environment.

## Sources

- Krav til bruk av HelseID for system-til-system tilgang til APIer: https://helsenorge.atlassian.net/wiki/spaces/HELSENORGE/pages/2663776258/Krav+til+bruk+av+HelseID+for+system+til+system+tilgang+til+APIer
- Systemdokumentasjon for integrasjon med Helsenorge (overview): https://helsenorge.atlassian.net/wiki/spaces/HELSENORGE/overview?mode=global

## Environment-Specific HelseID Endpoints

| Environment | HelseID STS URL                 |
| ----------- | ------------------------------- |
| TEST1       | https://helseid-sts.test.nhn.no |
| TEST2       | https://helseid-sts.test.nhn.no |
| QA          | https://helseid-sts.qa.nhn.no   |
| PROD        | https://helseid-sts.nhn.no      |

## Security Best Practices

- Store credentials securely (use secrets management)
- Rotate client secrets periodically
- Use certificate-based authentication for higher security
- Implement proper token caching (respect expiry)
- Log authentication failures for monitoring
