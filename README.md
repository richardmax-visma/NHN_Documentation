# NHN Documentation

Mermaid diagrams and documentation for Norsk Helsenett (NHN) APIs.

## APIs

### HelsenorgeAktivSjekken

Check if citizens are digitally active on Helsenorge.

📁 [Documentation](./diagrams/HelsenorgeAktivSjekken/HelsenorgeAktivSjekken_README.md)

| Diagram                                                                         | Description             |
| ------------------------------------------------------------------------------- | ----------------------- |
| [Flow](./diagrams/HelsenorgeAktivSjekken/HelsenorgeAktivSjekken_Flow.mmd)       | REST API sequence       |
| [Classes](./diagrams/HelsenorgeAktivSjekken/HelsenorgeAktivSjekken_Classes.mmd) | Request/Response models |

---

### Helsekontakt

Citizen's entry point for digital healthcare communication.

📁 [Documentation](./diagrams/Helsekontakt/README.md)

| Sub-API               | Technology  | Documentation                                                                                  |
| --------------------- | ----------- | ---------------------------------------------------------------------------------------------- |
| AMQP Tjenesteoversikt | AMQP        | [Docs](./diagrams/Helsekontakt/AMQP%20Tjenesteoversikt/AMQP_Tjenesteoversikt_README.md)        |
| Medlemstjenester      | FHIR        | [Docs](./diagrams/Helsekontakt/Medlemstjenester/Medlemstjenester_README.md)                    |
| AMQP Notifikasjon     | AMQP + FHIR | [Docs](./diagrams/Helsekontakt/AMQP%20Notifikasjon%20Helsekontakt/AMQP_Notifikasjon_README.md) |

---

### E-kontakt

Bidirectional administrative messaging between citizens and healthcare providers.

📁 [Documentation](./diagrams/Ekontakt/Ekontakt_README.md)

| Diagram | Description |
| ------- | ----------- |
| [Flow](./diagrams/Ekontakt/Ekontakt_Flow.mmd) | AMQP message flow |
| [Classes](./diagrams/Ekontakt/Ekontakt_Classes.mmd) | Message data models |

---

## Reference Documentation

| Document | Description |
| -------- | ----------- |
| [HelseID Authentication](./diagrams/_Reference/HelseID_Auth.md) | System-to-system authentication (deadline: 1.12.2025) |
| [Test Environments](./diagrams/_Reference/Test_Environments.md) | MAS-02, TEST1, TEST2, QA, Prodkopi, PROD |

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
