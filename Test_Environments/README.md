# NHN Test Environments Reference

NHN provides multiple test environments for development and validation of Helsenorge integrations.

## When to use

- Determine which environment to target during development, testing, or production.
- Find base URLs for Helsenorge, AMQP, and HelseID endpoints.

See also: [HelseID Authentication](../Authentication/HelseID_Auth/) for REST/FHIR tokens and [AMQP Authentication](../Authentication/AMQP_Auth/) for mTLS certs/queues.

## Environment summary

| Environment | Purpose           | Stability | Use Case                       |
| ----------- | ----------------- | --------- | ------------------------------ |
| MAS-02      | Development       | Low       | Early development, prototyping |
| TEST1       | Integration       | Medium    | Integration testing            |
| TEST2       | Integration       | Medium    | Integration testing            |
| QA          | Quality Assurance | High      | Pre-production validation      |
| Prodkopi    | Production Copy   | High      | Production simulation          |
| PROD        | Production        | Highest   | Live services                  |

## Environment Details

### MAS-02 (Development)

- **Purpose:** Early development and prototyping
- **Stability:** May have frequent changes/resets
- **Data:** Synthetic test data only

### TEST1

- **Purpose:** Integration testing
- **Stability:** Generally stable
- **Data:** Synthetic test data

### TEST2

- **Purpose:** Integration testing (parallel to TEST1)
- **Stability:** Generally stable
- **Data:** Synthetic test data

### QA (Quality Assurance)

- **Purpose:** Pre-production validation
- **Stability:** High - mirrors production
- **Data:** Synthetic test data
- **Note:** Final testing before production deployment

### Prodkopi (Production Copy)

- **Purpose:** Production simulation
- **Stability:** High
- **Data:** Anonymized production data copy
- **Note:** Closest to real production behavior

### PROD (Production)

- **Purpose:** Live services
- **Stability:** Highest
- **Data:** Real citizen/patient data
- **Note:** Only for validated, approved systems

## Base URLs

| Environment | Helsenorge Base URL            |
| ----------- | ------------------------------ |
| MAS-02      | https://mas-02.helsenorge.no   |
| TEST1       | https://test1.helsenorge.no    |
| TEST2       | https://test2.helsenorge.no    |
| QA          | https://qa.helsenorge.no       |
| Prodkopi    | https://prodkopi.helsenorge.no |
| PROD        | https://helsenorge.no          |

## AMQP Endpoints

Use mutual TLS with NHN-issued cert/key and the queue/vhost config NHN provides.

| Environment | AMQP Host               |
| ----------- | ----------------------- |
| MAS-02      | amqp://mas-02.mq.nhn.no |
| TEST1       | amqp://test1.mq.nhn.no  |
| TEST2       | amqp://test2.mq.nhn.no  |
| QA          | amqp://qa.mq.nhn.no     |
| PROD        | amqp://mq.nhn.no        |

## HelseID Endpoints

| Environment | HelseID STS URL                 |
| ----------- | ------------------------------- |
| TEST1/TEST2 | https://helseid-sts.test.nhn.no |
| QA          | https://helseid-sts.qa.nhn.no   |
| PROD        | https://helseid-sts.nhn.no      |

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

1. **Agreement:** Sign data processor agreement with NHN
2. **Registration:** Register in Adresseregisteret (Address Registry)
3. **HelseID:** Configure HelseID client for each environment
4. **Firewall:** Whitelist NHN IP ranges if needed

## Sources

- Testmiljøer og endepunkter: https://helsenorge.atlassian.net/wiki/spaces/HELSENORGE/pages/1552384092/Testmilj+er+og+endepunkter
- Systemdokumentasjon for integrasjon med Helsenorge (overview): https://helsenorge.atlassian.net/wiki/spaces/HELSENORGE/overview?mode=global
