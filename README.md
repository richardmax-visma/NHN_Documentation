# NHN Documentation

Mermaid diagrams and documentation for Norsk Helsenett (NHN) integrations.

## Spike goal (phase 1)

- High-level objective: enable secure, bidirectional messaging between citizens (via Helsenorge/DigiHelse) and municipal providers.
- Approach/services: use E-kontakt AMQP for messaging; use HelsenorgeAktivSjekken to check digital reachability; add Helsekontakt variants only if NHN requires them.
- Access prerequisites (blocking): request HelseID client credentials (client ID/secret + scopes for test) and NHN AMQP cert/key + queue/vhost config so we can connect to test and validate flows.
- Working mode: start in test environments; confirm scopes, queues, and payload shapes before production.

## Authentication (prerequisite)

HelseID is required before any API calls. Auth docs live separately under `DigiHealth/Authentication/HelseID/` because every service depends on it.

📁 [HelseID Folder](./DigiHealth/Authentication/HelseID/)

| Document                                                                      | Description                               |
| ----------------------------------------------------------------------------- | ----------------------------------------- |
| [Authentication](./DigiHealth/Authentication/HelseID/HelseID_Auth.md)         | System-to-system authentication (HelseID) |
| [Test Environments](./DigiHealth/Authentication/HelseID/Test_Environments.md) | MAS-02, TEST1, TEST2, QA, Prodkopi, PROD  |

## APIs

### HelsenorgeAktivSjekken

Check if citizens are digitally active on Helsenorge.

📁 [Documentation](./DigiHealth/APIs/HelsenorgeAktivSjekken/HelsenorgeAktivSjekken_README.md)

| Diagram                                                                                  | Description             |
| ---------------------------------------------------------------------------------------- | ----------------------- |
| [Flow](./DigiHealth/APIs/HelsenorgeAktivSjekken/HelsenorgeAktivSjekken_Flow.mmd)         | REST API sequence       |
| [Class Relations](./DigiHealth/APIs/HelsenorgeAktivSjekken/Relations/ClassRelations.mmd) | Request/Response models |

---

### Helsekontakt

Citizen's entry point for digital healthcare communication.

📁 [Documentation](./DigiHealth/APIs/Helsekontakt/README.md)

| Sub-API               | Technology  | Documentation                                                                                         |
| --------------------- | ----------- | ----------------------------------------------------------------------------------------------------- |
| AMQP Tjenesteoversikt | AMQP        | [Docs](./DigiHealth/APIs/Helsekontakt/AMQP%20Tjenesteoversikt/AMQP_Tjenesteoversikt_README.md)        |
| Medlemstjenester      | FHIR        | [Docs](./DigiHealth/APIs/Helsekontakt/Medlemstjenester/Medlemstjenester_README.md)                    |
| AMQP Notifikasjon     | AMQP + FHIR | [Docs](./DigiHealth/APIs/Helsekontakt/AMQP%20Notifikasjon%20Helsekontakt/AMQP_Notifikasjon_README.md) |

---

### E-kontakt

Bidirectional administrative messaging between citizens and healthcare providers.

📁 [Documentation](./DigiHealth/APIs/Ekontakt/Ekontakt_README.md)

| Diagram                                                                                   | Description             |
| ----------------------------------------------------------------------------------------- | ----------------------- |
| [Flow](./DigiHealth/APIs/Ekontakt/Ekontakt_Flow.mmd)                                      | AMQP message flow       |
| [Citizen-initiated](./DigiHealth/APIs/Ekontakt/Relations/CitizenInitiatedRelations.mmd)   | Citizen → Provider flow |
| [Provider-initiated](./DigiHealth/APIs/Ekontakt/Relations/ProviderInitiatedRelations.mmd) | Provider → Citizen flow |

---

---

## Quick Reference

| API                    | Tech      | Purpose                              |
| ---------------------- | --------- | ------------------------------------ |
| HelsenorgeAktivSjekken | REST      | Check if citizen is digitally active |
| AMQP Tjenesteoversikt  | AMQP      | Home care health contacts            |
| Medlemstjenester       | FHIR      | Membership-based health services     |
| AMQP Notifikasjon      | AMQP+FHIR | General health contact notifications |
| E-kontakt              | AMQP      | Administrative citizen messaging     |

## Viewing Diagrams

The `.mmd` files are Mermaid diagrams. You can view them:

- **VS Code**: Install "Mermaid Preview" extension
- **GitHub**: Renders automatically in preview
- **Online**: Paste into [Mermaid Live Editor](https://mermaid.live)
