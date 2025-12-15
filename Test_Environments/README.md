# NHN Test Environments Reference

NHN provides multiple test environments for development and validation of Helsenorge integrations.

## When to use

- Determine which environment to target during development, testing, or production.
- Find base URLs for EksternAPI (REST/FHIR), AMQP (Tjenestebuss), and HelseID token endpoints.

See also: [HelseID Authentication](../Authentication/HelseID_Auth/) for REST/FHIR tokens and [AMQP Authentication](../Authentication/AMQP_Auth/) for mTLS certs/queues.

## Environment summary

| Environment | Purpose                         | Stability      | Typical use                                                 |
| ----------- | ------------------------------- | -------------- | ----------------------------------------------------------- |
| MAS-02      | Development / early validation  | Very low       | Sprint/dev testing when newest code is needed               |
| TEST1       | New functionality test          | Low            | Integration/performance/security testing for “next” release |
| TEST2       | Regression + integration (prod) | Medium         | Most common environment for external integrations           |
| QA          | Pre-production verification     | High           | Final verification shortly before production deployment     |
| Prodkopi    | Production copy                 | High (limited) | Debugging/verification with same code as production         |
| PROD        | Production                      | High           | Live services (no testing)                                  |

## Environment Details

### MAS-02 (Development)

- **Purpose:** Early development and prototyping
- **Stability:** Very low (continuous deploys; can be unstable)
- **Data:** Synthetic test data only

### TEST1

- **Purpose:** Test environment for new Helsenorge functionality
- **Stability:** Low ("next" release; may be changed manually by teams)
- **Data:** Synthetic test data

### TEST2

- **Purpose:** Regression testing and integration with services available in production
- **Stability:** Medium
- **Data:** Synthetic test data

### QA (Quality Assurance)

- **Purpose:** Pre-production validation
- **Stability:** High (production-like)
- **Data:** Synthetic test data
- **Note:** Final testing before production deployment

### Prodkopi (Production Copy)

- **Purpose:** Production simulation
- **Stability:** High (typically limited opening hours)
- **Data:** Anonymized production data copy
- **Note:** Closest to real production behavior

### PROD (Production)

- **Purpose:** Live services
- **Stability:** High
- **Data:** Real citizen/patient data
- **Note:** Only for validated, approved systems

## Base URLs

These are the **EksternAPI** base URLs used for API calls over the internet. (Helsenorge web URLs like `helsenorge.no` are user-facing and not the API base URL.)

| Environment | EksternAPI Base URL                             |
| ----------- | ----------------------------------------------- |
| MAS-02      | https://eksternapi-hn-mas-02.int-hn.nhn.no      |
| TEST1       | https://eksternapi.hn.test.nhn.no               |
| TEST2       | https://eksternapi.hn2.test.nhn.no              |
| QA          | https://eksternapi.hn.qa.nhn.no                 |
| Prodkopi    | https://eksternapi-hn-prodkopi-01.int-hn.nhn.no |
| PROD        | https://eksternapi.helsenorge.no                |

Note: Some endpoints are also available on Helsenett with separate `eksternapi-helsenett.*` base URLs.

## AMQP Endpoints

Use mutual TLS with NHN-issued cert/key.

The Atlassian docs describe **one broker host for test** and **one for production** (port `5671`). In practice this is AMQP over TLS (often written as `amqps://`), but the exact URI scheme varies by client library.

| Scope | AMQP Host      | Port | Notes                                                    |
| ----- | -------------- | ---- | -------------------------------------------------------- |
| Test  | tb.test.nhn.no | 5671 | Available on both internet and Helsenett (different IPs) |
| Prod  | tb.nhn.no      | 5671 | Available on Helsenett                                   |

## HelseID Endpoints

| Scope | Token endpoint                                |
| ----- | --------------------------------------------- |
| Test  | https://helseid-sts.test.nhn.no/connect/token |
| Prod  | https://helseid-sts.nhn.no/connect/token      |

## Test Users

Test environments provide synthetic test users (test-fødselsnummer) for development.
Contact NHN for access to test user credentials.

## HERID (Adresseregister)

Each organization must register their HERID for messaging:

- Test HERIDs are separate from production
- Register in each environment you need access to

## Recommended Development Flow

```
MAS-02 ──► TEST1/TEST2 ──► QA ──► Prodkopi ──► PROD
  │            │           │         │          │
  └── Dev ─────┴── Test ───┴── Validate ───────┴── Live
```

## Access Requirements

1. **Connectivity:** Agreement with NHN/Helsenett and access to relevant services (e.g., Tjenestebuss for AMQP)
2. **Certificates:** Obtain and maintain a valid virksomhetssertifikat (mTLS) for AMQP usage
3. **Address registry:** Ensure correct registrations in NHN Adresseregisteret (HERID, endpoints, roles)
4. **HelseID:** Obtain HelseID client credentials (client ID/secret + scopes) for REST/FHIR APIs
5. **Firewall:** Open/whitelist required IPs/ports per environment (see sources)

## Sources

- Testmiljøer og endepunkter: https://helsenorge.atlassian.net/wiki/spaces/HELSENORGE/pages/1552384092/Testmilj+er+og+endepunkter
- Meldingsutveksling med Helsenorge (AMQP + firewall openings): https://helsenorge.atlassian.net/wiki/spaces/HELSENORGE/pages/690913297/Meldingsutveksling+med+Helsenorge
- Systemdokumentasjon for integrasjon med Helsenorge (overview): https://helsenorge.atlassian.net/wiki/spaces/HELSENORGE/overview?mode=global
