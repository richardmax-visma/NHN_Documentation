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

🔐 [HelseID Auth](./DigiHealth/Authentication/HelseID_Auth/README.md)
🔒 [AMQP Auth](./DigiHealth/Authentication/AMQP_Auth/README.md)

## APIs

### HelsenorgeAktivSjekken

Check if citizens are digitally active on Helsenorge.

📁 [Documentation](./DigiHealth/APIs/HelsenorgeAktivSjekken/README.md)

| Diagram                                                                                  | Description             |
| ---------------------------------------------------------------------------------------- | ----------------------- |
| [Flow](./DigiHealth/APIs/HelsenorgeAktivSjekken/HelsenorgeAktivSjekken_Flow.mmd)         | REST API sequence       |
| [Class Relations](./DigiHealth/APIs/HelsenorgeAktivSjekken/Relations/ClassRelations.mmd) | Request/Response models |

---

### Helsekontakt

Citizen's entry point for digital healthcare communication.

_Prerequisite: run HelsenorgeAktivSjekken first to confirm the citizen can be reached digitally (self or via representative) before sending notifications/messages._

📁 [Documentation](./DigiHealth/APIs/Helsekontakt/README.md)

| Sub-API                                                                                                            | Tech      | Purpose                          |
| ------------------------------------------------------------------------------------------------------------------ | --------- | -------------------------------- |
| [AMQP Tjenesteoversikt](./DigiHealth/APIs/Helsekontakt/AMQP%20Tjenesteoversikt/AMQP_Tjenesteoversikt_README.md)    | AMQP      | Home care service overview       |
| [Medlemstjenester](./DigiHealth/APIs/Helsekontakt/Medlemstjenester/Medlemstjenester_README.md)                     | FHIR      | Membership-based health services |
| [AMQP Notifikasjon](./DigiHealth/APIs/Helsekontakt/AMQP%20Notifikasjon%20Helsekontakt/AMQP_Notifikasjon_README.md) | AMQP+FHIR | General notifications            |

---

### E-kontakt

Bidirectional administrative messaging between citizens and healthcare providers.

_Prerequisite: run HelsenorgeAktivSjekken to verify the citizen’s digital reachability and channel before sending AMQP messages._

📁 [Documentation](./DigiHealth/APIs/Ekontakt/README.md)

| Diagram                                                                                   | Description             |
| ----------------------------------------------------------------------------------------- | ----------------------- |
| [Flow](./DigiHealth/APIs/Ekontakt/Ekontakt_Flow.mmd)                                      | AMQP message flow       |
| [Citizen-initiated](./DigiHealth/APIs/Ekontakt/Relations/CitizenInitiatedRelations.mmd)   | Citizen → Provider flow |
| [Provider-initiated](./DigiHealth/APIs/Ekontakt/Relations/ProviderInitiatedRelations.mmd) | Provider → Citizen flow |

## Test Environments

Environment reference and endpoints: [Test Environments](./DigiHealth/Test_Environments/README.md) (MAS-02, TEST1, TEST2, QA, Prodkopi, PROD).

## Quick Reference

| API                                                                                                                | Tech      | Purpose                              |
| ------------------------------------------------------------------------------------------------------------------ | --------- | ------------------------------------ |
| [HelsenorgeAktivSjekken](./DigiHealth/APIs/HelsenorgeAktivSjekken/README.md)                                       | REST      | Check if citizen is digitally active |
| [AMQP Tjenesteoversikt](./DigiHealth/APIs/Helsekontakt/AMQP%20Tjenesteoversikt/AMQP_Tjenesteoversikt_README.md)    | AMQP      | Home care health contacts            |
| [Medlemstjenester](./DigiHealth/APIs/Helsekontakt/Medlemstjenester/Medlemstjenester_README.md)                     | FHIR      | Membership-based health services     |
| [AMQP Notifikasjon](./DigiHealth/APIs/Helsekontakt/AMQP%20Notifikasjon%20Helsekontakt/AMQP_Notifikasjon_README.md) | AMQP+FHIR | General health contact notifications |
| [E-kontakt](./DigiHealth/APIs/Ekontakt/README.md)                                                                  | AMQP      | Administrative citizen messaging     |

### Auth per API (quick view)

| API                                                                                                                        | Tech      | Auth                                                                                                               |
| -------------------------------------------------------------------------------------------------------------------------- | --------- | ------------------------------------------------------------------------------------------------------------------ |
| [HelsenorgeAktivSjekken](./DigiHealth/APIs/HelsenorgeAktivSjekken/README.md)                                               | REST      | [HelseID (tokens)](./DigiHealth/Authentication/HelseID_Auth/)                                                      |
| [Helsekontakt Medlemstjenester](./DigiHealth/APIs/Helsekontakt/Medlemstjenester/Medlemstjenester_README.md)                | FHIR/REST | [HelseID (tokens)](./DigiHealth/Authentication/HelseID_Auth/)                                                      |
| [Helsekontakt Tjenesteoversikt](./DigiHealth/APIs/Helsekontakt/AMQP%20Tjenesteoversikt/AMQP_Tjenesteoversikt_README.md)    | AMQP      | [AMQP mTLS](./DigiHealth/Authentication/AMQP_Auth/)                                                                |
| [Helsekontakt Notifikasjon](./DigiHealth/APIs/Helsekontakt/AMQP%20Notifikasjon%20Helsekontakt/AMQP_Notifikasjon_README.md) | AMQP+FHIR | [AMQP mTLS](./DigiHealth/Authentication/AMQP_Auth/); [HelseID (tokens)](./DigiHealth/Authentication/HelseID_Auth/) |
| [E-kontakt](./DigiHealth/APIs/Ekontakt/README.md)                                                                          | AMQP      | [AMQP mTLS](./DigiHealth/Authentication/AMQP_Auth/)                                                                |

## Viewing Diagrams

The `.mmd` files are Mermaid diagrams. You can view them:

- **VS Code**: Install "Mermaid Preview" extension
- **GitHub**: Renders automatically in preview
- **Online**: Paste into [Mermaid Live Editor](https://mermaid.live)
