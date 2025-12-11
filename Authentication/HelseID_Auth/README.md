# HelseID Authentication Reference

HelseID is Norway's national authentication service for the health sector, providing secure identity verification for both users and systems.

## When to use

- Any system-to-system (machine-to-machine) API call to NHN/Helsenorge.
- User authentication flows for healthcare applications.

See also: [Test Environments](../Test_Environments/README.md) for endpoint URLs per environment.

## ⚠️ Important

**As of December 1, 2025, all healthcare actors must use HelseID for system-to-system API access.**

## Authentication types

### 1. User Authentication

- For end-user login flows
- Supports Norwegian national ID providers

### 2. System-to-System (Machine-to-Machine)

- For server-to-server API calls
- Uses OAuth 2.0 client credentials flow
- Required for all NHN API integrations

## Implementation Requirements

### For System-to-System Access

1. Register your system in the HelseID portal
2. Obtain client credentials (client_id, client_secret or certificate)
3. Request appropriate scopes for your API needs
4. Implement token acquisition flow
5. Include bearer token in API requests

## Token Flow

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

Request only the scopes needed for your integration:

- Helsenorge APIs
- AMQP messaging
- FHIR resources
- Specific service endpoints

## Sources

- Krav til bruk av HelseID for system-til-system tilgang til APIer: https://helsenorge.atlassian.net/wiki/spaces/HELSENORGE/pages/2663776258/Krav+til+bruk+av+HelseID+for+system+til+system+tilgang+til+APIer
- Systemdokumentasjon for integrasjon med Helsenorge (overview): https://helsenorge.atlassian.net/wiki/spaces/HELSENORGE/overview?mode=global

## Environment-Specific HelseID Endpoints

| Environment | HelseID Base URL                |
| ----------- | ------------------------------- |
| TEST1       | https://helseid-sts.test.nhn.no |
| TEST2       | https://helseid-sts.test.nhn.no |
| QA          | https://helseid-sts.qa.nhn.no   |
| PROD        | https://helseid-sts.nhn.no      |

## Migration Notes

If currently using basic authentication or other methods:

1. Register in HelseID portal
2. Update authentication flow
3. Test in TEST1/TEST2 environment
4. Validate in QA
5. Deploy to production before deadline

## Security Best Practices

- Store credentials securely (use secrets management)
- Rotate client secrets periodically
- Use certificate-based authentication for higher security
- Implement proper token caching (respect expiry)
- Log authentication failures for monitoring
