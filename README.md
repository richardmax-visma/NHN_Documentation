# NHN Documentation

Mermaid diagrams and documentation for Norsk Helsenett (NHN) integrations.

---

## Spike goal (phase 1)

- High-level objective: enable secure, bidirectional messaging between citizens (via Helsenorge/DigiHelse) and municipal providers.
- Approach/services: use E-kontakt AMQP for messaging; use HelsenorgeAktivSjekken to check digital reachability; add Helsekontakt variants only if NHN requires them.
- Access prerequisites (blocking): request HelseID client credentials (client ID/secret + scopes for test) and NHN AMQP cert/key + queue/vhost config so we can connect to test and validate flows.
- Working mode: start in test environments; confirm scopes, queues, and payload shapes before production.

---

## Authentication (prerequisite)

- **Before calling any NHN APIs, set up auth for both channels: HelseID (tokens) for REST/FHIR and mTLS (certs) for AMQP.**
  - REST/FHIR (e.g., HelsenorgeAktivSjekken, Helsekontakt Medlemstjenester): OAuth2 client-credentials via HelseID → short-lived bearer tokens per request.
  - AMQP (e.g., E-kontakt, Helsekontakt AMQP flows): mutual TLS with NHN-issued client cert/key plus queue/vhost ACLs → no bearer tokens inside messages.

🔐 [HelseID Auth](./Authentication/HelseID_Auth/)
🔒 [AMQP Auth](./Authentication/AMQP_Auth/)

## APIs

### HelsenorgeAktivSjekken

Check if citizens are digitally active on Helsenorge.

📁 [Documentation](./APIs/HelsenorgeAktivSjekken/)

| Diagram                                                               | Description             |
| --------------------------------------------------------------------- | ----------------------- |
| [Flow](./APIs/HelsenorgeAktivSjekken/HelsenorgeAktivSjekken_Flow.mmd) | REST API sequence       |
| [Class Relations](./APIs/HelsenorgeAktivSjekken/Relations/)           | Request/Response models |

---

### Helsekontakt

Citizen's entry point for digital healthcare communication.

Helsekontakt consists of three APIs: **Tjenesteoversikt** (AMQP), **Medlemstjenester** (REST + FHIR), and **Notifikasjon Helsekontakt** (AMQP + FHIR).

_Prerequisite: run HelsenorgeAktivSjekken first to confirm the citizen can be reached digitally (self or via representative) before sending notifications/messages._

📁 [Documentation](./APIs/Helsekontakt/)

#### Helsekontakt — Tjenesteoversikt (AMQP)

📁 [Docs](./APIs/Helsekontakt/AMQP%20Tjenesteoversikt/)

| Diagram                                                                            | Description                               |
| ---------------------------------------------------------------------------------- | ----------------------------------------- |
| [Flow](./APIs/Helsekontakt/AMQP%20Tjenesteoversikt/AMQP_Tjenesteoversikt_Flow.mmd) | AMQP message flow for home care services  |
| [Class Relations](./APIs/Helsekontakt/AMQP%20Tjenesteoversikt/Relations/)          | MsgHead and Applikasjonskvittering models |

#### Helsekontakt — Medlemstjenester (REST + FHIR)

📁 [Docs](./APIs/Helsekontakt/Medlemstjenester/)

| Diagram                                                                | Description                                    |
| ---------------------------------------------------------------------- | ---------------------------------------------- |
| [Flow](./APIs/Helsekontakt/Medlemstjenester/Medlemstjenester_Flow.mmd) | FHIR bundle flow for membership services       |
| [Class Relations](./APIs/Helsekontakt/Medlemstjenester/Relations/)     | HealthcareService, Patient, and related models |

#### Helsekontakt — Notifikasjon (AMQP + FHIR)

📁 [Docs](./APIs/Helsekontakt/AMQP%20Notifikasjon%20Helsekontakt/)

| Diagram                                                                                   | Description                                   |
| ----------------------------------------------------------------------------------------- | --------------------------------------------- |
| [Flow](./APIs/Helsekontakt/AMQP%20Notifikasjon%20Helsekontakt/AMQP_Notifikasjon_Flow.mmd) | Notification flow with MsgHead + FHIR payload |
| [Class Relations](./APIs/Helsekontakt/AMQP%20Notifikasjon%20Helsekontakt/Relations/)      | EpisodeOfCare and related models              |

---

### E-kontakt

Bidirectional administrative messaging between citizens and healthcare providers.

_Prerequisite: run HelsenorgeAktivSjekken to verify the citizen’s digital reachability and channel before sending AMQP messages._

📁 [Documentation](./APIs/Ekontakt/)

| Diagram                                                                        | Description             |
| ------------------------------------------------------------------------------ | ----------------------- |
| [Flow](./APIs/Ekontakt/Ekontakt_Flow.mmd)                                      | AMQP message flow       |
| [Citizen-initiated](./APIs/Ekontakt/Relations/CitizenInitiatedRelations.mmd)   | Citizen → Provider flow |
| [Provider-initiated](./APIs/Ekontakt/Relations/ProviderInitiatedRelations.mmd) | Provider → Citizen flow |

## Test Environments

Environment reference and endpoints: [Test Environments](./Test_Environments/) (MAS-02, TEST1, TEST2, QA, Prodkopi, PROD).

## Quick Reference

| API                                                                          | Tech      | Purpose                              |
| ---------------------------------------------------------------------------- | --------- | ------------------------------------ |
| [HelsenorgeAktivSjekken](./APIs/HelsenorgeAktivSjekken/)                     | REST      | Check if citizen is digitally active |
| [AMQP Tjenesteoversikt](./APIs/Helsekontakt/AMQP%20Tjenesteoversikt/)        | AMQP      | Home care health contacts            |
| [Medlemstjenester](./APIs/Helsekontakt/Medlemstjenester/)                    | REST+FHIR | Membership-based health services     |
| [AMQP Notifikasjon](./APIs/Helsekontakt/AMQP%20Notifikasjon%20Helsekontakt/) | AMQP+FHIR | General health contact notifications |
| [E-kontakt](./APIs/Ekontakt/)                                                | AMQP      | Administrative citizen messaging     |

### Auth per API (quick view)

| API                                                                                  | Tech      | Auth                                                                                         |
| ------------------------------------------------------------------------------------ | --------- | -------------------------------------------------------------------------------------------- |
| [HelsenorgeAktivSjekken](./APIs/HelsenorgeAktivSjekken/)                             | REST      | [HelseID (tokens)](./Authentication/HelseID_Auth/)                                           |
| [Helsekontakt Medlemstjenester](./APIs/Helsekontakt/Medlemstjenester/)               | REST+FHIR | [HelseID (tokens)](./Authentication/HelseID_Auth/)                                           |
| [Helsekontakt Tjenesteoversikt](./APIs/Helsekontakt/AMQP%20Tjenesteoversikt/)        | AMQP      | [AMQP mTLS](./Authentication/AMQP_Auth/)                                                     |
| [Helsekontakt Notifikasjon](./APIs/Helsekontakt/AMQP%20Notifikasjon%20Helsekontakt/) | AMQP+FHIR | [AMQP mTLS](./Authentication/AMQP_Auth/); [HelseID (tokens)](./Authentication/HelseID_Auth/) |
| [E-kontakt](./APIs/Ekontakt/)                                                        | AMQP      | [AMQP mTLS](./Authentication/AMQP_Auth/)                                                     |

## Viewing Diagrams

The `.mmd` files are Mermaid diagrams. You can view them:

- **VS Code**: Install "Mermaid Preview" extension
- **GitHub**: Renders automatically in preview
- **Online**: Paste into [Mermaid Live Editor](https://mermaid.live)
